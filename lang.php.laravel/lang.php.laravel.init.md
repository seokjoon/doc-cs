# 라라벨 실행환경 초기화

## 신규 생성하는 경우
* composer create-project laravel/laravel foo --prefer-dist --verbose

## 기존 git 저장소에서 clone 하는 경우
* git clone https://github.com/foo/bar.git bar
* 설정 파일 생성: cp .env.example .env
* 의존성 설치: composer install
* 암호화 키: php artisan key:generate
* db 마이스레이션 및 시딩: php artisan migrate --seed --force

## 설정
* 설정 파일 편집: vi .env
* 퍼미션
	* chown -R www-data:www-data storage bootstrap/cache
	* chmod -R 775 storage bootstrap/cache
* git 공유 제외 설정: .gitignore


## requirement: wsl ubuntu 22.04
* apt-get update && apt-get -y install \
	php8.3-cli \
	php8.3-mysql mysql-client \
	php8.3-bcmath php8.3-curl php8.3-gd php8.3-mbstring php8.3-zip php8.3-xml \
	php8.3-redis
* curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer
