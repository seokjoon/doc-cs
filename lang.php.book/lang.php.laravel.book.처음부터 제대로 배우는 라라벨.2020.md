# 2 라라벨 개발 환경 구성하기
## 2.4 라라벨 프로젝트 생성하기 
* composer global require 'laravel/installer'
    * vi .bashrc
        * export PATH=${PATH}:$(composer global config bin-dir --absolute --quiet)
    * laravel new foo 
    * laravel new bar --jet


# 3 라우팅 및 컨트롤러
## 3.3 라우트 그룹
* failback
    * Route::fallback(function() {});
## 3.4 서명된 라우트
* Route::get('invits/{invit}{group}', InvitsController::class)->name('invits');
    * URL::signedRoute('invits', ['invit' => 1234, 'group' => 5678])->middleware('signed');
    * URL::temporarySignedRoute('invits', now()->addHours(4), ['invit' => 1234, 'group' => 5678])->middleware('signed');
## 3.6 컨트롤러
* Route::apiResource(), Route::apiResources([]);
## 3.7 라우트 모델 바인딩
## 3.8 라우트 캐싱
## 3.9 폼 메서드 스푸핑
* @method('DELETE')
## 3.10 CSRF 보호
* @csrf
## 3.11 리다이렉트
* redirect(), ->to(), ->route(), ->back(), ->refresh(), ->away(), ->with()
## 3.12 요청 중단하기
* abort(), abort_if(), abort_unless(),
## 3.13 커스텀 응답
* resonse(), ->make(), ->json(), ->jsonp(), ->download(), ->streamDownload(), ->file(),
## 3.14 CORS 처리
 

# 4 블레이드 템플릿
## 4.4 뷰 컴포저와 서비스 주입
## 4.5 커스텀 블레이드 지시어


# 5 데이터베이스와 엘로퀀트
## 5.4
* 트랜잭션
    * DB::transaction(function() use() {})
    * DB::beginTransaction(); DB::commit(); DB::rollback()
## 5.5 엘로퀀트 소개
* 로컬 스코프
    * public function scopeFoo($query) { return $query->where() }
* 글로벌 스코프
* 접근자
    * public function getFooAttribute($val) {}
* 변경자
    * public function setFooAttribute($val) {}
* 커스텀 형변환
    * class Foo implements CastsAttribute {}
    * protected $casts = [ 'bar' => Foo::class, ];
* 컬렉션
    * $foo = collect([1,2,3])->filter(function($l) {})->reject(function($m) {})->map(function($n) {})->sum();
        * max(), whereIn(), flattern(), flip(), ...
            * https://laravel.kr/docs/8.x/collections
## 5.6 엘로퀀트 이벤트
* created, creating, deleted, deleting, retrieved, updated, updating, 
* saved, saving: create + update
* restored, restoring: 소프트 삭제 복원
 

# 6 프런트엔드 컴포넌트
## 6.2 프런트엔드 프리셋
## 6.3 페이지네이션
## 6.4 메시지 백
## 6.5 문자열 처리를 위한 Str 클래스, 복수 표기, 다국어 처리


# 7 사용자 데이터의 조회 및 처리
## 7.1 Request 객체를 사용한 데이터 조회
* $request->has(), $request->json(), $request->input('foo.bar')
## 7.3 파일 업로드
## 7.4 유효성 검증
## 7.5 폼 요청 객체
 

# 8 아티즌과 팅커
## 8.2 기본적인 사용법
* clear-compiled, down/up, optimize
* --no-interaction, --env
## 8.3 아티즌 명령어 생성 방법
* 인자/옵션: argument(), arguments(), option(), options()
* 프롬프트: ask(), secret(), confirm(), anticipate(), choice()
* 화면출력
    * info(), comment(), question(), erro(), line()
    * table(), progressStart(), progressAdvance(), progressFinish()
## 8.4 일반 코드에서 아티즌 명령어의 호출
* Artisan::call('foo:bar', []), Artisan::callSilent('foo:bar', [])


# 9 사용자 인증과 인가

## 9.1 User 모델과 마이그레이션

## 9.2 auth() 글로벌 헬퍼와 Auth 퍼사드 사용하기

## 9.3 인증 컨트롤러

## 9.4 Auth::routes()

## 9.5 인증 스캐폴드

## 9.6 remember me로 사용자 로그인 유지하기

## 9.7 비밀번호 재확인

## 9.8 수동으로 인증하기

## 9.9 수동으로 로그아웃하기

## 9.10 인증 미들웨어 

## 9.11 이메일 검증

## 9.12 블레이드 인증 지시어

## 9.13 가드

## 9.14 인증 이벤트

## 9.15 인가

## 9.16 테스트

## 9.17 마치며

 

# 10 요청, 응답, 미들웨어

## 10.1 라라벨 요청 생명주기

## 10.2 요청 객체

## 10.3 응답 객체

## 10.4 라라벨과 미들웨어

## 10.5 신뢰할 수 있는 프록시

## 10.6 테스트

## 10.7 마치며

 

# 11 컨테이너

## 11.1 의존성 주입 훑어보기

## 11.2 의존성 주입과 라라벨

## 11.3 app() 글로벌 헬퍼

## 11.4 컨테이너는 어떻게 의존 객체를 연결하는가?

## 11.5 컨테이너에 클래스 바인딩하기

## 11.6 라라벨 프레임워크의 주요 클래스의 생성자 주입

## 11.7 메서드 주입

## 11.8 퍼사드와 컨테이너

## 11.9 컨테이너와 서비스 프로바이더

## 11.10 테스트

## 11.11 마치며

 

# 12 테스트

## 12.1 테스트 기초

## 12.2 테스트 이름 짓기

## 12.3 테스트 환경

## 12.4 테스트 트레이트

## 12.5 간단한 유닛 테스트

## 12.6 애플리케이션 테스트: 동작 원리

## 12.7 HTTP 테스트

## 12.8 데이터베이스 테스트

## 12.9 라라벨 내부 시스템 테스트하기

## 12.10 목킹

## 12.11 아티즌 명령어 테스트하기

## 12.12 브라우저 테스트

## 12.13 마치며

 

# 13 API 작성하기

## 13.1 RESTful JSON API 기초

## 13.2 컨트롤러 구성과 JSON 응답 

## 13.3 헤더 읽기 및 전송

## 13.4 엘로퀀트 페이지네이션

## 13.5 정렬과 필터링

## 13.6 API 리소스

## 13.7 라라벨 패스포트를 이용한 API 인증

## 13.8 API 토큰 인증

## 13.9 라라벨 생텀을 이용한 API 인증

## 13.10 404 응답 변경하기

## 13.11 테스트

## 13.12 마치며

 

# 14 스토리지와 검색

## 14.1 로컬과 클라우드 파일 관리자

## 14.2 기본적인 파일 업로드와 조작

## 14.3 단순 파일 다운로드

## 14.4 세션

## 14.5 캐시

## 14.6 쿠키

## 14.7 로그

## 14.8 라라벨 스카우트를 이용한 풀 텍스트 검색

## 14.9 테스트

## 14.10 마치며

 

# 15 메일과 알림

## 15.1 메일

## 15.2 알림

## 15.3 테스트

## 15.4 마치며

 

# 16 큐, 잡, 이벤트, 브로드캐스팅, 스케줄러

## 16.1 큐

## 16.2 라라벨 호라이즌

## 16.3 이벤트

## 16.4 웹소켓과 라라벨 에코를 이용한 이벤트 브로드캐스팅

## 16.5 스케줄러

## 16.6 테스트

## 16.7 마치며

 

# 17 헬퍼와 컬렉션

## 17.1 헬퍼

## 17.2 컬렉션

## 17.3 레이지 컬렉션

## 17.4 마치며


# 18 라라벨 생태계

## 18.1 이 책에서 다룬 도구

## 18.2 이 책에서 다루지 않은 도구

## 18.3 기타 자료