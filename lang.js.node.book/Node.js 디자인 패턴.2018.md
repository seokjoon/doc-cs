# 1장. Node.js 플랫폼에 오신 것을 환영합니다

## 1.2
* 글래스 구문
    * class Foo { constructor() {} f1() {} static f2() {} }
    * class FooChild extends Foo {}


## 1.3 Reactor 패턴
* 논 블로킹 I/O, 이벤트 디멀티플렉싱, Reactor 패턴 소개
* Node.js의 논 블로킹 엔진 libuv, Node.js를 위한 구조


# 2장. Node.js 필수 패턴

## 2.1 콜백 패턴
* 연속 전달 방식, 동기냐? 비동기냐?
    * 지연 실행: 비동기
        * process.nextTick(() => callback);
        * setImmediate()
    * Node.js 콜백 규칙: 인수의 처음은 오류/마지막은 콜백, 오류 전파는 호출 체인의 다음에서 콜백으로
    * 동기와 비동기를 (if로) 섞지 않음

## 2.2 모듈 시스템과 그 패턴
* 노출식 모듈 패턴: const mod = (() => { const foo = []; const bar = { getFoo: () => {}, }; return bar; })();
* Node.js 모듈 설명

* 모듈 정의 패턴
    * exports 지정하기: exports.foo = () => {};
        * 사용: 모듈의 속성처럼: const foo = require('./foo'); foo.bar();
    * 함수 내보내기: module.exports = () => {}; module.exports.foo = () => {};
        * 사용: const foo = require('./foo'); foo();
    * 생성자 내보내기
        * function foo() {}; module.exports = foo;
        * class foo {}; module.exports = foo;
            * 사용: const foo = require('./foo'); const bar = new Foo(); bar.test();
        * function Foo(bar) { if(!(this instanceof Foo)) return new Foo(bar); this.bar = bar; };
        * function Foo(bar) { if(!(new.target)) return new FooConstructor(bar); this.bar = bar; }
            * 사용: 팩토리로: const Foo = require('./foo'); const bar = Foo('hmm'); bar.test();
    * 인스턴스 내보내기: function foo(bar) {}; module.exports = new Foo('test');
        * 사용: const foo = require('./foo'); foo.bar();

## 2.3 관찰자 패턴
* EventEmitter 클래스: 패턴은 이미 코어에 내장, 1개 이상 함수를 리스너로 등록 가능
    * const ee = require('events').EventEmitter; const ei = new ee();
    * on(), once(), removeListener(): params: event, listener
    * emit(): params: event, [arg1], [...]
* EventEmitter 생성 및 사용
    * function foo() { const bar = new ee(); bar.emit('e1', p1); bar.emit('e2', p2); return bar; }
    * foo().on('e1', 'test').on('e2', 'test');
* 오류 전파: 비동기 발생 오류를 에러 이벤트 리스너로
* 관찰 가능한 객체 만들기
    * class Foo extends ee { bar() { this.emit('e1', p1); } }
    * const foo = new Foo(); foo.bar().on('e1', 'test');
* 동기 및 비동기 이벤트: 두 가지를 섞으면 안됨, 동기시 이벤트 방출 전 모든 리스너 등록, 비동기시 초기화 이후에도 새 리스너 등록 가능
* EventEmitter vs 콜백
* 콜백과 EventEmitter의 결합


# 3장. 콜백을 사용한 비동기 제어 흐름 패턴
 
## 3.1 비동기 프로그래밍의 어려움
* 간단한 웹 스파이더 만들기
* 콜백 헬: asyncA(err => { asyncB(err => { asyncC(err) => { ... } }) });
 
## 3.2 일반 JavaScript의 사용
* 콜백 규칙: 함부로 클로저를 사용하지 않음, 빨리 종료(return, ccontinue, break), 콜백은 클로저 외부에 배치되고 명명된 함수 & 중간 결과를 인자로 전달, 함수들로 모듈화
* 순차 실행
* 병렬 실행: 논 블로킹: 순차 재귀를 한번에 생성으로 변경, 모든(혹은 일정 개수) 작업 완료시 최종 콜백 호출
* 제한된 병렬 실행: 동시실행 개수 제한: 큐
 
## 3.3 비동기 라이브러리
* 순차 실행: eachSeries(), mapSeries(), filterSeries(), rejectSeries(), reduct(), reduceRight(), detectSeries(), concatSeries(), series(), whilst(), odWhilst(), until(), doUntil(), forever(), waterfall(), compose(), seq(), applyEachSeries(), iterator(), timesSeries()
* 병렬 실행: each(), map(), filter(), reject(), detect(), some(), every(), concat(), parallel(), applyEach(), time(),
* 제한된 병렬 실행: eachLimit(), mapLimit(), parallelLimit(), queue(), cargo(),
 
 
# 4장. ES2015 이후 비동기식 프로그램의 제어 흐름 패턴: promise, generator, async await
 
## 4.1 프라미스(Promise)
* 프라미스란 무엇인가?: 함수가 Promise 객체 반환하는 추상화, 비동기 작업 결과
    * 대기중(pending)
    * 처리(settled): 이행(fullfilled), 거부(rejected)
        * promise.then(onFullfilled, onRejected): foo().then(res => {}, err => {});
        * catch 될때까지 오류 자동 전파: foo.then().then().then(bar, err => {});
* Promises/A+ 구현
    * 생성자: new Promise(function(resolve, reject) {})
    * 정적 메소드: resolve(obj), reject(err), all(iterable), race(iterable)
    * 인스턴스 메소드: then(), catch()
* Node.js 스타일 함수 프라미스화하기
    * module.exports.promisify = function(foo) { return function promisified() { return new Promise(() => { ... foo.apply(); }); } };
* 순차 실행
    * let pm = Promise.resolve(); [...].forEach(foo => pm = pm.then(() => { return foo(); }); ); pm.then(() => {});
    * let pm = [...].reduce((prev, foo) => { return foo.then(() => { return foo(); }); }, Promise.resolve()); pm.then(() => {});
* 병렬 실행: const pms = [...].map(foo => bar()); return Promise.all(pms);
* 제한된 병렬 실행
* 공개 API로 콜백과 프라미스 노출하기
    * module.exports = function foo(a,b,cb) { return new Promise(resolve, reject) => { process.nextTick() => { resolve(); } }; };
    * 콜백: foo(1,2,(err, res) => {});
    * 프라미스: foo(1,2).then(res => {}).catch(err => {})

## 4.2 제너레이터(Generator)
* 제너레이터의 기본: function* foo() { yield 'foo'; yield 'bar'; return 'foo'; } const bar = foo(); bar.next();
    * 세미 코루틴, 호출시 이외에도 진입점이 존재
    * next()가 반환하는 객체의 속성: value(yield 리턴값), done(종료 여부)
    * function* foo(arr) { for(let i = 0; i < arr.length; i++) { yield arr[i]; } };
        * const bar = foo([1,2,3]); let current = bar.next(); while(!(current.done)) { current = bar.next(); }
    * 값을 제너레이터로 전달: next() 메소드에 전달된 인자는 yield 반환값이 됨: foo.next('bar'); foo.next(new Error());
* 제너레이터를 사용한 비동기 제어 흐름: 제너레이터를 입력받아 인자로 콜백을 주고 인스턴스화 하는 함수, 비동기 작업이 완료되면 제너레이터 실행 재개
* 순차 실행, 병렬 실행: co/thunkify
* 제한된 병렬 실행: 생산자-소비자 패턴(queue-worker)
 
## 4.3 Babel을 사용한 비동기 await
* function foo() { return new Promise(function(resolve, reject) { resolve(); }) }; async function bar() { const foo = await foo(); }
* Babel의 설치 및 실행
 
## 4.4 비교
* async, promise, generator, async await

 
# 5장. 스트림 코딩
 
## 5.1 스트림의 중요성
* 버퍼링 대 스트리밍: 공간 효율성, 시간 효율성, 결합성
    * fs.readFile(file, (err, bf) => { zlib.gzip(bf, (err, bf) => { fs.writeFile(file, bf, err => {}); }); });
    * fs.createReadStream(file).pipe(zlib.createGzip()).pipe(fs.createWriteStream(file)).on('finish', () => {});
    * req.pipe(zlib.createGunzip()).pipe(fs.createWriteSteam()).on('finish', () => {});
 
## 5.2 스트림 시작하기
* 스트림의 구조: EventEmitter의 인스턴스, 바이너리 모드, 객체 모드
* Readable 스트림
    * readable.read([size])
    * 읽기
        * non-flowing 모드: process.stdin.on('readable', () => {}).on('end', () => {});
        * flowing 모드(legacy): process.stdin.on('data', chunk => {}).on('end', () => {});
    * 구현: push() 사용하는 _read() 메소드
        * class Foo extends require('stream').Readable { _read(size) { ... this.push(chunk) } }; module.exports = Foo;
            * foo.on('readable', () => { let chunk; while((chunk = foo.read()) !== null) { ... } });
* Writable 스트림
    * writable.write(chunk, [encoding], [callback]); writable.end([chunk], [encoding], [callback]);
    * ... foo.write(bar); ... foo.end(bar); res.on('finish', () => {});
    * 백프레셔: write() 메소드가 false 반환시 병목 판정으로 중단, 버퍼가 비워지면 drain 이벤트 발생
        * let bool = foo.write(); if(!(bool)) return foo.once('drain', self);
    * 구현: _write(), 인자 형식은 { path: <path>, content: <string or buffer> }
        * class Foo extends ('stream').Writable { _write(chunk, encoding, callback) {} }; module.exports = Foo;
* 양방향(Duplex) 스트림: readable/writable 모두 가능(모두 상속), 소켓 유사, _read() 와 _write() 구현
* Transform 스트림: transform() 과 _flush() 구현
 
## 5.3 스트림을 사용한 비동기 제어 흐름
* 순차 실행
* 비순차 병렬 실행
* 제한된 비순차 병렬 실행
 
## 5.4 파이프 패턴
* 스트림 결합하기: ex) 압축/암호화 pipe 해독/해제
* 스트림 포크(Fork)하기: ex) readable 1개를 writable n개로
* 스트림 병합(merge)하기
* 멀티플렉싱과 디멀티플렉싱: ex) 원격 로거
 
 
# 6장. 디자인 패턴
 
## 6.1 팩토리(Factory)
* 객체를 생성하기 위한 제너릭 인터페이스
* 캡슐화를 강제하기 위한 메커니즘
* 간단한 코드 프로파일러 작성하기
* 합성 가능한 팩토리 함수
 
## 6.2 공개 생성자(Revealing constructor)
* 생성자의 인수로 함수(executor)를 받음
 
## 6.3 프록시(Proxy)
* 다른 객체(subject)에 대한 접근을 제어하는 객체, 미들웨어
* 생태계에서의 프록시 - 함수 후크 및 AOP
* ES2015 Proxy: const foo = new Proxy(target, handler);
 
## 6.4 데코레이터(Decorator)
* 기존 객체의 동작을 동적으로 증강
 
## 6.5 어댑터(Adapter)
* 다른 인터페이스를 사용하여 대상 객체의 함수에 접근

## 6.6 전략(Strategy)
* 컨텍스트 객체로 연산 로직 변형
 
## 6.7 상태(State)
* 컨텍스트 상태에 따라 전략이 변경
 
## 6.8 템플릿(Template)
* 추상 의사 클래스 정의
 
## 6.9 미들웨어(Middleware)
* 미들웨어로서의 Express
* 패턴으로서의 미들웨어
* ØMQ용 미들웨어 프레임워크 만들기
* Koa에서 제너레이터를 사용한 미들웨어
 
## 6.10 커맨드(Command)
* 유연한 패턴
* 보다 복잡한 명령
 
 
# 7장. 모듈 연결
 
## 7.1 모듈과 의존성
* Node.js의 가장 일반적인 종속성
* 응집력과 결합력
* 상태 저장 모듈
 
## 7.2 모듈 연결 패턴
* 하드코드된 종속성
* 의존성 주입
* 서비스 로케이터
* 의존성 주입 컨테이너
 
## 7.3 연결(Wiring)을 위한 플러그인
* 패키지로서의 플러그인
* 확장 포인트
* 플러그인 제어와 어플리케이션 제어 확장
* 로그아웃 플러그인 구현하기
 
 
# 8장. 웹 어플리케이션을 위한 범용 JavaScript
 
## 8.1 브라우저와 코드 공유하기
* 모듈 공유
* ES2015 모듈
 
## 8.2 Webpack 소개
* Webpack의 마력 탐구
* Webpack 사용의 이점
* Webpack과 함께 ES2015 사용하기
 
## 8.3 크로스 플랫폼 개발의 기본
* 런타임 코드 분기
* 빌드 타임 코드 분기
* 모듈 교환
* 크로스 플랫폼 개발을 위한 디자인 패턴
 
## 8.4 리액트(React) 소개
* 첫 번째 React 컴포넌트
* JSX가 뭐지?!
* JSX 변환을 위한 Webpack 설정
* 브라우저에서 렌더링하기
* React Router 라이브러리
 
## 8.5 범용 JavaScript 앱 만들기
* 재사용 가능한 컴포넌트 만들기
* 서버 측 렌더링
* 범용 렌더링 및 라우팅
* 범용 데이터 조회
 
 
# 9장. 고급 비동기 레시피
 
## 9.1 비동기적으로 초기화되는 require 수행 모듈
* 전통적인 솔루션
* 미리 초기화된 큐
* 실전에서는 어떻게 사용되는가
 
## 9.2 비동기 배치(일괄 처리) 및 캐싱
* 캐싱 또는 일괄 처리가 없는 서버 구현
* 비동기 요청 일괄 처리
* 비동기 요청 캐싱
* 프라미스를 사용한 일괄처리와 캐싱
 
## 9.3 CPU 바운딩 작업 실행
* 부분 집합의 합 문제 해결
* setImmediate를 사용한 인터리빙
* 멀티 프로세스 사용

 
# 10장. 확장성과 구조적 패턴
 
## 10.1 어플리케이션 확장에 대한 소개
* Node.js 응용 프로그램 확장
* 확장성의 세 가지 차원
 
## 10.2 복제 및 로드 밸런싱
* 클러스터 모듈
* 상태 저장 통신 다루기
* 역방향 프록시를 사용하여 확장
* 서비스 레지스트리 사용
* 피어-투-피어 로드 밸런싱
 
## 10.3 복잡한 어플리케이션 분해
* 단일(Monolitic) 아키텍처
* 마이크로 서비스 아키텍처
* 마이크로 서비스 아키텍처의 통합 패턴
 
 
# 11장. 메시징과 통합 패턴
 
## 11.1 메시징 시스템의 기본 사항
* 단방향 및 요청/응답 턴
* 메시지 유형
* 비동기 메시징 및 큐
* 피어 투 피어 또는 브로커 기반 메시징
 
## 11.2 게시/구독 패턴
* 간단한 실시간 채팅 어플리케이션 만들기
* 메시지 브로커로 Redis 사용하기
* ØMQ를 사용한 피어 투 피어 게시/구독
* 영구 구독자
 
## 11.3 파이프 라인 및 작업 배포 패턴
* ØMQ 팬아웃/팬인 패턴
* AMQP의 파이프라인과 경쟁 소비자
 
## 11.4 요청(request)/응답(reply) 패턴
* 상관 관계 식별자
* 반송 주소 