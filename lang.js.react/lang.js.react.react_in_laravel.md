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

## es6
* 화살표 함수 등 사용
	* npm install --save-dev babel-plugin-transform-class-properties
	* .babelrc 파일 생성
	```
    {
    	"presets": [
    		"@babel/preset-react"
    	],
    	"plugins": [
    		"babel-plugin-transform-class-properties"
    	]
    }
    ```
	    
## laravel view 연계
* views/bar.blade.php 생성
```
<html>
	<head>
		<meta name="csrf-token" content="{{ csrf_token() }}">
		<script src="{{ asset('js/app.js') }}" defer></script>
	</head>
	<body> <div id="bar_react"></div> </body>
</html>
```
* resources/assets/js/Components/Bar/Bar.js 생성
``` 
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

class Bar extends Component {
	render() {
		return (
			<div>
				react
			</div>
		);
	}
}

export default Bar;

ReactDOM.render(<Bar/>, document.getElementById('bar_react'));
```
* resources/assets/js/app.js 편집: ``` require('./components/Bar/Bar'); ```
* js require 파일 설정: public/mix-manifest.json