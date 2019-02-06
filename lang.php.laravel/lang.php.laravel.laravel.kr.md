# getting started

## installation: https://laravel.kr/docs/5.6/installation
* 프로젝트 생성: composer create-project --prefer-dist laravel/laravel foo
* 소유자/퍼미션 변경: storage, bootstrap/cache
* 앱 키 설정: php artisan key:generate

## configuration: https://laravel.kr/docs/5.6/configuration
* 설정 디렉토리/파일: config, .env

## deployment: https://laravel.kr/docs/5.6/deployment
* autoloader 최적화: composer install --optimize-autoloader --no-dev
* 설정내역 로딩 최적화: php artisan config:cache
* 라우트 로딩 최적화: php artisan route:cache



# architecture concepts

## lifecycle: https://laravel.kr/docs/5.6/lifecycle
* public/index.php, boostrap/app.php, app/Http/Kernel.php, app/Providers

## service container: https://laravel.kr/docs/5.6/container
* 바인딩: $this->app->bind(); $this->app->extend(); $this->app->instance(); $this->app->singleton(); $this->app->tag(); $this->app->when()->needs()->give();
* 의존성 해결: $this->app->make(); $this->app->makeWith(); resolve();
* 컨테이너 이벤트: $this->app->resolving();

## providers: https://laravel.kr/docs/5.6/providers
* 서비스 프로바이더 작성: php artisan make:provider FooServiceProvider

## facades: https://laravel.kr/docs/5.6/facades
* App, Artisan, Auth, Auth(Instance), Blade, Broadcast, Broadcast(Instance), Bus, Cache, Cache(Instance), Config, Cookie, Crypt, DB, DB(Instance), Event, File, Gate, Hash, Lang, Log, Mail, Notification, Password, Password(Instance), Queue, Queue(Instance), Queue(Base Class), Redirect, Redis, Redis(Instance), Request, Response, Response(Instance), Route, Schema, Session, Session(Instance), Storage, Storage(Instance), URL, Validator, Validator(Instance), View, View(Instance)

## contracts: https://laravel.kr/docs/5.6/contracts



# The Basics

## routing: https://laravel.kr/docs/5.6/routing
* 라우팅
	* Route::delete(); Route::get(); Route::options(); Route::patch(); Route::post(); Route::put(); 
	* Route::any(); Route::match(); Route::redirect() Route::view(); 
* 라우트 그룹
	* Route::group(); Route::domain()->group(); Route::middleware()->group(); Route::name()->group(); Route::namespace()->group(); Route::prefix()->group(); 
* 현재 라우팅 정보: Route::current(); Route::currentRouteAction(); Route::currentRouteName(); 

## middleware: https://laravel.kr/docs/5.6/middleware
* 미들웨어 생성: php artisan make:middleware Foo

## controllers: https://laravel.kr/docs/5.6/controllers
* 컨트롤러 리소스: php artisan make:controller FooController --resource
	* 리소스풀 컨트롤러 액션들
* 리소스 모델 지정: php artisan make:controller FooController --resource --model=Foo
* api 리소스 컨트롤러: php artisan make:controller API/FooController --api
* 라우트 캐시: php artisan route:cache, php artisan route:clear

## requests: https://laravel.kr/docs/5.6/requests
* $request->fullUrl(); $request->is(); $request->isMethod(); $request->method(); $request->path(); $request->url(); 
* $request->all(); $request->input(); $request->query();
* $request->except(); $request->filled(); $request->foo; $request->has(); $request->only(); 
* $request->flash(); $request->flashExcept(); $request->flashOnly(); 
	* redirect('form')->withInput();
* $request->cookie(); $request->old(); 
* $request->file(); $request->foo->extension(); $request->foo->path(); $request->file()->isValid(); $request->hasFile();
* $request->foo->store(); $request->foo->storeAs();

## responses: https://laravel.kr/docs/5.6/responses
* response()->header(); response()->header()->cookie(); response()->withHeaders();
* back()->withInput(); redirect(); redirect()->action(); redirect()->away(); redirect()->route(); redirect()->with();
* response()->json(); response()->json()->withCallback(); response()->view()->header();
* response()->download(); response()->download()->deleteFileAfterSend(); response()->file(); response()->streamDownload();

## views: https://laravel.kr/docs/5.6/views
* view(); view()->first(); view()->with(); View::exists(); View::share();
* View::composer(); View::creator();

## urls: https://laravel.kr/docs/5.6/urls
* url(); url()->current(); url()->full(); url()->previous();
* URL::signedRoute(); URL::temporarySignedRoute();
* action();

## session: https://laravel.kr/docs/5.6/session
* $request->session()->all(); $request->session()->exists(); $request->session()->flash(); $request->session()->flush(); $request->session()->forget(); $request->session()->get(); $request->session()->has(); $request->session()->keep(); $request->session()->pull(); $request->session()->push(); $request->session()->put(); $request->session()->reflash(); $request->session()->regenerate();
* session();

## validation: https://laravel.kr/docs/5.6/validation
* $request->validate();
* form requests 생성: php artisan make:request StoreBlogPost
* Validator::make(); Validator::make()->fails(); Validator::make()->validate();
* redirect()->withErrors()->withInput();
* Validator::make()->after(); Validator::make()->errors()->first(); Validator::make()->errors()->get(); Validator::make()->errors()->has(); Validator::make()->sometimes();
* Rule::unique()->ignore(); Rule::unique()->where();
* 사용자 정의 유효성 검사 규칙: php artisan make:rule Foo
* Validator::extend(); Validator::extendImplicit(); Validator::make()->passes(); Validator::replacer();

## errors: https://laravel.kr/docs/5.6/errors
* App\Exceptions\Handler
* abort(); report();
* {{ $exception->getMessage() }}

## logging: https://laravel.kr/docs/5.6/logging
* Log::alert(); Log::critical() Log::debug(); Log::emergency(); Log::error(); Log::info(); Log::notice(); Log::warning();
* Log::channel()->info(); Log::stack()->info();



# frontend

## blade: https://laravel.kr/docs/5.6/blade
* 레이아웃: @extends(), @hasSection(), @section(), @show, @yield()
* 컴포넌트&슬롯: @alert(), Blade::component(); @component(), @slot(), {{ $slot }}
* 데이터 표시: {{ }}, {!! !!}, @{{ }}, {{-- --}}, Blade::withoutDoubleEncoding(); @json(); @php, @verbatim, 
* 컨트롤 구조: @empty(), @for(), @foreach(), @forelse(), @if(), @isset(), @switch(), @unless(), @while()
	* $loop->count, $loop->depth, $loop->first, $loop->index, $loop->iteration, $loop->last, $loop->parent, $loop->remaining
* 인증: @auth, @auth(), @guest, @guest()
* 하위 뷰 포함: @include(), @includeFirst(), @includeIf(), @includeWhen()
* @each(), @prepend(), @push(), @stack()
* 서비스 인젝션 주입: @inject()
* 블레이드 기능 확장: Blade::directive(); Blade::if();
* 블레이드 뷰 캐시 제거: php artisan view:clear

## localization: https://laravel.kr/docs/5.6/localization
* App::getLocale(); App::isLocale(); App::setLocale();
* __(); {{ __() }}, @lang(),
* trans_choice();



# security

## authentication: https://laravel.kr/docs/5.6/authentication
* 인증 라우트/뷰 스캐폴딩: php artisan make:auth
* Auth::check(); Auth::guard(); Auth::id(); Auth::user();
* 라우트 보호: Route::get()->middleware('auth'); Route::get()->middleware('auth.basic'); Route::get()->middleware('auth.basic.once'); $this->middleware('auth');
* Auth::attempt(); Auth::guard()->login(); Auth::login(); Auth::loginUsingId(); Auth::logout(); Auth::logoutOtherDevices(); Auth::once(); Auth::onceBasic(); Auth::provider(); Auth::viaRemember(); Auth::viaRequest(); 
* 인증 과정 중 이벤트: EventServiceProvider

## api authentication: https://laravel.kr/docs/5.6/passport
* api 인증(passport): composer require laravel/passport

## authorization: https://laravel.kr/docs/5.6/authorization
* gate: Gate::after(); Gate::allows(); Gate::before(); Gate::define(); Gate::denies(); Gate::forUser()->allows(); Gate::forUser()->denies(); Gate::resource();
* policy 클래스 생성: php artisan make:policy FooPolicy
* policy 클래스(CRUD 포함) 생성: php artisan make:policy FooPolicy --model=Foo
* @can(), @cannot()

## encryption: https://laravel.kr/docs/5.6/encryption
* Crypt::encryptString(); Crypt::decryptString(); decrypt(); encrypt();

## hash: https://laravel.kr/docs/5.6/hashing
* Hash::check(); Hash::make(); Hash::needsRehash();



# digging deeper

## artisan: https://laravel.kr/docs/5.6/artisan
* php artisan make:command Foo, php artisan help foo, php artisan list, php artisan tinker
* Artisan::call(); Artisan::command(); Artisan::queue();

## broadcasting: https://laravel.kr/docs/5.6/broadcasting
* broadcast(); Broadcast::channel(); Broadcast::routes(); event();
* 채널 클래스 생성: php artisan make:channel FooChannel

## cache: https://laravel.kr/docs/5.6/cache
* Cache::add(); Cache::decrement(); Cache::extend(); Cache::flush(); Cache::forever(); Cache::forget(); Cache::get(); Cache::has(); Cache::increment(); Cache::remember(); Cache::rememberForever(); Cache::pull(); Cache::put(); Cache::store()->get(); Cache::store()->put(); Cache::tags();
* cache();

## collections: https://laravel.kr/docs/5.6/collections
* Collection::macro();
* collect();
	* all average avg chunk collapse combine concat contains containsStrict count crossJoin dd diff diffAssoc diffKeys dump each eachSpread every except filter first firstWhere flatMap flatten flip forget forPage get groupBy has implode intersect intersectByKeys isEmpty isNotEmpty keyBy keys last macro make map mapInto mapSpread mapToGroups mapWithKeys max median merge min mode nth only pad partition pipe pluck pop prepend pull push put random reduce reject reverse search shift shuffle slice sort sortBy sortByDesc sortKeys sortKeysDesc splice split sum take tap times toArray toJson transform union unique uniqueStrict unless unwrap valuesk when where whereStrict whereIn whereInStrict whereNotIn whereNotInStrict wrap zip

## events: https://laravel.kr/docs/5.6/events
* EventServiceProvider; Event::listen(); event();
* 이벤트 & 리스너 생성: php artisan event:generate
* 큐 처리 이벤트 리스너: ShouldQueue 인터페이스 추가
* 이벤트 Subscriber

## filesystem: https://laravel.kr/docs/5.6/filesystem
* 심볼릭 링크: php artisan storage:link
* asset(); storage_path();
* Storage::allDirectories(); Storage::allFiles(); Storage::append(); Storage::copy(); Storage::delete(); Storage::deleteDirectory(); Storage::directories(); Storage::disk()->delete(); Storage::disk()->exists(); Storage::disk()->put(); Storage::download(); Storage::files(); Storage::getVisibility(); Storage::makeDirectory(); Storage::move(); Storage::put(); Storage::get(); Storage::url(); Storage::temporaryUrl(); Storage::size(); Storage::lastModified(); Storage::prepend(); Storage::putFile(); Storage::putFileAs(); Storage::setVisibility();
* $request->file()->store(); $request->file()->storeAs();

## helpers: https://laravel.kr/docs/5.6/helpers
* 배열 & 객체: array_add array_collapse array_divide array_dot array_except array_first array_flatten array_forget array_get array_has array_last array_only array_pluck array_prepend array_pull array_random array_set array_sort array_sort_recursive array_where array_wrap data_fill data_get data_set head last
* 경로: app_path base_path config_path database_path mix public_path resource_path storage_path
* 문자열: __ camel_case class_basename e ends_with kebab_case preg_replace_array snake_case starts_with str_after str_before str_contains str_finish str_is str_limit Str::orderedUuid str_plural str_random str_replace_array str_replace_first str_replace_last str_singular str_slug str_start studly_case title_case trans trans_choice Str::uuid 
* URLs: action asset secure_asset route secure_url url
* 기타: abort abort_if abort_unless app auth back bcrypt blank broadcast cache class_uses_recursive collect config cookie csrf_field csrf_token dd decrypt dispatch dispatch_now dump encrypt env event factory filled info logger method_field now old optional policy redirect report request rescue resolve response retry session tap today throw_if throw_unless trait_uses_recursive transform validator value view with

## mail: https://laravel.kr/docs/5.6/mail
* Mailgun, SparkPost, 아마존 SES
* Mailables 생성: php artisan make:mail Foo
* Mailables 생성(마크다운): php artisan make:mail Foo --markdown=emails.foo
	* @component('mail::message') @component('mail::button') @component('mail::panel') @component('mail:table')
* Mail::to()->cc()->bcc()->queue(); Mail::to()->cc()->bcc()->later(); Mail::to()->cc()->bcc()->send(); Mail::to()->send(); ShouldQueue
* 이벤트(큐 아닌 직접 발송시): MessageSending, MessageSent

## notification: https://laravel.kr/docs/5.6/notifications
* 알림 생성: php artisan make:notification Foo
* Notificable 트레이트: $user->notify();
* Notification 파사드: Notification::send();
* 큐를 통한 notification: ShouldQueue 인터페이스 구현, Queueable 트레이트 사용
	* $user->notify()->delay();
* Notification::route()->route()->notify();
* 알림(메일): MailMessage(); Mailable(); 
* 알림(메일) 템플릿 커스텀: php artisan vendor:publish --tag=laravel-notifications
* 알림(메일-마크다운): php artisan make:notification Foo --markdown=mail.foo
* 알림(데이터베이스): php artisan notifications:table && php artisan migrate
	* $user->notifications
	* $user->unreadNotifications
* 알림(브로드캐스팅): BroadcastMessage(); Echo.private();
* 알림(SMS): NexmoMessage()
* 알림(슬랙): SlackMessage()
 
## package: https://laravel.kr/docs/5.6/packages
* 라라벨/헬퍼 접근 가능 패키지: https://github.com/orchestral/testbench
* 패키지 discovery 추가/제외; 서비스 프로바이더
* artisan 명령어 등록: $this->commands();
* public asssets: $this->publishes();
	* 패키지 asset들을 지정된 퍼블리싱 위치로 복사: php artisan vendor:publish --tag=public --force
	* 패키지 asset들과 resource 파일들을 그룹단위로 퍼블리싱: php artisan vendor:publish --tag=config
	
## queues: https://laravel.kr/docs/5.6/queues
* config/queue.php: db, beanstalkd, amazon SQS, redis, sync
* Job::dispatch(); Job::dispatch()->onQueue('emails');
* job 큐 우선 순위 부여: php artisan queue:work --queue=high,default
* 드라이버 준비(DB): php artisan queue:table && php artisan migrate
* job 클래스 생성: php artisan make:job ProcessFoo
* job 처리: ProcessFoo::dispatch(); ProcessFoo::dispatch()->delay();
* job 체이닝: ProcessFoo::withChain()->dispatch(); ProcessFoo::withChain()->dispatch()->allOnConnection()->allOnQueue();
* ProcessFoo::dispatch()->onConnection(); ProcessFoo::dispatch()->onConnection()->onQueue(); ProcessFoo::dispatch()->onQueue();
* 최대 재시도 횟수(job 클래스 내 $tries 값이 우선): php artisan queue:work --tries=3
* 최대 재시도 시간: job 클래스 내 retryUnit();
* 최대 수행 시간(job 클래스 내 $timeout 값이 우선): php artisan queue:work --timeout=30
* 실행 속도 제한: Redis::throttle()->allow()->every()->then();
* job 동시 처리 worker 최대 개수 지정: Redis::funnel()->limit()->then();
* 큐 worker 실행: php artisan queue:work
	* 단일 job 지정: php artisan queue:work --once
	* 커넥션 지정: php artisan queue:work redis
	* 큐 지정: php artisan queue:work redis --queue=emails
* 리소스 고려사항(메모리 해제): 데몬 큐 worker는 각 job을 처리하기 전에 프레임워크 리부트 하지 않음
* 큐 worker 코드 변경 적용: php artisan queue:restart
* worker 잠자기 시간: php artisan queue:work --sleep=3
* supervisor 설치: apt-get install supervisor
	* queue:worker 프로세스 종료시 자동으로 재시작
* 실패 job 처리 테이블: php artisan queue:failed-table && php artisan migrate
* 실패 job 보기(DB 테이블): php artisan queue:failed
* 실패 job 재시작: php artisan queue:retry 5
	* 실패 job 모두 재시작: php artisan queue:retry all
* 실패 job 삭제: php artisan queue:forget 5
	* 실패 job 모두 삭제: php artisan queue:flush
* job 이벤트: Queue::after(); Queue::before(); Queue::looping();

## scheduling: https://laravel.kr/docs/5.6/scheduling
* cron 등록: * * * * * php /path-to-your-project/artisan schedule:run >> /dev/null 2>&1
* App\Console\Kernel 클래스 schedule()
	* $schedule->call()->daily();
	* $schedule->command()->daily();
	* $schedule->exec()->daily();
	* $schedule->command()->daily()->before()->after();	
	* $schedule->command()->daily()->pingBefore()->thenPing();
	* $schedule->command()->daily()->sendOutputTo(); $schedule->command()->sendOutputTo()->emailOutputTo();
	* $schedule->command()->daily()->skip(); $schedule->command()->daily()->when();
	* $schedule->command()->fridays()->at()->onOneServer();
	* $schedule->command()->hourly()->between(); $schedule->command()->hourly()->unlessBetween();
	* $schedule->command()->timezone()->at();
	* $schedule->command()->withoutOverlapping();
	* $schedule->job()->everyFiveMinutes();
	


# database

## database: https://laravel.kr/docs/5.6/database
* read, write 커넥션 설정
* 여러 커넥션 사용: DB::connection('foo')->...;
* pdo 인스턴스: DB::connection()->getPdo();
* raw 쿼리: DB::delete(); DB::insert(); DB::select(); DB::statement(); DB::update();
* 쿼리 이벤트 리스닝: DB::listen();
* DB 트랜잭션: DB::transaction();
	* 수동: DB::beginTransaction(); DB::commit(); DB::rollBack();

## queries: https://laravel.kr/docs/5.6/queries
* 결과 조회
	* 모든 레코드: DB::table()->get();
	* 단일 레코드: DB::table()->where()->first();
	* 단일 컬럼: DB::table()->where()->value();
	* 행: DB::table()->pluck();
	* 결과 분할: DB::table()->orderBy()->chunk();
	* 집계(aggregates): DB::table()->avg(); DB::table()->count(); DB::table()->max(); DB::table()->min(); DB::table()->sum();
	* 존재 확인: DB::table()->where()->doesntExist(); DB::table()->where()->exists();
* select: DB::table()->distinct()->get(); DB::table()->select()->get(); $query->addSelect()->get();
* raw: sql 인젝션 주의: DB::havingRaw(); DB::orderByRaw(); DB::orHavingRaw(); DB::orWhereRaw(); DB::raw(); DB::selectRaw(); DB::whereRaw();
* join
	* inner: DB::table()->join(); DB::table()->join()->join()...;
	* left: DB::table()->leftJoin();
	* cross: DB::table()->crossJoin();
	* DB::table()->join('foo', function($join) { $join->on()->where(); })->get();
	* sub query: DB::table()->joinSub(); DB::table()->leftJoinSub(); DB::table()->rightJoinSub();
* union: DB::table()->union();
* where 
	* DB::table()->orWhere();
	* DB::table()->where();
	* DB::table()->where(function($query) { $query->where()->orWhere(); });
	* DB::table()->whereBetween();
	* DB::table()->whereColumn();
	* DB::table()->whereDate();
	* DB::table()->whereDay();
	* DB::table()->whereExists(function($query) { $query->select()->from()->whereRaw(); });
	* DB::table()->whereIn();
	* DB::table()->whereMonth();
	* DB::table()->whereNotBetween();
	* DB::table()->whereNotIn();
	* DB::table()->whereNotNull();
	* DB::table()->whereNull();
	* DB::table()->whereTime();
	* DB::table()->whereYear();
* where(json): DB::table()->where('foo->bar', 'test')->get();
* ordering: DB::table()->first(); DB::table()->inRandomOrder(); DB::table()->latest(); DB::table()->orderBy();
* grouping/having: DB::table()->groupBy()->having();
* skip/take: DB::table()->offset()->limit(); DB::table()->skip()->take();
* conditional: DB::table()->when();
* insert: DB::table()->insert();
* auto incrementing id(추가된 id 리턴): DB::table()->insertGetId();
* update: DB::table()->update();
* update(json): DB::table()->update(['foo->bar' => 'test']);
* 컬럼값 증가/감소: DB::table()->decrement(); DB::table()->increment();
* delete: DB::table()->delete(); DB::table()->truncate();
* 배타적 잠금(pessimistic locking): DB::table()->lockForUpdate(); DB::table()->sharedLock();

## pagination: https://laravel.kr/docs/5.6/pagination
* 쿼리 빌더 결과 페이징: DB::table()->paginate(); DB::table()->simplePaginate();
* 엘로퀀트 결과 페이징: App\User::paginate(); User::where()->paginate(); User::where()->simplePaginate();
* 수동 Paginator 생성: LengthAwarePaginator; Paginator;
* 페이지네이션 결과 출력: {{ $fooPlural->links() }}
* paginator uri 구성: $fooPlural->withPath();
* 질의 스트링 추가: {{ $fooPlural->appends()->links() }} {{ $fooPlural->fragment()->links() }}
* 페이지네이션 결과 출력(json): toJson();
* 페이지네이션 뷰 커스텀(복사): php artisan vendor:publish --tag=laravel-pagination
* 페이지네이션 뷰 커스텀: $paginator->links('foo'); Paginator::defaultSimpleView(); Paginator::defaultView();
* paginator 인스턴스 메소드: $results->count(); $results->currentPage(); $results->firstItem(); $results->hasMorePages(); $results->lastItem(); $results->lastPage(); $results->nextPageUrl(); $results->perPage(); $results->previousPageUrl(); $results->total(); $results->url($page);

## migration: https://laravel.kr/docs/5.6/migrations
* 마이그레이션 파일 생성
	* php artisan make:migration create_users_table
	* php artisan make:migration create_users_table --create=users
	* php artisan make:migration add_votes_to_users_table --table=users
* 마이그레이션
	* php artisan migrate
	* php artisan migrate --force
* 롤백
	* php artisan migrate:rollback
	* php artisan migrate:rollback --step=5
* 리셋: php artisan migrate:reset
* 롤백&마이그레이트
	* php artisan migrate:refresh
	* php artisan migrate:refresh --seed
	* php artisan migrate:refresh --step=5
* 모든 테이블&마이그레이션 drop
	* php artisan migrate:fresh
	* php artisan migrate:fresh --seed
* 테이블: Schema::connection()->create(); Schema::create(); Schema::drop(); Schema::dropIfExists(); Schema::hasColumn(); Schema::hasTable(); Schema::rename();
* 컬럼 생성/수정/삭제: Schema::table('foo', function($table) { $table->... });
* 인덱스 생성/변경/삭제: $table->...
* 외래키: $table->foregin()->references()->on(); $table->foregin()->references()->on()->onDelete();
* 외래키 제약 활성/비활성: Schema::disableForeignKeyConstraints(); Schema::enableForeignKeyConstraints();

## seeding: https://laravel.kr/docs/5.6/seeding
* seeder 생성: php artisan make:seeder UsersTableSeeder
* seeder 클래스 run(): DB::table()->insert([...]); $this->call([...]);
* 모델 팩토리: factory()->create()->each();
* seeder 실행
	* composer dump-autoload
	* php artisan db:seed
	* php artisan db:seed --class=UsersTableSeeder

## redis: https://laravel.kr/docs/5.6/redis
* composer require predis/predis
* Redis::command(); Redis::connection(); Redis::get(); Redis::lrange(); Redis::pipeline(); Redis::psubscribe(); Redis::publish(); Redis::set(); Redis::subscribe();



# eloquent ORM

## eloquent: https://laravel.kr/docs/5.6/eloquent
* 모델 생성: php artisan make:model Foo
	* php artisan make:model Foo --migration
* 모델 목록 조회(Collection 인스턴스): App\Foo::all(); App\Foo::where()->orderBy()->take()->get();
	* 결과 분할: Foo::chunk(); Foo::where()->cursor();
* 모델 항목 조회: App\Foo::find(); App\Foo::where()->first();
* 예외 처리: App\Foo::findOrFail(); App\Foo::where()->firstOrFail();
* 합계 조회: App\Foo::where()->count(); App\Foo::where()->max();
* 모델 추가: $foo = new Foo; ...; $foo->save();
* 모델 수정: $foo = App\Foo::find(1); ...; $foo->save();
	* 모델 목록 수정: App\Foo::where()->update();
* 모델 추가(대량 할당)
	* $fillable = [...]; $guarded = [...]; 
	* App\Foo::create(); $foo->fill();
	* App\Foo::firstOrCreate(); App\Foo::firstOrNew();
	* App\Foo::updateOrCreate();
* 모델 삭제: $foo->delete(); App\Foo::destroy();
* 모델 목록 삭제: App\Foo::where()->delete();
* 조회에 소프트 삭제 포함: App\Foo::withTrashed()->where()->get(); $foo->history()->withTrashed()->get();
* 소프트 삭제만 조회: App\Foo::onlyTrashed()->where()->get();
* 소프트 삭제 복구: App\Foo::restore(); $foo->history()->restore();
* 소프트 삭제 목록 복구: App\Foo::withTrashed()->where()->restore();
* 소프트 삭제를 완전 삭제: $foo->forceDelete(); $foo->history()->forceDelete();
* 질의 스코프(글로벌): static::addGlobalScope();
* 질의 스코프(글로벌) 제거: Foo::withoutGlobalScope()->get();
* 질의 스코프(로컬): scopeBar(); App\User::bar()->get();
* 이벤트: created, creating, deleted, deleting, restored restoring, retrieved, saved, saving, updated, updating, 
	* $dispatchesEvents = [ ... ];
* 옵저버 생성: php artisan make:observer FooObserver --model=Foo
	* Foo::observe(FooObserver::class);

## eloquent: relationships: https://laravel.kr/docs/5.6/eloquent-relationships
* 일대일 관계: belongsTo(); belongsTo()->withDefault(); hasOne();
* 일대다 관계: belongsTo(); hasMany();
* 다대다 관계: belongsToMany(); belongsToMany()->withPivot(); belongsToMany()->withTimestamps();
	* 중간 테이블 조회: foreach($foo->bars as $bar) { $bar->pivot->...; }
	* 중간 테이블 컬럼 필터링: belongsToMany()->wherePivot(); belongsToMany()->wherePivotIn();
	* 중간 테이블 정의(커스텀): belongsToMany()->using();
* 연결을 통한 다수 관계 정의: hasManyThrough();
* 다형성 관계: morphMany(); morphTo();
	* 다형성 타입(사용자 정의): Relation::morphMap();
* 다대다 다형성 관계 정의: morphedByMany(); morphToMany();
* 관계 질의(연결): 지연 로드됨: $foo->bar()->where()->get();
* 관계 존재 여부 질의: App\Foo::has()->get(); App\Foo::whereHas();
* 관계 미존재 여부 질의: App\Foo::doesntHave()->get(); App\Foo::whereDoesntHave()->get();
* 연관된 모델 개수 확인(카운팅): App\Post::withCount();
* 관계의 Eager 로딩: N+1 질의 문제 해결: App\Foo::all(); 대신 App\Foo::with()->get();
	* 부모 모델 조회 이후 관계 Eager 로딩: $bars = App\Foo::all(); if($condition) $bars->load();
	* 미로딩시에만 관계 모델 로딩: loadMissing();
* 연관 모델 삽입/수정
	* save: eloquent 모델 인스턴스를 받음: $foo->bars()->save(); $foo->bars()->saveMany();
	* create: php 배열을 받음: $fool->bars()->create();
* belongsTo 관계 변경: $foo->bar()->associate(); $foo->save();
* belongsTo 관계 제거: $foo->bar()->dissociate(); $foo->save();
* 다대다 관계 추가/제거: $foo->bars()->attach(); $foo->bars()->detach();
* 다대다 관계 연결 동기화: $foo->bars()->sync(); $foo->bars()->syncWithoutDetaching();
* 다대다 연결 토글: $foo->bars()->toggle();
* 피벗 테이블 추가적 데이터 저장: $foo->bars()->save();
* 피벗 테이블 레코드 수정: $foo->bars()->updateExistingPivot();
* 부모의 타임스탬프 값 갱신: $touches = ['foo'];

## eloquent: mutators: https://laravel.kr/docs/5.6/eloquent-mutators 
* 날짜 mutators: $dates = [];
* date formats: $dateFormat = '';
* 속성 캐스팅: $casts = []; 
	* 배열 & JSON 캐스팅: $casts = [ 'foo' => 'array' ];
	* 날짜 캐스팅: $casts = ['foo' => 'datetime:Y-m-d'];

## eloquent: api resource: https://laravel.kr/docs/5.6/eloquent-resources
* 리소스 클래스 생성: php artisan make:resource Bar
* 리소스 컬렉션 생성
	* php artisan make:resource Bars --collection
	* php artisan make:resource BarCollection
* BarResource::collection(); 
* 페이지네이션: return new FooCollection(Foo::paginate());
* 조건에 따른 표현: return [ 'foo' => $this->when(Auth::user()->isAdmin(), 'bar'), ];
* 조건에 따른 포함: return [ $this->mergeWhen(Auth::user()->isAdmin(), ['foo' => 'bar']), ];
* 조건에 따른 관계 표시: return [ 'bars' => BarResource::collection($this->whenLoaded('bars')), ];
* 조건에 따른 피벗 정보 포함: return [ 'foo' => $this->whenPivotLoaded('bar', function() { return $this->pivot->...; }), ];
* 메타 데이터 추가
	* toArray(); with();
	* return new FooCollection()->additional();
* 리소스 응답
	* return new FooResource()->response()->header();
	* withResponse();

## eloquent: serialization: https://laravel.kr/docs/5.6/eloquent-serialization
* 모델 & 컬렉션 serializing: toArray(); toJson(); php의 json 인코딩 옵션 지정 가능
* json 변환시 속성값 숨기기: $hidden = []; $visible = [];
	* 노출도 일시적 수정: $foo->makeHidden('bar')->toArray(); $foo->makeVisible('bar')->toArray();
* json 변환시 특정 값 추가: accessor 정의 후 $appends = []; 추가
	* 런타임 추가: $foo->append()->toArray(); $foo->setAppends()->toArray();
* 날짜 serialization: $casts = [ 'foo' => 'date:Y-m-d', 'bar' => 'datetime:Y-m-d', ];



# 테스팅

## 시작하기: https://laravel.kr/docs/5.6/testing 
* 테스트 생성
	* php artisan make:test UserTest
	* php artisan make:test UserTest --unit



# 공식 패키지들

## Cashier: https://laravel.kr/docs/5.6/billing
* 구독(정기 과금) 서비스
* composer require laravel/cashier

## Envoy: https://laravel.kr/docs/5.6/envoy
* 원격 서버 작업 실행
* composer global require laravel/envoy

## Horizon: https://laravel.kr/docs/5.6/horizon
* redis queue 대시보드
* composer require laravel/horizon

## Passport: https://laravel.kr/docs/5.6/passport
* api 사용자 인증
* composer require laravel/passport

## Scout: https://laravel.kr/docs/5.6/scout
* full-text 검색
* composer require laravel/scout

## Socialite: https://laravel.kr/docs/5.6/socialite
* OAuth 인증(소셜)
* composer require laravel/socialite