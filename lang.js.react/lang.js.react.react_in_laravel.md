# 라라벨에서 리액트 사용하기

## 참고
* https://laravel.kr/docs/5.7/frontend
* https://laravel.kr/docs/5.7/mix
* https://github.com/appkr/l5code/issues/11

## laravel 통합
* laravel에서 react 스캐폴딩 사용
	* php artisan preset react
* 의존성 설치
	* npm install
* 빌드
	* npm run dev
* 모니터링
	* npm run watch

## 기타
* 화살표 함수 등 사용
	* npm install --save-dev babel-plugin-transform-class-properties
	* .babelrc 파일 생성
		```
		{
		  "presets": [
		    "react"
		  ],
		  "plugins": [
		    "babel-plugin-transform-class-properties"
		  ]
		}
		```