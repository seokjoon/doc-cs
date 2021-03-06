## PART 2 자바스크립트 기초 다지기
* 029 객체 이해하기 ②(속성 접근/추가/수정/삭제)
* 030 ES6의 향상된 객체 문법 알아보기 - 단축 속성명
* 031 ES6의 향상된 객체 문법 알아보기 - 속성 계산명
* 032 ES6의 향상된 객체 문법 알아보기 - 비구조화 할당
* 047 화살표 함수 이해하기
* 052 클래스 상속 이해하기
* 053 클래스 정적 메소드와 속성 정의하기
* 056 모듈 시스템 이해하기
* 057 모듈 기본값 정의하고 가져오기: export function foo(bar) {}; import {foo} from './foo.js'; foo('bar');
* 058 모듈을 여러 이름으로 내보내고 가져오기
* 059 모듈을 다양한 방식으로 사용하기


## PART 3 자바스크립트 실력 다지기
* 060 표준 내장 객체 이해하기: Object, Number, String, Array, Math, Date, JSON, RegExp, Map, Set, ...
* 061 자료형 확인하기: typeof func === "function"; obj instanceof Object;
* 062 NaN 값 확인하기: Number.isNaN()
* 063 정수 확인하기: Number.isInteger()
* 064 배열 자료형 확인하기: Array.isArray()
* 065 문자열을 숫자형 정수로 변환하기: parseInt()
* 066 실수형 숫자로 변환하기: parseFloat()
* 067 문자열 양 끝의 공백/탭/줄바꿈 없애기: foo = bar.trim()
* 068 문자열 자르기 1: foo = bar.slice(start, stop)
* 069 문자열 자르기 2: foo = bar.substring(start, stop)
* 070 문자열 자르기 3: foo = bar.substr(start, length)
* 071 문자열 길이 구하기: foo.length()
* 072 문자열로 변환하기: 모든 객체: foo.toString()
* 074 특정 위치의 문자 반환하기: foo.charAt(index)
* 075 특정 문자열 위치 확인하기 1: 위치 인덱스 혹은 -1 반환: foo.indexOf('bar')
* 076 특정 문자열 위치 확인하기 2: 뒤에서부터 확인: foo.lastIndexOf('bar')
* 077 특정 문자열 포함 여부 확인하기: foo.includes('bar') 
* 078 문자열 대소문자 변환하기: foo.toLowerCase(), foo.toUpperCase()
* 079 배열 요소를 분할/변환하기: 문자열을 배열로: foo = Array.from(bar)
* 080 문자열을 특정 구분자에 의해 배열로 나누기: foo = bar.split(',')
* 081 배열 뒤에 요소 추가하기: foo.push('bar')
* 082 배열 앞에 요소 추가하기: foo.unshift('bar')
* 083 배열 길이 구하기: foo.length()
* 084 배열 합치기: foo1.concat(foo2, foo3, foo4)
* 085 배열에 특정 구분자 넣어 문자형으로 변환하기: foo.join('\n')
* 086 배열 마지막 요소 추출하기: foo.pop()
* 087 배열 맨 앞 요소 추출하기: foo.shift()
* 088 배열 특정 위치의 요소 추출하기: foo = bar.slice(start, stop)
* 089 배열 인덱스로 특정 요소 수정하기: foo.splice(start, countRemove, add1, add2, add3)
* 090 배열의 특정 요소 위치 확인하기: foo.indexOf(bar)
* 091 배열 순환하기: foo.forEach(callback)
* 092 배열 정렬하기: foo.sort()
* 093 배열의 순서를 반대로 나열하기: foo.reverse()
* 094 배열 요소가 특정 조건을 만족하는지 확인하기: true 반환 시점에 종료: foo.some(bar => bar > 1)
* 095 모든 배열 요소가 특정 조건을 만족하는지 확인하기: false 반환 시점에 종료: foo.every(bar => bar.attr === 1)
* 096 배열의 특정 조건을 기준으로 필터링하기: foo = bar.filter(a => a < 1)
* 097 배열의 특정 조건을 충족하는 요소 찾기: 콜백의 리턴값은 bool이어야 함: true인 첫 요소 반환: foo = bar.find(a => a === 1)
* 098 배열 요소 일괄 변경하기: foo = bar.map(a => a.b)
* 099 배열 내 값을 누적시키기: reduce
* 100 중첩된 배열을 단일하게 만들기: 다차원 배열을 일차원 배열로: foo = bar.reduce((a, b) => { return a.concat(b) }, [])
* 101 객체에서 키만 추출하기: foo = Object.keys(bar)
* 102 객체에서 값만 추출하기: foo = Object.values(bar)
* 103 객체를 배열로 변환하기: foo = Object.entries(bar)
* 104 객체 변경되지 않도록 하기: foo = Object.freeze(bar)
* 105 객체에 속성 추가 못하게 만들기: foo = Object.seal(bar)
* 106 객체 병합 확장하기: foo = Object.assign({}, a, b)
* 107 진수 변환하기: toString
* 108 10진수 아닌 진법을 다른 진법으로 변환하기: parseInt
* 109 랜덤값 구하기: foo = Math.floor(Math.random() * range)
* 110 특정 자리수에서 반올림하기: Math.round(foo)
* 111 특정 자리수에서 올림하기: Math.ceil(foo)
* 112 특정 자리수에서 내림하기: Math.floor(foo)
* 113 현재 시간을 원하는 포맷으로 출력하기: new Date().getFullYear(), getMonth(), getDate();
	* Date.prototype.yyyymmdd = function() {}
* 114 UTC 기준 날짜 출력하기: DateUTC
* 115 두 개의 날짜 사이의 경과 시간 계산하기
* 116 JSON을 문자열로 변환하기: JSON.stringify(foo)
* 117 JSON 문자열을 JSON으로 변환하기: JSON.parse(foo)
* 118 정규표현식으로 대응되는 문자열 위치 확인하기: 첫번째 일치값 반환: foo = bar.search(regex)
* 119 정규표현식으로 문자열 확인하기: 정규식에 g 플래그 없는 경우 추가 정보 포함 반환: foo = bar.match(regex)
* 120 정규표현식으로 특정 문자의 포함 여부 확인하기: bool 리턴: foo = regex.test(bar)
* 121 정규표현식으로 문자열 변환하기: 일치값 배열로 반환, 없으면 null 반환: foo = regex.exec(bar)
* 122 정규표현식으로 문자열 치환하기: foo = bar.replace(교체 대상 문자열 혹은 정규식, 대체될 문자열 또는 함수)
* 123 반복 가능한 객체와 반복자 이해하기
* 124 문자열 순환하기: for-of: for(const foo of bar) {}
* 125 배열 순환하기: for-of: for(const foo of bar) {}
* 126 Map 객체에 요소 추가/삭제/확인하기: new Map().set(foo, bar), get(foo), delete(foo), has(foo)
* 127 Map 객체의 크기 확인하기: 함수가 아닌 속성: new Map().size
* 128 Map 객체 요소 나열하기: new Map().keys(), values(), entries(): 
* 129 Map 객체 순환하기 1: for-of, foreach: for(let [k,v] of foo.entries()) {}, foo.forEach((v,k) => {})
* 130 Map 객체 순환하기 2: for(let [func,v] of map) { func(v) }
* 131 Set 객체의 값 추가/삭제/확인하기: new Set().add(foo), delete(foo), has(foo)
* 132 Set 객체의 크기 확인하기: new Set().size
* 133 Set 객체로 Array 중복 요소 없애기: const foo = new Set(bar); console.log([...foo])
* 134 Set 객체 값 나열하기: new Set().keys(), values(), entries()
* 135 Set 객체 순환하기: for-of, foreach: for(let k of foo.keys()) {}; for(let v of foo.values()) {}; for(let [k,v] of foo.entries()) {}; foo.forEach(v,k) => {}
* 136 일정 시간 후에 코드 실행하기: setTimeout(function() {}, 1000)
* 137 일정 시간마다 코드 실행하기: setInterval(() => {}, 1000)
* 138 Promise 이해하기
	* pm = new Promise((resolve, reject) => { ...; resolve({ foo: bar }); reject(new Error(foo) });
	* pm.then(res => {}).catch(err => {});
* 139 Promise 조합하기
	* function foo(bar) { return new Promise(resolve, reject) { setTimeout(() => {}); }); };
	* foo(a, b).then().then().then().catch();
* 140 Async 이해하기
	* function foo(a,b) { return new Promise(() => {}); }; 
	* const bar = async function() { try { let v = await foo(a,b); } catch(e){} }
	* bar();


## PART 4 자바스크립트 응용 다지기


## PART 5 자바스크립트 프로그래밍 작성
