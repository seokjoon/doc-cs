## URL
* https://github.com/chiraggude/awesome-laravel

## composer
* api: appkr/api
	* ApiServiceProvider::class
* api: dingo/api
* cors: barryvdh/laravel-cors
	* CORS: 클라이언트 Origin 요청 헤더 검사, Access-Control-* 응답 헤더 추가: 미들웨어 적용
	* ServiceProvider::class
* dbal: doctrine/dbal
	* users.password 컬럼 null 허용 마이그레이션 필요 컴포넌트
* debugbar: barryvdh/laravel-debugbar
	* 라라벨 디버그 바
	* ServiceProvider::class
* envoy: laravel/envoy
	* 원격 서버 작업 자동화 도구
	* echo 'export PATH="$PATH:$HOME/.composer/vendor/bin" >> ~/YOUR_SHELL_PROFILE'
* flash: laracasts/flash
	* 플래시 메시지 컴포넌트
	* FlashServiceProvider::class, Flash::class
* guzzlehttp: guzzlehttp/guzzle
	* http client
* intervention image: intervention/image
	* 인터벤션 이미지 컴포넌트(웹 서버 루트 외부 이미지를 컨트롤러에서 반환)
	* ImageServiceProvider::class, Image::class
* jwt: tymon/jwt-auth
	* jwt(json web token) 인증
	* JWTAuthServiceProvider::class, JWTAuth::class, JWTFactory::class
* oauth: composer require league/oauth2-server
	* Oauth 인증
* parsedown-extra: erusev/parsedown-extra
	* 마크다운
* slack: maknz/slack
	* 슬랙 메시지 전송
* 난독화(리소스 아이디): jenssegers/optimus

## etc
* admin: https://github.com/z-song/laravel-admin
* admin lte: https://github.com/acacha/adminlte-laravel
* admin voyager: https://github.com/the-control-group/voyager
* awesome: https://github.com/chiraggude/awesome-laravel
* example: https://github.com/bestmomo/laravel5-example
* excel: https://github.com/Maatwebsite/Laravel-Excel
* generator: https://github.com/InfyOmLabs/laravel-generator
* generator boilerplate: https://github.com/rappasoft/laravel-5-boilerplate
* pdf dom: https://github.com/barryvdh/laravel-dompdf
* permission: https://github.com/spatie/laravel-permission
* permission entrust: https://github.com/Zizaco/entrust
* scrum gitscrum: https://github.com/gitscrum-community/laravel-gitscrum
* shopping cart: https://github.com/Crinsane/LaravelShoppingcart
* table(UI data): https://github.com/yajra/laravel-datatables