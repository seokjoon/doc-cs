* php artisan about
	* 환경 표시

* php artisan cache:clear
	* 캐시 삭제 
    
* php artisan config:cache
    * 설정내역 로딩 최적화
* php artisan config:clear

* php artisan config:show cache, database, ...
    
* php artisan db:seed
    * seeder 실행(composer dump-autoload 이후)
    * php artisan db:seed --class=UsersTableSeeder
    
* php artisan event:generate
   	* 이벤트 채널과 리스너 스캐폴드 생성
    
* php artisan down, php artisan up
    * 앱 다운/업
    * php artisan down --message="Upgrading Database" --retry=60
    * php artisan down --allow=127.0.0.1 --allow=192.168.0.0/16
    
* php artisan key:generate
	* 앱 키 설정
    
* php artisan make:auth
	* 인증 라우트/뷰 스캐폴딩(라라벨 내장 사용자 인증 생성)
    
* php artisan make:channel FooChannel
	* 채널 클래스 생성
    
* php artisan make:class
	* php artisan make:enum
	* php artisan make:interface
	* php artisan make:trait

* php artisan make:command Foo
    * 커맨드 생성
    
* php artisan make:controller API/FooController --api
	* api 리소스 컨트롤러
* php artisan make:controller FooController --resource
	* 컨트롤러 리소스
* php artisan make:controller FooController --resource --model=Foo
	* 리소스 모델 지정
    
* php artisan make:event ArticleCreated
	* 이벤트 클래스
	
* php artisan make:factory FooFactory --model=Foo
	* DB 시딩 팩토리
	
* php artisan make:job ProcessFoo
	* job 클래스 생성
	
* php artisan make:listener ArticleEventListener --event=ArticleCreated
	* 이벤트 리스너
    
* php artisan make:mail Foo
	* Mailables 생성 
* php artisan make:mail Foo --markdown=emails.foo
	* Mailables 생성(마크다운) 
    
* php artisan make:middleware Foo
	* 미들웨어 생성
	
* php artisan make:model Foo
	* 모델 생성 
	* php artisan make:model Foo --migration
	
* php artisan make:notification Foo
	* 알림 생성
* php artisan make:notification Foo --markdown=mail.foo
	* 메일(마크다운) 알림 생성
	
* php artisan make:observer FooObserver --model=Foo
	* 옵저버 생성

* php artisan make:policy FooPolicy
	* policy 클래스 생성
* php artisan make:policy FooPolicy --model=Foo
	* policy 클래스(CRUD 포함) 생성

* php artisan make:provider FooServiceProvider
	* 서비스 프로바이더 작성
	* config/app.php 편집

* php artisan make:request StoreFooPost
	* form request 생성
	
* php artisan make:resource User
	* 리소스 클래스 생성
	* 리소스 컬렉션 생성
		* ~~php artisan make:resource Users --collection~~
		* ~~php artisan make:resource UserCollection~~
	
* php artisan make:rule Foo
	* 사용자 정의 유효성 검사 규칙
	
* php artisan make:seeder UsersTableSeeder
	* seeder 생성
	* php artisan make:seeder Foo/FoosTableSeeder
	
* php artisan make:test UserTest
* php artisan make:test UserTest --unit
	* 테스트 생성
	
* php artisan migrate
    * 마이그레이션
   	* php artisan migrate --force
	* php artisan migrate --path=database/migrations/foo
* php artisan make:migration create_users_table
	* 마이그레이션 파일 생성
	* php artisan make:migration create_users_table --create=users
	* php artisan make:migration add_votes_to_users_table --table=users
	* php artisan make:migration --path=database/migrations/foo create_foos_table --create=foos
* php artisan migrate:fresh
	* 모든 테이블&마이그레이션 drop
	* php artisan migrate:fresh --seed
* php artisan migrate:refresh
	* 롤백&마이그레이트
	* php artisan migrate:refresh --seed
	* php artisan migrate:refresh --step=5
* php artisan migrate:rollback
    * 롤백
   	* php artisan migrate:rollback --step=5
* php artisan migrate:reset
    * 리셋
	
* php artisan notifications:table && php artisan migrate
	* 알림(데이터베이스) 
    
* php artisan passport:install
	* 액세스 토큰 생성 위한 암호화 키 생성
    
* php artisan queue:failed-table && php artisan migrate
	* 실패 job 처리 테이블
* php artisan queue:failed
    * 실패 job 보기(DB 테이블)
* php artisan queue:retry 5
	* 실패 job 재시작
	* php artisan queue:retry all
		* 실패 job 모두 재시작
* php artisan queue:forget 5
	* 실패 job 삭제
	* php artisan queue:flush
		* 실패 job 모두 삭제
    
* php artisan queue:restart
	* 큐 워커 코드 변경 적용
    
* php artisan queue:table && php artisan migrate
	* 드라이버 준비(DB)

* php artisan queue:batches-table && php artisan migrate
	* job 일괄처리
	
* 큐 worker 실행: php artisan queue:work
	* 단일 job 지정: php artisan queue:work --once
	* 커넥션 지정: php artisan queue:work redis
	* 큐 지정: php artisan queue:work redis --queue=emails
    
* php artisan queue:work --queue=high,default
	* job 큐 우선 순위 부여
	
* php artisan queue:work --sleep=3
	* worker 잠자기 시간
	
* php artisan queue:work --timeout=30
	* 최대 수행 시간(job 클래스 내 $timeout 값이 우선)
* php artisan queue:work --tries=3
	* 최대 재시도 횟수(job 클래스 내 $tries 값이 우선)
	
* php artisan route:cache
	* 라우트 로딩 최적화
	* php artisan route:clear
	
* php artisan route:list
	* 라우트 목록 확인

* php artisan schedule:run
	* cron 등록: * * * * * php /path-to-your-project/artisan schedule:run >> /dev/null 2>&1
	
* php artisan storage:link
	* 심볼릭 링크
	
* php artisan tinker

* php artisan make:transformer "App\Foo"
	* Transformer 생성
	
* php artisan view:clear
	* 블레이드 뷰 캐시 제거
	
* php artisan vendor:publish --provider="Foo\Bar\ServiceProvider"
	* 컴포넌트 리소스 가져오기(커스텀)
	
* php artisan vendor:publish --tag=config
	* 패키지 asset들과 resource 파일들을 그룹단위로 퍼블리싱: 
* php artisan vendor:publish --tag=public --force
	* 패키지 asset들을 지정된 퍼블리싱 위치로 복사
	
* php artisan vendor:publish --tag=laravel-notifications
	* 메일 알림 템플릿 커스텀 설정
	
* php artisan vendor:publish --tag=laravel-pagination
	* 페이지네이션 뷰 커스텀(복사)
	
