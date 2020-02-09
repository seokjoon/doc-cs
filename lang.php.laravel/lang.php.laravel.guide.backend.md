# 라라벨 백엔드 가이드

## 목차
* 엔티티 및 구성요소


## 엔티티
    

## 구성요소
* 엔티티: worker(작업자), agent(의뢰자), job(작업)
    * job-worker: 다대일
    * agent-worker: 다대다
* Controller, Model, Resource  
* DB Factory/Migration/Seeder
* Eloquent ORM/Relationship, Query Builder
* Event, Listener, Notification, Observer, Queue
* Policy
* Middleware, Provider


## Controller, Model, Resource
* 목록과 항목의 CRUD를 위한 컨트롤러/모델
    * php artisan make:controller Api/v1/Work/WorkersController --api --model=Models/Worker/Worker
    * php artisan make:controller Api/v1/Agent/AgentsController --api --model=Models/Agent/Agent
    * php artisan make:controller Api/v1/Job/JobsController --api --model=Models/Job/Job
* index(), show(), store(), update(), delete()
* api 응답을 위한 항목 Resource, 목록 Collection
    * php artisan make:resource Work/WorkResource 
    * php artisan make:resource AgentAgentCollection 


## DB Factory/Migration/Seeder
* php artisan 
* php artisan 
* php artisan 


## Eloquent ORM/Relationship, Query Builder



## MVC
* artisan 사용 예제: https://github.com/seokjoon/doc-cs/tree/master/lang.php.laravel/lang.php.laravel.cmd.artisan.md
 
* pa make:controller Api/v1/Foo/FoosController --api --model=Models/Foo/Foo
* vi routes/api.php
* vi app/Http/Controllers/Api/v1/*
* 라라벨 사용법: 퍼블리셔: https://github.com/seokjoon/doc-cs/blob/master/lang.php.laravel/lang.php.laravel.publisher.md


## DB migrate/seed
* php artisan make:migration create_foos_table --create=foos
* php artisan migrate
    * php artisan migrate:rollback
    
* php artisan make:factory FooFactory --model=Models/Foo/Foo
* php artisan make:seeder FoosTableSeeder
* vi database/seeds/DatabaseSeeder.php
* vi database/seeds/FoosSeeder.php
* vi database/factories/FooFactory.php
* php artisan db:seed


## eloquent relationship
* https://laravel.kr/docs/6.x/eloquent-relationships

* 세부 질의: 쿼리 빌더: https://github.com/seokjoon/doc-cs/tree/master/lang.php.laravel/lang.php.laravel.db.queryBuilder.md


## API

* https://laravel.kr/docs/6.x/eloquent-resources

* app/Http/Controllers/Api/v1/FoosController.php
    * store(), update(), destroy()
* postman crud
    * get: localhost/api/v1/foos
    * post: localhost/api/v1/foos
    * put: localhost/api/v1/foos/n
    * delete: localhost/api/v1/foos/n
