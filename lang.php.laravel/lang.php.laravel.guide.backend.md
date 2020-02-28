# 라라벨 백엔드 가이드

## 목차
* 개요
* Controller, Model, Resource  
* DB Factory/Migration/Seeder
* Eloquent ORM/Relationship, Query Builder
* Event, Listener, Observer
* ~~Queue, Notification~~
* ~~Policy~~
* ~~Middleware, Provider~~


## 개요
* 엔티티: player(플레이어), client(의뢰자), quest(퀘스트)
    * quest-player: 다대일
    * client-player: 다대다
* 개발 방법: 샘플 데이터를 구성하고 코드로 테스트하는 것을 반복


## Controller, Model, Resource
* 목록과 항목의 CRUD를 위한 컨트롤러/모델
    * php artisan make:controller Api/v1/Player/PlayersController --api --model=Models/Player/Player
    * php artisan make:controller Api/v1/Client/ClientsController --api --model=Models/Client/Client
    * php artisan make:controller Api/v1/Quest/QuestsController --api --model=Models/Quest/Quest
    * php artisan make:model Models/Client/ClientPlayer
* 모델 설정: $fillable, $table, $casts
* api 응답을 위한 항목 Resource, 목록 Collection
    * php artisan make:resource Player/PlayerResource
    * php artisan make:resource Client/ClientCollection 
* 메소드 구현: index(), show(), store(), update(), destroy()
    * rest get, post, put, delete
* 참고
    * artisan: https://github.com/seokjoon/doc-cs/tree/master/lang.php.laravel/lang.php.laravel.cmd.artisan.md
    * resource: https://laravel.kr/docs/6.x/eloquent-resources


## DB Factory/Migration/Seeder
* 테이블 생성
    * php artisan make:migration create_players_table --create=players
    * php artisan make:migration create_clients_table --create=clients
    * php artisan make:migration create_quests_table --create=quests
    * php artisan make:migration create_client_player_table --create=client_player
    * php artisan migrate 
        * 제거: php artisan migrate:rollback
* 샘플 테이터 생성
    * php artisan make:factory PlayerFactory --model=Models/Player/Player
    * php artisan make:factory ClientFactory --model=Models/Client/Client
    * php artisan make:factory QuestFactory --model=Models/Quest/Quest
    * php artisan make:factory ClientPlayerFactory --model=Models/Client/ClientPlayer
    * php artisan make:seeder PlayersTableSeeder
    * php artisan make:seeder ClientsTableSeeder
    * php artisan make:seeder QuestsTableSeeder
    * php artisan make:seeder ClientPlayerTableSeeder
    * 편집: DatabaseSeeder.php
        * 외래키 제한 임시 비활성 필요
    * php artisan db:seed


## Eloquent ORM/Relationship, Query Builder
* 모델 메소드 생성
    * Player
        * clients(): client-player: 다대다: belongsToMany
        * quests(): quest-player: 다대일: hasMany
    * Client
        * players(): client-player: 다대다: belongsToMany
    * Quest
        * player(): quest-player: 다대일: belongsTo
* php artisan tinker
    * $p = Player::find(1)
        * $p->quests
            * $p->quests[0]->player
        * $p->clients
    * $c = Client::find(2)
        * $c->players[2]->quests
    * $q = Quest::find(5)
        * $q->player->clients
* 질의, with(eager 로딩), resource
    * $outs = Client::with('players')->get()->all();
    * $outs = Player::with('clients', 'quests'')->get()->all();
    * 라우터에서 질의 찍어보면 N+1 문제 여부 확인 가능
    * resource, collection 에서 출력 편집
    * api/v1/clients
    * api/v1/players/2
* 참고
    * create, update: sync()
    * eloquent relationship: https://laravel.kr/docs/6.x/eloquent-relationships
    * 세부 질의: 쿼리 빌더
        * https://laravel.kr/docs/6.x/queries
        * https://github.com/seokjoon/doc-cs/tree/master/lang.php.laravel/lang.php.laravel.db.queryBuilder.md

## Event, Listener, Observer
* 스캐폴드 생성
    * app/Providers/EventServiceProvider.php
    	* projected $listen = [ 
            ...,
            'App\Events\Subsc\SubscCreatedEvent' => [ 'App\Listeners\Subsc\SubscCreatedEventListener', ],
            ...
        ];
	* php artisan event:generate
		* 이벤트와 리스너를 생성
* app/Events/Subsc/SubscCreatedEvent.php
	* public function __construct(Subsc $subsc)
		* $this->subsc = $subsc;
			* 이벤트 호출자에게서 subsc 인스턴스를 전달받아 보관
* app/Listeners/Subsc/SubscCreatedEventListener.php
	* public function handle(SubscCreatedEvent $event)
		* 내부에 subsc 인스턴스를 포함한 이벤트를 수신
* 옵서버 생성
    * php artisan make:observer Subsc/SubscObserver --model=Models/Subsc/Subsc
    * app/Observers/Subsc/SubscObserver.php
        * public function created(Subsc $subsc)
            * event(new SubscCreatedEvent($subsc));
* 옵서버 등록
    * app/Providers/AppServiceProvider.php
        * public boot()
            * \App\Models\Subsc\Subsc::observe(\App\Observers\Subsc\SubscObserver::class);
* 참고: 옵서버 메소드: https://www.larashout.com/how-to-use-laravel-model-observers
    * retrieved : after a record has been retrieved.
    * creating : before a record has been created.
    * created : after a record has been created.
    * updating : before a record is updated.
    * updated : after a record has been updated.
    * saving : before a record is saved (either created or updated).
    * saved : after a record has been saved (either created or updated).
    * deleting : before a record is deleted or soft-deleted.
    * deleted : after a record has been deleted or soft-deleted.
    * restoring : before a soft-deleted record is going to be restored.
    * restored : after a soft-deleted record has been restored. 

* queue(데이터베이스)
    * 설정
        * .env 혹은 config/queue.php 파일 편집
            * QUEUE_CONNECTION 값을 sync 에서 database 로
        * php artisan queue:table && php artisan migrate
    * listener 에 ShouldQueue 구현
    * php artisan queue:work --sleep=3 --tries=3