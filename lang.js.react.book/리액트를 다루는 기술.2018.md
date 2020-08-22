* https://github.com/velopert/learning-react

## 목차
```
1. 리액트 시작
2. JSX
3. 컴포넌트
4. 이벤트 핸들링
5. ref: DOM에 이름 달기
6. 컴포넌트 반복
7. 컴포넌트의 라이프사이클 메서드
8. 함수형 컴포넌트
9. 컴포넌트 스타일링
10. 일정 관리 웹 애플리케이션 생성
11. 컴포넌트 리렌더링 최적화
12. 리덕스 개념 이해
13. 리덕스로 리액트 애플리케이션 상태 관리
14. 리덕스, 더 편하게 사용
15. 리덕스 미들웨어와 외부 데이터 연동
16. react-router로 SPA 개발
17. 코드 스플리팅
18. 백엔드 프로그래밍: Node.js의 Koa 프레임워크
19. mongoose를 이용한 MongoDB 연동 실습
20. 블로그 프로젝트
21. 프로젝트에서 API 연동
22. 프로젝트 마무리 작업
23. 그다음은?
```

## 1. 리액트 시작
* 설치: nvm, node, yarn
* IDE plugin: reactjs code snippets: webstorm 에서 rcc 타이핑으로 컴포넌트 스니핏 호출
* create-react-app: yarn global add create-react-app OR npm install -g create-react-app
* 프로젝트 생성: create-react-app r1

## 2. JSX
* if 대신 조건부 연산자: { (condition) ? foo : bar }; { (condition) && foo }
* 인라인 스타일링, css import

## 3. 컴포넌트
* props: 컴포넌트 자신에게는 읽기 전용
	* ```<Foo bar="value" />, <Foo bar={value}>```
	* { this.props.bar }
	* static defaultProps = { bar: value, };
	* 검증: static propTypes = { bar: PropTypes.number.isRequired, };
	    * npm install prop-types
* state: 컴포넌트 내부에서 쓰기 가능
	* 항상 기본값 설정: constructor(props) { super(props); this.state = { foo: value, ... } }
		{ this.state.foo }
	* 항상 this.setState() 로만 값 변경
		* ```<button onClick={() => { this.setState({ foo: this.state.foo + 1 }) } }>add</button>```

## 4. 이벤트 핸들링
* 이벤트 이름은 camelCase, 이벤트에 코드가 아닌 함수 형태 값 전달, DOM 요소에만 이벤터 설정 가능
* 이벤트 종류: https://reactjs.org/docs/events.html
* onChange, onClick, onKeyPress 예제
	* form
	```
	<input ... value={this.state.foo} onChange={this.handleChange} onKeyPress={this.handleKeyPress} />
	<button onClick={this.handleClick}>RESET</button>
	```
	* function: constructor 에서 바인딩하지 않으려면 화살표 표기
	```
	state = { foo: '', };
	handleChange = (e) => { this.setState({ [e.target.name]: e.target.value }) }
	handleClick = () => { this.setState({ foo: '', }); };
	handleKeyPress = (e) => { if(e.key === 'Enter') { this.handleClick(); } }
	```

## 5. ref: DOM에 이름 달기
* ref: DOM 을 직접 건드려야 할 때 사용: 일반적으로 react 는 DOM 에 직접 접근하지 않고 state 활용
* DOM 사용 상황: 특정 input에 포커스, 스크롤 박스 조작, Canvas 요소 그림 그리기
	* input 포커스
	```
	<input ref={(ref) => {this.input=ref}} ... />
	<button onClick={this.handleButtonClick}>validate</button>
	----
	handleButtonClick () => { this.setState({ ... }); this.input.focus(); }
	```
	* 스크롤 박스 조작: 컴포넌트에 ref 달고 내부 메소드 호출
	```
	<Ch5Scroll ref={(ref) => this.scrollBox=ref}/>
	<button onClick={() => this.scrollBox.scrollToBottom()}>toBottom</button>
	----
	scrollToBottom = () => { ... }
	```

## 6. 컴포넌트 반복
* map(), filter(): 반복, 추가, 제거
	```
	state = { name = ''; names = ['a', 'b', 'c']; }
	handleChange = (e) => { this.setState({ name: e.target.value }); };
	handleInsert = () => { this.setState({ name: '', names: this.state.names.concat(this.state.name) }); };
	handleRemove = (index) => { const { names } = this.state; this.setState({ names: names.filter((item, i) => i !== index) }); }
	----		
	const nameList =this.state.names.map((name, index) => (<li key={index} onDoubleClick={() => this.handleRemove(index)}>{name}</li>));
	<input onChange={this.handleChange} value={this.state.name} />
	<button onClick={this.handleInsert}>insert</button>
	<ul>{nameList.reverse()}</ul>
	```

## 7. 컴포넌트의 라이프사이클 메서드
* 마운트: 페이지에 컴포넌트 표시. 컴포넌트 만들기
	* constructor: 초기 state 설정 가능
	* getDerivedStateFromProps: props 값을 state 에 동기화
	* render: state 변경 불가. DOM 접근/변화 불가
	* componentDidMount: 컴포넌트 표시 후 호출. DOM 접근/변화 가능. 다른 js 작업 처리
* 업데이트: 컴포넌트 정보 업데이트, 리렌더링
	* 경우: props 변경시, state 변경시, 부모 컴포넌트 리렌더링시, this.forceUpdate 로 강제 렌더링 트리거시
	* getDerivedStateFromProps
	* shouldComponentUpdate: 리렌더링 여부 결정. 반드시 true 혹은 false. props, state 접근 가능
	* render
	* getSnapshotBeforeUpdate: 변화를 DOM 반영 직전
	* componentDidUpdate: DOM 처리 가능
* 언마운트: 페이지에서 컴포넌트가 사라짐
	* componentWillUnmount: 사라지기 전 호출. componentDidMount 에서 등록한 이벤트, 타이머, DOM 등 제거 처리
* 151p 그림 7-9

## 8. 함수형 컴포넌트
* 라이프사이클과 state 를 사용할 필요 없고 props만 받아 렌더링할 경우 사용
	```
	function Foo(props) { return (<div>{props.name}</div>) }
	export default Foo;
	```

## 9. 컴포넌트 스타일링
* https://velog.io/@velopert/create-react-app-v2
* css module
	* create-react-app v2의 경우: npm install classnames
	* deprecated: ~~yarn eject, yarn install, edit config/webpack.config.dev.js~~
* Sass, 변수, 믹스인
	* create-react-app v2의 경우: npm install node-sass
	* deprecated: ~~yarn add node-sass sass-loader, edit config/webpack.config.dev.js~~
	    * npm install include-media open-color
* styled-components
	* yarn add styled-components

## 10. 일정 관리 웹 애플리케이션 생성
* react add on
* e.stopPropagation();

## 11. 컴포넌트 리렌더링 최적화
* 가상 DOM 불필요 렌더링을 shouldComponentUpdate 에서 방지 
* 경우: 리스트 컴포넌트, 리스트 내부 아이템 컴포넌트, 개수 많은 하위 컴포넌트

## 12. 리덕스 개념 이해

## 13. 리덕스로 리액트 애플리케이션 상태 관리
* yarn add redux react-redux
	* yarn add prop-types

* redux devTools(firefox plugin)
	* const store = createStore(reducers, window.devToolsExtension && window.devToolsExtension());

## 14. 리덕스, 더 편하게 사용
* immutable Map: 객체 대신
    * const { Map } = Immutable; const data = Map({a:1, b:2});
    * const { Map, fromJS } = Immutable; const data = fromJS({a:1, b:2, c:{d:4, e:5}});
    * 값 조회: data.get('a'); data.getIn(['c', 'd']);
    * 값 설정: data.set('a', 4); data.setIn(['c', 'd'], 10);
        * 여러 값 동시 설정: const newData = data.mergeIn(['c'], {d:10, e:10});
            * const newData = data.merge({a:10, b:10});
    * 일반 객체로: const deserial = data.toJS();
* immutable List: 배열 대신
    * const { List } = Immutable; const list = List([0,1,2]);
    * const { List, Map, fromJS } = Immutable; const List = fromJS([ {a:1}, {b:2} ]);
    * 값 조회: list.get(0); list.getIn([0, 'v']);
    * 값 설정: const newList = list.set(0, Map({value: 10})); const newList = list.setIn([0, 'value'], 10);
        * const newList = list.update(0, item = > item.set('value', item.get('value') * 5));
    * 아이템 추가: const newList = list.push(Map({value: 3})); const newList = list.unshift(Map({value: 0}));
    * 아이템 제거: const newList = list.delete(1); const newList = list.pop();
    * 크기, 비어 있음 확인: list.size; list.isEmpty();
    * 일반 객체로: const array = list.toJS();
* npm install redux-actions immutable

## 15. 리덕스 미들웨어와 외부 데이터 연동
* 
* npm install redux-thunk
	* npm install node-gyp
* npm install redux-promise-middleware
* npm install redux-pender

## 16. react-router로 SPA 개발

## 17. 코드 스플리팅

## 18. 백엔드 프로그래밍: Node.js의 Koa 프레임워크

## 19. mongoose를 이용한 MongoDB 연동 실습

## 20. 블로그 프로젝트

## 21. 프로젝트에서 API 연동

## 22. 프로젝트 마무리 작업

## 23. 그다음은?

