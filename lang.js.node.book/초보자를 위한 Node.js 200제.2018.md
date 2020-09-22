## PART 1 입문 Nodejs 프로그램 걸음마 배우기
* 006 `${변수}` 백틱을 이용한 포맷팅
* 011 숫자인지 판단하기 isNaN(): is not a number: isNaN(foo)
* 014 문자열 개수 세기 length
* 015 해당 문자열 찾기 indexOf(): foo.indexOf(bar)
* 017 배열(array)에 값 넣기: foo.push(bar); foo.push(1,2,3)
* 021 typeof로 변수의 타입(형) 알아보기: typeof foo
* 023 증감연산자: +=, -=


## PART 2 초급 Nodejs 프로그램 기본기 연마하기
* 031 반복문 for: for(let foo = 0; foo < 3; foo++) {}
* 033 for문 끝내기 break: for() { ... break; }
* 034 자주 쓰는 반복문 for of: for(const n of ['foo', 'bar']) {}
* 035 forEach() 포 이치: [2,3,4].forEach(n => console.log(n));
* 036 반복문 while: while(foo < bar) {}
* 037 날짜 시간 생성하기 Date(): new Date(2020, 1, 2).toLocaleString()
* 038 날짜 시간 출력하기: toLocaleDateString(), toLocaleTimeString(), getFullYear(), (getMonth() + 1), getDate(), getHours(), getMinutes(), getSeconds()
* 039 yyyy-MM-dd 형식으로 날짜 출력하기
* 040 Timestamp(타임스탬프): unixtime: new Date().getTime()
* 042 예외처리 try catch final: try {} catch(e) {} finally {}
* 043 전역 객체(Global Object): process, console, buffer, require(), __filename, __dirname, module, exports, Timeout
    * process: env, argv, exit()
* 055 난수 생성(random): Math.floor(Math.random() * (10 * range))
* Math:반올림 round(number), 최대값 max(), 최소값 min(), 절대값 abs(), 거듭제곱 pow(), 제곱근 함수, 세제곱근 함수 sqrt(), cbrt(), 부호 함수 sign(), 로그함수 log(), log10(), log2(), log1p(), 바닥함수, 천장함수 floor(), ceil(), 버림함수 trunc(), 밑이 자연상수(e)인 지수함수 exp(), expm1(), 삼각함수 sin(), cos(), tan(), 역삼각함수 asin(), acos(), atan(), 쌍곡함수 sinh(), cosh(), tanh(), 역쌍곡함수 asinh(), acosh(), atanh()
* 070 특정 문자열 바꾸기 replace(): foo.replace(from, to);
* 071 문자열 나누기 split(): foo.split(delimiter)
* 072 문자열 추출하기 substring(): foo.substring(start, stop)
* 073 숫자로 바꾸기 Number()
* 074 정규 표현식(regexp) \ 이스케이프, 정규 표현식(regexp) 점, 정규 표현식(regexp) {0, 1} 중괄호, 정규 표현식(regexp) [], 정규 표현식 match()
* 079 정기적으로 실행하기 setInterval(fn, milsec)
* 080 몇 초 후에 실행하기 setTimeout(fn, milsec)
* 081 정기적으로 실행 취소하기 clearInterval(fn)
* 083 배열 뒤집기 reverse()
* 084 정렬하기 오름차순 sort()
* 085 정렬하기 여러 조건 sort(): foo.sort((prev, next) => { if(prev.col1 > next.col1) return 1; else if(prev.col1 < next.col1) return -1; else if(prev.col2 > next.col2) return 1; return 0; });
* 086 JSON 오브젝트 정렬: foo.sort((prev, next) => prev.col1 - next.col1);
* 087 배열에서 필요한 부분만 뽑기 slice(): [1,2,3,4].slice(start, stop)
* 089 배열 합치기 concat(): [1,2].concat([3,4])
* 090 배열 shift(), unshift(): foo.shift(); foo.unshift(bar);
* 091 배열 pop(): [1,2,3].pop();


## PART 3 중급 Nodejs 함수형 프로그램과 실전 예제
* 098 재귀함수, 피보나치 수열
* 101 클로저 closer
* 102 합성함수: func1(func1())
* 103 커링 curring: 화살표 개수보다 인수값이 적으면 함수를 반환: const foo = x => y => x + y; const bar = foo(1); bar(2);
* 106 프리디케이트 predicate
* 107 프리디케이트로 정렬 sort(predicate)
* 108 filter() 함수 사용하기: [1,2,3].filter(n => n > 1);
* 110 map() 함수 사용하기: [1,2,3].map(n => n * 10);
* 112 reduce() 함수 사용하기: [1,2,3].reduce((a,b) => (a + b)); reduce(prev, next, index, array)
* 117 프로미스 promise: const pm = new Promise(resolve => resolve(1)).then(res => res);
* 118 Promiseall()을 이용해 후처리하기: Promise.all([pm1, pm2]).then(res => res);
* 119 exports: exports.func = func; exports.func = () => {}
* 120 require: const foo = require(path);


## PART 4 활용 Nodejs 라이브러리를 활용할 실전 응용
* 123 파일로 출력하기 fswrite(): fs.writeFile(path, contents);
* 124 동기로 파일 열기 fsreadFileSync(): fs.readFileSync(path).toString();
* 125 비동기로 파일 열기 fsreadfile(): fs.readFile(path, (err, data) => { if(err) throw err; console.log(data.toString()); });
* 126 파일 내용 수정하기: fs.readFile(path, (err, data) => { fs.writeFile(path, outs); });
* 127 파일에 내용 추가하기 fsappendFile(): [1,2,3].forEach(n => fs.appendFile(path, n));
* 128 디렉토리 만들기 fsmkdirSync(): fs.mkdirSync(path);
* 129 파일 리스트 출력하기: fs.readdirSync(path);
* 130 list를 json 형식으로 파일에 저장하기, JSONstringify(): fs.writeFile(path, JSON.stringify(foo));
* 131 파일을 json 형식으로 불러오기, JSONparse(): fs.readFile(path, (err, data) => { console.log(JSON.parse(data.toString())) });
* 132 파일 이름 바꾸기: fs.rename(from, to, (err) => {})
* 133 http 모듈: const server = reqquire('http').createServer(); server.listen(port, () => {}); server.close();
* 134 http 모듈 - event: server.on(event, () => {});
    * request, connection, close, clientError, checkContinue,
* 135 http 모듈 - response 객체: require('http').createServer((req, res) => { res.writeHead(); res.end(); }).listen(port), () => {});
* 137 http 모듈 - response 객체, fs 모듈 활용②: ... fs.readFile(path, (err, data) => { res.writeHead(); res.end(data) }); ...
* 138 http 모듈 - request 객체, url 속성 활용
* 139 http 모듈 - request 객체, method 속성 GET
* 140 http 모듈 - request 객체, method 속성 POST
* 141 쿠키(Cookie) 생성: ... res.writeHead(200, { ... 'Set-Cookie': '[foo=bar]', }); ...
* 142 쿠키(Cookie) 추출: ... req.headers.cookie.split(';').map(n => {})
* 144 프로젝트 초기화 하기-npm init, npm install, npm uninstall
* 148 request로 구글 크롤링하기
* 149 request로 파라미터 추가해 호출하기: require('request')({ url: url, method: 'GET', qs: { q: foo }}, (err, res, body) => console.log(body));
* 150 한글 깨지는 문제 해결하기: encoding: null, iconv.decode(body, 'utf-8')
* 152 cheerio 이용해서 필요한 부분 추출하기: jquery 문법
* 153 request 실행 결과 파일로 저장하기: fs.appendFile(path, outs);
* 154 ejs 모듈, pug 모듈: 템플릿(웹 페이지)
* 159 winston 모듈(로그 파일): const log = new (requre('winston').Logger) ({ transports: [], exceptionHandlers: [], }); log.info(foo);
* 160 express 모듈 ① - overview
    * const express = require('express'); const app = express();
        * app.get('/', (req, res) => { res.send(foo) });
        * app.listen(port, () => {});
* 161 express 모듈 ② - response
    * res.send(foo); res.status(404).send(foo); 
    * res.download(), res.end(), res.json(), res.jsonp(), res.redirect(), res.render(), res.sendFile(), res.sendStatus()
* 162 express 모듈 ③ - request
    * app.use((req, res) => { res... });
        * req.header(), req.headers, req.query.*, req.body, req.params
* 163 express 모듈 ④ - 미들웨어: app.use((req, res, next) => { ... next(); });
* 164 express 모듈 ⑤ - static 미들웨어: app.use(express.static(path)); app.use((req, res) => { ... });
* 165 express 모듈 ⑥ - body parser 미들웨어: POST 데이터 추출: const bp = require('body-parser'); app.use(bp.urlencoded({})); app.use(dp.json());
* 166 express 모듈 ⑦ - router 미들웨어: app.get('/foo/:bar', (req, res) => { console.log(req.params.bar) });
* 167 express 모듈 ⑧ - morgan 미들웨어
* 168 express 모듈 ⑨ - cookie parser 미들웨어
* 169 express 모듈 ⑩ - connect-multiparty 미들웨어
* 170 express 모듈 ⑪ - express-session 미들웨어
* 171 node-schedule 모듈 ①
* 173 Nodemailer 모듈 ① - 메일 보내기(TEXT)
* 174 Nodemailer 모듈 ② - 메일 보내기(HTML)
* 175 Nodemailer 모듈 ③ - 메일 보내기(첨부파일)
* 176 MySQL ① - 설치
* 177 MySQL ② - 데이터베이스 생성
* 178 MySQL ③ - 테이블 생성
* 179 MySQL ④ - 데이터 삽입
* 180 MySQL ⑤ - 데이터 조회&기본적인 WHERE 절
* 181 MySQL ⑥ - 데이터 수정
* 182 MySQL ⑦ - 데이터 삭제
* 183 socketio ① - 클라이언트
* 184 socketio ② - 서버
* 185 socketio ③ - 이벤트


## PART 5 실무 Nodejs로 간단한 프로그램 만들기
* 186 크롤러를 활용한 뉴스 속보 이메일 발송 시스템 ①
* 190 MySQL 모듈을 활용한 게시판 구현 ① - 모듈 소개
* 198 텔레그램 봇 만들기
* 199 텔레그램 봇 라이브러리 설치하기
* 200 텔레그램 봇 애플리케이션 띄우기