* https://laravel.kr/docs/5.7ers


* abort(): app()->abort()
	* abort_if()
	* abort_unless()
* action(): app('url')->action()
* app(): Container::getInstance()
* app_path(): app('path')
* asset(): app('url')->asset()
* auth(): app(AuthFactory::class)
* back(): app('redirect')->back()
* base_path(): app()->basePath()
* bcrypt(): app('hash')->driver('bcrypt')->make()
* broadcast(): app(BroadcastFactory::class)->event(플래시 메시지 컴포넌트: composer require "laracasts/flash")
* cache(): app('cache')
* config(): app('config')
* config_path(): app()->make('path.config')
* cookie(): app(CookieFactory::class)
* csrf_field(): HtmlString(... csrf_token() ...)
* csrf_token(): app('session')->token()
* database_path(): app()->databasePath()
* decrypt(): app('encrypter')->decrypt($value)
* dispatch(): new PendingDispatch()
* dispatch_now(): app(Dispatcher::class)->dispatchNow()
* elixir()
* encrypt(): app('encrypter')->encrypt()
* event(): app('events')->dispatch()
* factory(): app(EloquentFactory::class)->of()
* info(): app('log')->info()
* logger(): app('log')->debug()
* logs(): app('log')
* method_field(): HtmlString(... $method ...)
* mix()
* now(): Carbon::now()
* old(): app('request')->old()
* policy(): app(Gate::class)->getPolicyFor()
* public_path(): app()->make('path.public')
* redirect(): app('redirect')
* report(): app(ExceptionHandler::class)->report()
* request(): app('request')
* rescue()
* resolve()
* resource_path(): app()->resourcePath()
* response(): app(ResponseFactory::class)
* route(): app('url')->route()
* secure_asset()
* secure_url()
* session(): app('session')
* storage_path(): app('path.storage')
* today(): Carbon::today()
* trans(): app('translator')
	* trans_choice(): app('translator')->transChoice()
	* __: app('translator')->getFromJson()
* url(): app(UrlGenerator::class)
* validator(): app(ValidationFactory::class)
* view(): app(ViewFactory::class)

