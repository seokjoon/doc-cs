# 도커 활용 가이드

## 커맨드라인 기반
* images
	* docker pull redis
	* docker pull mysql:5.7
	* docker pull seokjoon/all:ec11.1
* redis
	* docker run -d --restart unless-stopped --name redis -p 6379:6379 -v /d1/db/redis/data:/data redis redis-server --appendonly yes
* mysql
	* docker run -d --name mysql57 -e MYSQL_ROOT_PASSWORD="TEST_PW" -v /d1/db/mysql57/data:/var/lib/mysql -p 3306:3306 mysql:5.7
	* docker exec -it mysql57 bash
		* mysql -u root -p
		* alter user 'root'@'%' identified by 'REAL_PW' password expire never;
		* alter user 'root'@'localhost' identified by 'REAL_PW' password expire never;
		* flush privileges;
	* docker run -d --restart unless-stopped --name mysql57 -v /d1/db/mysql57/data:/var/lib/mysql -v /d1/db/mysql57/log:/var/log/mysql -v /etc/localtime:/etc/localtime:ro -p 3306:3306 mysql:5.7 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
* www80
	* docker run -d --restart unless-stopped --name www80 -v /d1/app/www/80:/var/www -v /d1/app/www/80/log:/var/log/nginx -v /etc/localtime:/etc/localtime:ro --link mysql57:mysql57 --link redis:redis -p 80:80 seokjoon/all:ec11.1
