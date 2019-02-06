* https://github.com/appkr/l5code

# 목차
```
# 라라벨 입문
01 라라벨 설치
02 전역 환경 설정
03 라우팅 
04 뷰와 데이터 바인딩
05 블레이드
06 데이터베이스와 모델
07 데이터베이스 마이그레이션
08 컨트롤러
10 엘로퀀트 ORM
11 데이터베이스 시딩
12 즉시 로드와 페이징
13 입력값 유효성 검사
14 이벤트 시스템
15 예외 처리와 디버깅
17 컴포저

# 실전 프로젝트 1 - 마크다운 뷰어
18 모델
19 컨트롤러와 도우미 함수
20 다듬질
21 엘릭서와 프런트엔드

# 실전 프로젝트 2 - 포럼
22 계획과 준비
23 사용자 인증 재구성
24 소셜 로그인
25 아티클 기능 구현
26 태그 기능 구현
27 파일 첨부 기능 구현
28 댓글 기능 구현
29 다듬질 1
30 다듬질 2

# 실전 프로젝트 3 - RESTful API
31 기본기 익히기
32 구조 설계
33 클라이언트 인증
34 데이터 트랜스폼
35 다듬질 1
36 다듬질 2

# 코드 배포
37 서버 준비
38 코드 배포
```


# 라라벨 입문

## 일러두기
* 복제: git clone https://github.com/appkr/l5code.git l5code
* 오토로드 레지스트리 업데이트: composer dump-autoload
* 의존성 설치: composer install
* 환경 설정: cp .env.example .env
* 암호화 키: php artisan key:generate
* 디렉토리 퍼미션: chown, chmod -R 775 storage bootstrap/cache
* db 마이스레이션 및 시딩: php artisan migrate --seed --force

## 01 라라벨 설치
* composer create-project laravel/laravel foo --prefer-dist --verbose
* git init, git add ., git commit -m 'foo', git tag bar

## 02 전역 환경 설정
* edit .gitignore
* edit .env
* edit config/database.php

## 03 라우팅
* Route::get('/{foo}', function($foo) { return $foo; })->where('foo', '[0-9a-zA-Z]{3}');
* Route::get('/{foo?}', function($foo = 'bar') { return $foo; });
* Route::get('/', ['as' => 'home', function() { return 'foo'; }]);
* Route::get('home', function() { return redirect(route('home')); });
* 라우트 목록 확인: php artisan route:list

## 04 뷰와 데이터 바인딩
* Route::get('error', function() { return view('errors.503'); });
* Route::get('/', function() { return view('foo')->with('bar', 'BAR'); });
* Route::get('/', function() { return view('foo')->with(['bar' => 'BAR', 't1' => 'T1']); });
* Route::get('/', function() { return view('foo', ['bar' => 'BAR', 't1' => 'T1']); });

## 05 블레이드
* {{ $foo or $bar }}, {{-- comment --}}
* {{ @if() @elseif() @else @endif }}
* {{ @foreach() @endforeach }}
* {{ @forelse() @empty @endforelse }}: if 와 foreach 의 결합
* 템플릿 상속
    * 마스터 레이아웃: @yield('content')
    * 자식 뷰: @extends('layouts.master') @section('content') @endsection
    * @extends('layouts.master') @section('style') @endsection @section('content') @endsection @section('script') @endsection
* 조각 뷰 삽입
    * @include(): 마스터/자식의 섹션 안/밖 어디서든 가능 
    * @extends() @section() @include('partials.footer') @endsection
* 섹션의 상속: @parent 
* 블레이드는 html 뿐 아니라 xml, css, javascript, php 등 어떤 형식이든 활용 가능

## 06 데이터베이스와 모델
* raw query
	* DB::insert('insert into tests(foo, bar) values(?,?)', ['FOO','BAR']); 
	* DB::select('select * from tests'); 
	* DB::selectOne('select * from tests where id = ?', [1]); 
* query builder		
	* DB::table('tests')->delete(1); 
	* DB::table('tests')->get(); 
	* DB::table('tests')->find(1); 
	* DB::table('tests')->first(); 
	* DB::table('tests')->insert(['nameCol' => 'valueCol']);
	* DB::table('tests')->limit(1)->get();
	* DB::table('tests')->orderBy('name', 'desc')->get();
	* DB::table('tests')->pluck('name', 'id');
	* DB::table('tests')->update(['nameCol' => 'valueCol']);
	* DB::table('tests')->where('id', '=', 1)->get(); 
	* DB::table('tests')->where('id', 1)->get(); 
	* DB::table('tests')->where(function($query) { $query->where('id', 1); })->get(); 
	* DB::table('tests')->whereId(1)->get(); 
	* DB::table('test')->...
		* count(), distinct(), groupBy(), having(), join(), union(), whereNull(), whereNotNull(), 
		* select(DB::raw('count(*) as cnt'));
* 엘로퀀트 ORM
	* 모델 생성: php artisan make:model Foo
		* 테이블 이름은 복수, 모델 이름은 단수
		* 테이블과 모델 이름이 관례를 따르지 않을 경우: $table = 'tests';
	* 모델 질의: App\Foo::get();
	* 모델 저장(A): $foo = new App\Foo; $foo->bar = 'BAR'; $foo->save();
	* 모델 저장(B): App\User::create(['email' => 'a@b.c', 'password' => bcrypt('foo')]);
	* MassAssignmentException: $fillable = []; $guarded = [];
	* 조회시 속성 숨김: $hidden = [];
	* updated_at, created_at 비사용: $timestamps = false;

## 07 데이터베이스 마이그레이션
* 참고: 외래키 오류 방지: set foreign_key_checks=0; ...; set foreign_key_checks=1;
* 마이그레이션 생성(테이블 생성): php artisan make:migration create_tests_table --create=tests
* 마이그레이션 생성(테이블 변경): php artisan make:migration add_foo_to_tests_table --table=tests
* 마이그레이션 실행: php artisan migrate
* 마이그레이션 롤백(직전): php artisan migrate:rollback
* 마이그레이션 롤백(모든): php artisan migrate:reset
* 마이그레이션 초기화 후 재실행: php artisan migrate:refresh

## 08 컨트롤러
* 컨트롤러 생성: php artisan make:controller FooController
	* Route::get('/', 'FooController@bar');
* 컨트롤러 생성(restful): php artisan make:controller BarsController --resource
	* Route::resource('bars', 'BarsController');
* 추가 restful 라우트: Route::any(); Route::delete(); Route::match(); Route::options(); Route::patch(); Route::post(); Route::put();
* csrf 보호 임시 제외: 미들웨어 VerifyCsrfToken의 $except = [];
* HTTP 메소드 오버라이드: body에서 _method 파라미터 혹은 헤더에서 X-HTTP-Method-Override

## 09 사용자 인증
* 라라벨 내장 사용자 인증 생성: php artisan make:auth
* 사용자 생성: App\User::create(['email' => 'a@b.c', 'password' => bcrypt('PW')]);
* 사용자 로그인: auth()->attempt(['email'=>'a@b.c', 'password' => 'PW']);
	* 혹은 auth()->login($user);
* 사용자 여부 확인: auth()->check();
	* auth 미들웨어: Route::get('protected', ['middleware' => 'auth', function() { ... }]);
* 게스트 여부 확인: auth()->guest();
* 로그아웃: auth()->logout();

## 10 엘로퀀트 ORM
* 일대다 관계
	* 마이그레이션(articles)
		* $table->foreign('user_id')->references('id')->on('users')->onUpdate('cascade')->onDelete('cascade');
		* 테이블이름_열이름_foreign 관계 생성됨
		* 삭제: $table->dropForeign('articles_user_id_foreign');
	* 연결(Article::user()): $this->belongsTo(User::class); $this->belongsTo(User::class, 'custom_col');
	* 연결(User::articles()): $this->hasMany(Article::class); $this->hasMany(Article::class, 'custom_col');
	* 레코드 생성(외래키 자동 삽입): App\User::find(1)->articles()->create([...]);
	* 조회
		* App\User::find(1)->articles()->get();
		* App\Article::find(1)->user()->first();
* 다대다 관계: 사례 테이블: articles, article_tag, tags
	* 피벗 테이블 이름: 두 테이블 이름을 단수로 바꾸고 알파벳 순으로 밑줄 연결 
	* 마이그레이션(article_tag)
		* $this->foreign('article_id')->references('id')->on('articles')->onDelete('cascade');
		* $this->foreign('tag_id')->references('id')->on('tags')->onDelete('cascade');
	* 연결(Tag::articles()): $this->belongsToMany(Article::class); $this->belongsToMany(Article::class, 'custom_table', 'custom_col');
	* 연결(Article::tags()): $this->belongsToMany(Tag::class); $this->belongsToMany(Tag::class, 'custom_table', 'custom_col');
	* 레코드 생성(외래키 자동 삽입): App\Article::find(1)->tags()->sync([1,2,...]);
	* 조회
		* App\Article::find(1)->tags()->pluck('name', 'id');
		* App\Tag::find(1)->articles();
* 일대일 관계
* 다형적 관계
* 다대다 다형관계

## 11 데이터베이스 시딩
* 시더 생성: php artisan make:seeder UsersTableSeeder
	* UsersTableSeeder::run(): App\User::create([...]);
* 시딩
	* php artisan db:seed
	* php artisan db:seed --class=UsersTableSeeder
* 시딩(마이그레이션 포함): php artisan migrate:refresh --seed
* 모델 팩토리
	* UsersTableSeeder::run(): factory(App\User::class, 5)->create();
	* UserFactory.php: $factory->define(App\User::class, function(Faker $faker) { return [...]; });
* 마스터 시더
	* DatabaseSeeder::run(): App\User::truncate(); $this->call(UsersTableSeeder::class);

## 12 즉시 로드와 페이징
* 즉시 로드(N+1 문제 해결): \App\Article::get(); 을 \App\Article::with('user')->get(); 으로 변경
* 지연 로드: $articles = \App\Article::get(); ...; $articles->load('user'); 
* 페이징
	* \App\Article::latest()->paginate(3);
	* @if($articles->count()) {!! $articles->render() !!}

## 13 입력값 유효성 검사
* 전송 폼: ArticlesController::create(): return view('articles.create');
	* {{ route('articles.store') }}
	* {!! csrf_field() !!}
		* {!! method_field($method) !!}
	* {{ old('title') }}
		* {{ old(') }}
	* ```{!! $errors->first('title', '<span class="form-error">:message</span>') !!}```
	* {{ $errors->has('title') ? 'has-error' : '' }}
* 컨트롤러 자체 처리 이용: ArticlesController::store()
	* $rules = [ 'title' => ['required'], 'content' => ['required', 'min:10'], ];
	* $validator = \Validator::make($request->all(), $rules);
	* if($validator->fails()) { return back()->withErrors($validator)->withInput(); }
	* $article = \App\User::find(1)->articles()->create($request->all());
	* if(!($article)) { return back()->with('flash_message', 'error message')->withInput(); }
	* return redirect(route('articles.index'))->with('flash_message', 'save message');
* 플래시 메시지: @if(session()->has('flash_message')) {{ sessions('flash_message') }} @endif
* 오류 메시지 사용자화: $validator = \Validator::make($request->all(), $rules, $message);
* 트레이트 메소드 이용: ArticlesController::store()
	* $this->validate($request, $rules, $message);
* 폼 리퀘스트 클래스 이용
	* php artisan make:request ArticleRequest
	* ArticlesRequest::authorise(); ArticlesRequest::rules(); ArticlesRequest::messages(); ArticlesRequest::attribute();
	* ArticlesController::store(ArticleRequest $request) {}

## 14 이벤트 시스템
* 수동	
	* 이벤트 클래스: php artisan make:event ArticleCreated
	* 이벤트 리스너: php artisan make:listener ArticleEventListener --event=ArticleCreated
		* ArticlesEventListener::handle(ArticleCreated $event) {}
	* 이벤트 레지스트리: EventServiceProvider::boot();
		* \Event::listen(ArticleCreated::class, ArticlesEventListener::class);
	* 이벤트 발생: event(new ArticleCreated($article));
* 스캐폴드 이용
	* 이벤트 레지스트리: EventServiceProvider::$listen = [ ArticlesEvent::class => [ ArticlesEventListener::class, ], ];
	* 이벤트 채널과 리스너 스캐폴드 생성: php artisan event:generate
		* 이벤트 클래스: ArticlesEvent(\App\Article $articles, $action='created');
		* 이벤트 리스너: ArticlesEventListener::handle(ArticlesEvent $event) { if($event->action === 'created') {} }; 
	* 이벤트 발생(컨트롤러): event(new ArticlesEvent($article));
* 내장 이벤트 채널: 레지스트리에 채널과 리스너 등록 => php artisan event:generate => 리스너에 이벤트 처리 로직 구현

## 15 예외 처리와 디버깅
* Handler::report(); Handler::render(); Handler::$dontReport;
* \App\Article::findOrFail($id);
* 예외 던지기: abort(int $code, string $message = ''); abort_if(bool $boolean, int $code, string $message='''); abort_unless();
	* php: throw 예외클래스('message');
* 중단(덤프): dd($value);
* dump($value);
* 질의 디버깅
	* DB::listen(function($query) { dump($query->sql); });
	* 컬렉션 질의일 경우 toSql(): App\Foo::where()->toSql();
* 로그: storage/logs/laravel.log
* 라라벨 디버그 바: github.com/barryvdh/laravel-debugbar

## 16 이메일 보내기
* config/mail.php, .env
* Mail::send('emails.articles.created', compact('article'), function($message) use($article) { $message->...(); });
	* Mail::send(뷰, 데이터, 메일 구성);
		* $message->to(string $address, string $name = null); $message->to(array $address, string $name = null);
		* $message->from(string $address, string $name = null);
		* $message->cc(string $address, string $name = null); 필요시 반복
		* $message->bcc(string $address, string $name = null); 필요시 반복
		* $message->attach(string $file, array $options = [ 'as' => 'foo', 'mine' => 'bar' ]);
* 메일 본문 내 이미지: {{ $message->embed(storage_path('foo.jpg')) }}

## 17 컴포저
* composer require 벤더/패키지
* composer require 벤더/패키지 --dev
	* composer install --no-dev
* 일반(라라벨 전용이 아닌) 컴포넌트: 생성자 파라미터에 타입 힌트 있으면 의존성 자동 주입: app(Foo::class)->bar($bar);
* 라라벨 전용 컴포넌트
	* config/app.php
		* 'providers' => [ Foo\Bar\ServiceProvider::class, ];
	* 혹은 AppServiceProvider::register() { $this->app->register(\Fpp\Bar\ServiceProvider::class); }
	* 컴포넌트 리소스 가져오기(커스텀): 필요시: php artisan vendor:publish --provider="Foo\Bar\ServiceProvider"
* composer install: 프로젝트 의존 컴포넌트 설치
* composer update: 설치된 컴포넌트 버전 업그레이드
* 라라벨 디버그 바: composer require "barryvdh/laravel-debugbar"
	* ServiceProvider::class



# 실전 프로젝트 1 - 마크다운 뷰어

## 18 모델

## 19 컨트롤러와 도우미 함수
* 사용자 정의 헬퍼: composer.json 파일 autoload 의 files 배열에 경로 추가
	* composer dump-autoload --optimize

## 20 다듬질
* 캐시
	* .env 파일 설정: CACHE_DRIVER: file, array, memcached, redis, apc 등
	* $content = \Cache::remember('docs.index', 120, function() {});
		* \Cache::remember(캐시 키, 유효 기간(분), 클로저)
	* php artisan cache:clear
* 이미지 라우팅: Route::get('docs/images/{image}', 'DocsController@image');
	* 인터벤션 이미지 컴포넌트(웹 서버 루트 외부 이미지를 컨트롤러에서 반환)
		* composer require "intervention/image"
			* ImageServiceProvider::class, Image::class
		* \Image::make();
		* response($image->encode('png'), 200, ['Content-Type' => 'image/png']);
* 클라이언트 캐싱: Etag(문자열) 또는 If-Modified-Since(날짜 값): HTTP 헤더
	* $etag = md5($file . (File::lastModified($path, $dir)));
	* $etagReq = \Request::getEtags();
	* if(isset($etagReq[0])) { if($etagReq[0] === $etag) { return response('', 304); } }
	* 캐시 히트가 아닐 경우: 응답에 Cache-Control 과 Etag 값 추가

## 21 엘릭서와 프런트엔드



# 실전 프로젝트 2 - 포럼

## 22 계획과 준비
* 전역 설정값 만들기
	* config/foo.php 편집: return [ 'key' => 'value' ];
	* config('foo.key');
* 플래시 메시지 컴포넌트: composer require "laracasts/flash"
	* FlashServiceProvider::class, Flash::class
	* 컨트롤러: flash($msg); flash()->success($msg); flash()->warning($msg); flash()->danger($msg);
	* 뷰(블레이드): @include('flash::message')
	
## 23 사용자 인증 재구성
* 커스텀
	* 가입
		* Route::get(): auth/register, users.create, UsersController@create
		* Route::post(): auth/register, users.store, UsersController@store
		* Route::get(): auth/confirm/{code}, users.confirm, UsersController@confirm
	* 인증
		* Route::get(): auth/login, sessions.create, SessionsController@create
		* Route::post(): auth/login, sessions.store, SessionsController@store
		* Route::get(): auth/logout, sessions.destroy, SessionsController@destroy
	* 비밀번호 초기화
		* Route::get(): auth/remind, remind.create, PasswordsController@getRemind
		* Route::post(): auth/remind, remind.store, PasswordsController@postRemind
		* Route::get(): auth/reset/{token}, reset.create, PasswordsController@getReset
		* Route::post(): auth/reset, reset.store, PasswordsController@postReset
* 모델 컬럼 타입 (자동)캐스팅: protected $casts = [ 'foo' => 'bar' ];
* 컨트롤러 생성자에 미들웨어 적용: __construct(): $this->middleware('foo');
	* $this->middleware('guest', [ 'only' => ['foo', 'bar'] ]);
	* $this->middleware('guest', [ 'except' => ['foo'] ]);
* 이벤트 구독: 리스너 클래스 하나로 여러 이벤트 구독, 클래스 내부에서 이벤트 처리
	* event(new \App\Events\UserCreated($user));
	* EventServiceProvider::$subscribe = [ \App\Listeners\UsersEventListener::class, ];
		* 이벤트 리스너임과 동시에 이벤트 구독자
	* UsersEventListener::subscribe($event) { $event->listen(외부 이벤트 클래스, 내부 이벤트 메소드); }
	* UsersEventListener::onUserCreated($event) { ... }

## 24 소셜 로그인
* 소셜라이트 컴포넌트: composer require "laravel/socialite"
	* SocialiteServiceProvider::class, Socialite::class
* users.password 컬럼 null 허용 마이그레이션 필요 컴포넌트: composer require doctrine/dbal
* $user = \Socialite::driver($provider)->user();
	* $user = (\App\User::whereEmail($user->getEmail())->first()) ?: \App\User::create([ ... ]);
* 질의 스코프: 반복 질의 처리를 위해 모델에 메소드 선언
	* 메소드 이름은 scope 접두어 뒤 파스칼 표기법 스코프 이름 
		* scopeSocialUser(Illuminate\Database\Eloquent\Builder $query, $emil) { return $query->where...; }
	* 사용: $socialUser = \App\User::socialUser($email);

## 25 아티클 기능 구현
* 라우트 모델 바인딩: 라우트 파라미터 값에 해당하는 모델을 컨트롤러에서 조회 생략하고 바로 사용
	* RouteServiceProvider::boot() { parent::boot(); Route::model('article', \App\Article::class); }
	* $id 기반 조회 생략: ArticlesController::show($article) { return view('articles.show', compact('article')); }
* 아티클 목록: @forelse($articles as $article) @include('articles.partial.article', compact('article')) @empty ... @endforelse
	* 페이지네이션: @if($articles->count()) {!! $articles->appends(Request::except('page'))->render() !!}
		* 각 페이지 별 링크에 질의 스트링 보존
	* 아티클 항목 링크: ```<a href="{{ route('articles.show', $article->id) }}"> {{ $article->title }} </a>```
* gravatar
* @php ... @endphp
* {!! method_field('PUT') !!}
* ajax
	* jQuery.ajaxSetup({ header: { 'X-CSRF-TOKEN': jQuery('meta[name="csrf-token"]').attr('content') } });
	* jQuery.ajax({ type: 'DELETE', ... });
	* return response()->json([], 204);
* 인증: ArticlesController::__construct(): $this->middleware('auth', ['except' => ['index', 'show']]);
* 인가
	* AuthServiceProvider::boot()
		* Gate::define('update', function($user, $model) { return $user->id === $model->user_id; });
	* ArticlesController::edit($article) { $this->authorize('update', $article); }
* 뷰 노출 여부 결정: @can('update', $article) ... @endcan
* 즉시 로드(with() 메소드 체인 대신 프로퍼티 이용): Article::$with = [ 'user' ];
* null object 패턴(undefined variable 대응): $article = new \App\Article;
	
## 26 태그 기능 구현
* 뷰 컴포저: ex) 모든 뷰에서 필요한 데이터 전달
	* AppServiceProvider::boot()
		* view()->composer('*', function($view) { $foo = ...; $view->with(compact('foo')); });
* 유효성 검사 규칙 추가: ArticlesRequest::rules() { return [ 'tags' => ['required', 'array'], ]; }
* 저장: ArticlesController::store($request) { ...; $article->tags()->sync($request->input('tags')); }

## 27 파일 첨부 기능 구현
* 유효성 검사에서 세션 저장 예외: ArticlesRequest::$dontFlash = ['files'];
* 유효성 검사: ArticlesRequest::rules() { return [ ...; 'files' => ['array'], 'files.*' => ['mimes:jpg,png,zip,tar', 'max:30000'] ]; }
* 메타 데이터 저장: 일대다: Article, Attachment
* UI 개선: npm install dropzone --save-dev

## 28 댓글 기능 구현
* 다형적 다대다: 외래키 연결: 사용자 대 댓글, 부모 댓글 대 자식 댓글
	* Comment::user(): return $this->belongsTo(User::class);
	* Comment::commentable(): return $this->morphTo();
	* Comment::replies(): return $this->hasMany(Comment::class, 'parent_id')->latest();
	* Comment::parent(): return $this->belongsTo(Comment::class, 'parent_id', 'id);
	* User::comments(): return $this->hanMany(Comment::class);
	* Article::comments(): return $this->morphMany(Comment::class, 'commentable');
* 중첩 라우트: 점(.): Route::resource('articles.comments', 'CommentsController', ['only' => 'store']);
	* /articles/{article}/comments 
* 라우트 모델 바인딩
* 댓글 목록: ArticlesController::show($article)
	* $comments = $article->comments()->with('replies')->whereNull('parent_id')->latest()->get();
* 댓글 저장: CommentsController::store($request, $article)
	* $comment = $article->comments()->create(array_merge($request->all(), ['user_id' => $request->user()->id]));
* 투표 기능
	* 외래키 연결: 댓글, 사용자
		* Vote::comment(): return $this->belongsTo(Comment::class);
		* Vote::user(): return $this->belongsTo(User::class);
		* Comment::votes(): return $this->hanMany(Vote::class);
		* User::votes(): return $this->hasMany(Vote::class);
	* 개수
		* Comment::getUpCountAttribute(): return $this->votes()->sum('up');
		* Comment::getDownCountAttribute(): return $this->votes()->sum('down);
	* 저장: CommentsController::vote($request, $comment)
		* $comment->votes()->create([...]);

## 29 다듬질 1
* 검색, 정렬: ArticlesController::index()
* 댓글 수: Article::getCommentCountAttribute(): return $this->comments->count();
* 알림 메일: 저장할 때 이벤트 던짐: event(new \App\Events\CommentsEvent($comment));
* missing 파일 삭제: 사용자 정의 아티즌 콘솔 작성
	* 명령 생성: php artisan make:command ClearOrphanedAttachments --command=my:coa
	* 콘솔 커널에 등록: Kernel::$commands = [ Commands\ClearOrphanedAttachments::class, ];
	* 등록 확인: php artisan
	* 명령 클래스 본문 작성: ClearOrphanedAttachments::handle()
	* cron 등록: php /path/artisan schedule:run >> /dev/null 2>&1
		* Kernel::schedule($schedule): $schedule->command('my:coa')->daily();
* 댓글 소프트 삭제
	* migration: $table->softDeletes();
	* Comment 모델: use SoftDeletes;
		* Comment::$dates = ['deleted_at'];
	* 댓글 목록: ArticlesController::show($article)
		* $comments = $article->comments()->with('replies')->withTrashed()->...
	* 댓글 삭제: CommentsController::destroy($comment)
		* $comment->delete() 혹은 $comment->forceDelete()
* 모델 질의에 캐시 적용 예제
	* 캐싱 로직: 부모 컨트롤러에 구현: Controller::cache(): return \Cache::remember();
	* 설정 플래그 작성: config/project.php: 'cache' => true,
	* 캐시 키 생성(헬퍼 함수 작성): ArticlesController::index(): $cacheKey = cache_key('articles.index');
	* 캐시 리턴: ArticlesController::index(): $articles = $this->cache($cacheKey, ...);
* 캐시 클리어: store(), update(), destroy(): 여러 메소드에서 사용되니 이벤트로 추출
	* 이벤트: event(new \App\Events\ModelChanged(['articles']));
	* 이벤트 채널/리스너
		* EventServiceProvider::$listen = [ ... \App\Events\ModelChanged::class => [\App\Listeners\CacheHandler::class], ... ];
		* php artisan event:generate
		* ModelChanged::__construct($cacheTags): $this->cacheTags = $cacheTags;
		* CacheHandler::handle(ModelChanged $event): return \Cache::flush();
* 캐시 저장소 변경(memcached)
	* 메모리 캐시: 캐시 태그(캐시 키는 요청마다, 캐시 태그는 모델/컨트롤러마다 다름) 사용 가능

## 30 다듬질 2
* 다국어 지원
	* 전역 config/app.php, 런타임 오버라이드 AppServiceProvider::boot()
	* 언어 사전 위치 resource/lang/*, 사용 trans()
	* 쿠키
		* $cookie = cookie()->forever('foo', 'bar'); cookie()->queue($cookie);
		* if(request()->cookie('foo') == $bar) ...
	* 예제: 다국어 태그, 다국어 메일
* 오류 알림(슬랙)



# 실전 프로젝트 3 - RESTful API

## 31 기본기 익히기
* 메소드 오버라이드: body에서 _method 파라미터 혹은 헤더에서 X-HTTP-Method-Override
* 리소스(엔드포인트): 동사 대신 명사, 복수(plural)
	* 컬렉션(목록): /articles, 목록(GET), 저장(POST)
	* 인스턴스(항목): /articles/{id}, 상세보기(GET), 수정(PUT), 삭제(DELETE)
	* 리소스 관계 노출: 중첩: /tags/{id}/articles
	* 질의 문자열: 물음표 뒤에 표현: /articles?foo=1&bar=2
* 응답: 코드, 메시지, ...
* api 버전: v1, v2, ...

## 32 구조 설계
* 라우팅: Route::group(): domain, namespace, prefix
* 응답: return response()->json([ ... ], $code, [], JSON_PRETTY_PRINT);
* 응답(아티클): return $article->toJson(JSON_PRETTY_PRINT);

## 33 클라이언트 인증
* HTTP 기본 인증: 헤더 Authorization 에 인증정보를 base64 인코딩
	* 라우트 미들웨어 사용: make:middleware 이후 커널에 등록
	* auth()->onceBasic(): 쿠키를 만들지 않음
* JWT(json web token) 인증
	* composer require tymon/jwt-auth
		* JWTAuthServiceProvider::class, JWTAuth::class, JWTFactory::class
	* 헬퍼: jwt() { return app('tymon.jwt.auth'); }, is_api_domain()
	* 요청 처리: auth()->attempt() 대신 jwt()->attempt()
	* 응답: return response()->json(['token'=>$token,], 201, [], JSON_PRETTY_PRINT);
	* 적용: JWT 미들웨어를 커널에 등록, 컨트롤러에 미들웨어 적용
	* 만료 토큰 교체
* Oauth: composer require league/oauth2-server

## 34 데이터 트랜스폼
* 수동
	* 컨트롤러에서 json 응답 대신 트랜스포머 객체 리턴
		* return (new \App\Transformers\ArticleTransformerBasic)->withPagination($article); 
		* return (new \App\Transformers\ArticleTransformerBasic)->withItem($article);
	* ArticleTransformerBasic::withPagination($articles): $payload = [...]; return response()->json($payload, ...);
	* ArticleTransformerBasic::withItem($article): return response()->json($this->transform($article), ...);
	* ArticleTransformerBasic::transform($article): return [...];
* 컴포저: dingo/api, appkr/api
	* composer require appkr/api
		* ApiServiceProvider::class
	* php artisan make:transformer "App\Article" --includes="App\Comment:comments:true"
		* 내용 채우기: ArticlesTransformer::transform($article): $payload = [ ... ];
		* 적용(목록): ArticlesController::respondCollection($article)
			* return json()->withPagination($article, new \App\Transformers\ArticleTransformer);
		* 적용(항목): ArticlesController::respondInstance($article, $comments)
			* return json()->withItem($article, new \App\Transformers\ArticleTransformer);
		* ArticlesController::respondCreated($article)
	* php artisan make:transformer "App\Comment"
	* 직렬화(JsonApiSerializer)
* 다국어 지원

## 35 다듬질 1
* 캐싱: Etag, If-None-Match: hit 일 경우 304 빈 본문, miss 일 경우 새 Etag 헤더와 함께 응답 본문
	* EtagTrait::etag(): 항목 updated_at + 캐시 키
	* EtagTrait::etags(): etag() 리턴값들 결합 + 캐시 키

## 36 다듬질 2
* CORS: 헤더 Access-Control-Allow-Origin
	* composer require barryvdh/laravel-cors
		* CORS: 클라이언트 Origin 요청 헤더 검사, Access-Control-* 응답 헤더 추가: 미들웨어 적용
		* ServiceProvider::class
* 사용량 제한: throttle 미들웨어: 커널에 등록 후 api 라우팅에 포함
* 로그인 오류 횟수 제한
* 난독화(리소스 아이디): composer require jenssegers/optimus



# 코드 배포

## 37 서버 준비

## 38 코드 배포 
* envoy
	* composer require laravel/envoy
		* echo 'export PATH="$PATH:$HOME/.composer/vendor/bin" >> ~/YOUR_SHELL_PROFILE'
	* github 연결
	* 배포 전략: clone

