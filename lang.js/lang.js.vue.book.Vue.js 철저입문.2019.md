## 01장: 프로그레시브 프레임워크 Vue.js
* 1.4 프로그레시브 프레임워크가 제공하는 단계적 영역
    * 선언적 렌더링, 컴포넌트 시스템, 클라이언트 사이드 라우팅, 대규모 상태 관리, 빌드 시스템, 클라이언트-서버 데이터 퍼시스턴스

## 02장: Vue.js의 기본 사용법
* 2.3 Vue 객체
    * 인스턴스를 변수에 대입하는 경우: ex) var vm1 = new Vue({ ... }); vm1.$watch()
* 2.4 Vue 인스턴스 마운트하기
    * Vue 인스턴스의 적용(el), 메서드를 이용한 마운트($mount 메서드)
* 2.5 UI 데이터 정의(data)
    * 2.5.1 Vue 인스턴스 확인하기
    * 2.5.2 데이터 변경 탐지하기: $watch(모니터링 대상 값 반환 함수, 값 변경시 콜백 함수);
* 2.6 템플릿 문법
    * 텍스트 전개 {{}}, 속성값 전개 v-bind:attr
* 2.7 필터
    * filters: { foo: function() {}, }
    * {{ val | foo }}, {{ val | foo | bar }}
* 2.8 계산 프로퍼티: 함수로 구현, 참조는 프로퍼티처럼, 인스턴스 내부에서는 this로 자신을 참조, 의존 데이터가 동일하다면 계산 결과를 캐시
    * computed: { foo: function() { return this.items... }, }, data: { items: ... }
* 2.9 디렉티브
    * v-if: dom 추가/제거(변경 적을때), v-show: display 속성값 변경(변경 많을때)
    * v-bind:class={foo: bool, bar: !(bool)}, v-bind:style={color: (bool ? 'green' : 'yellow'')}: 클래스와 스타일 연결
    * v-for="v in [...]" v-bind:key="v", v-for="(v, k) in [...]" v-bind:key="v": 리스트 렌더링
    * v-on:이벤트명="값 평가 표현식 혹은 메소드"
        * v-on:input="item.value = $event.target.value" v-bind:value="item.value" 
        * v-on:change="item.value = $event.target.value" v-bind:value="item.value"
        * 생략 표기: v-on:click => @click
        * 디렉티브 수정자: v-on:click.prevent
    * v-model: 폼 입력 바인딩
        * v-model="item.value"
* 2.10 생애주기 훅
    * beforeCreate, created, beforeMount, mounted, beforeUpdate, updated, beforeDestroy, destroyed
    * created: vuex 미사용시 api, 타이머 등, mounted: dom 조작 및 이벤트 리스너, beforeDestroy: mounted 에서 등록한 것들 뒷정리
* 2.11 메서드
    * methods: { foo: function($e) {}, }


## 03장: 컴포넌트의 기초
* 3.1 컴포넌트란 무엇인가?
    ```
    <div id="bar"><foo></foo></div>
    Vue.component('foo', { data: function() { return { ... } }, template: ... }); // component의 data는 function 이어야 함
    new Vue({ el: '#bar', }); // el 은 최상위 Vue 인스턴스만 추가 가능
    ```
* 3.2 Vue 컴포넌트 정의하기
    * 전역/지역 컴포넌트, 커스텀태그/하위생성자 방식
    * 분리(부모/자식), 재사용, 반복
    * 생성자 사용 컴포넌트 정의
        ```
        var foo = Vue.extend({ template: '<span>foo</span>' });
        Vue.component('foo', foo);
        ```
    * 전역 컴포넌트
        * Vue.component(tagName, options)
            * options: data, filters, methods, computed, template, props, created, ...
    * 지역 컴포넌트: 컴포넌트를 특정 Vue 인스턴스 내부에서만 사용하도록 등록, 하위생성자 컴포넌트 사용 가능
        * components: { foo: { ... } },
    * 템플릿을 만드는 그 외의 방법: text/x-template, render 함수, 단일 파일 컴포넌트, 인라인 템플릿, JSX
        * text/x-template: html 쪽으로 템플릿 분할
            ```
            <script type="text/x-template" id="foo"> ... </script>
            <div id="bar"></div>
            Vue.component('foo', { template: '#foo' });
            new Vue('#bar', { el: '#bar', template: '<foo></foo>', });
            ``` 
        * render
            * render: function(createElement) { return createElement( ... ) }
    * 컴포넌트 생애주기: Vue 인스턴스 생애주기와 유사
    * 컴포넌트 데이터: 컴포넌트의 data 속성은 함수
        * 모든 인스턴스가 공유하므로 인스턴스 간 서로 다른 데이터를 가지기 위해; data 속성에 객체로 값 지정시 경고
        * data: function() { return { foo: [ ... ], bar: { ... }, } }
* 3.3 컴포넌트 간 통신
    * 부모에서 자식으로
        ```
        <div id="comParent"><com-child v-bind:itme="item"></com-child></div>
        Vue.component('comChild', { props: { item: { ... } }, template: '<span>{{ item }}</span>', });
        new Vue({ data: { item: 'foo', }, el: '#comParent', });
        ```
        ```
        <div id="comPlural"><com-singular v-for="item in items" :key="item.title" :item="item"></com-singular>
        Vue.component('comSingular', { props: { item: { ... } }, template: '<span>{{ item.id }} | {{ item.title }}</span>', });
        new Vue({ data: { items: [ { id: 1, title: 'title 1' }, { id: 2, title: 'title 2' } ] }, el: '#comPlural', });
        ```
    * 자식에서 부모로: 커스텀 이벤트: 이벤트 리스닝 $on(eventName), $emit(eventName), v-on
        ```
   		<component-props-event-btn v-on:increment="increment()"></component-props-event-btn>
        var componentPropsEventBtn = Vue.extend({
            ...,
        	methods: { add: function () { this.counter += 1; this.$emit('increment'); }, },
        	template: '<span>{{ counter }} <button v-on:click="add">add</button></span>',
        });
        new Vue({ ..., methods: { increment: function() { this.total += 1; }, }, });
        ```
    * this.$parent, this.$children: 권고하지 않음
    * ref
    	```
    	<div id="parent"><child ref="foo"></child></div>
        var parent = new Vue({ el: '#parent' });
        var child = parent.$refs.foo;
    	```
    * 부모 네이티브 이벤트를 자식에게 전달: native 수정자
        * <foo v-on:click.native="bar"></foo>
    * 부모가 자식 이벤트를 구독: sync 수정자
* 3.4 컴포넌트 설계: slot, 단위테스트


## 04장: Vue Router를 활용한 애플리케이션 개발
* 4.1 Vue Router를 이용한 단일 페이지 애플리케이션
* 4.2 기초 라우팅
    * 4.2.1 라우터 설치하기: npm install vue-router
    * 4.2.2 라우팅 설정
        ```
        <div id=app><router-link to="/foo">foo</router-link><router-view></router-view></div>
        var router = new VueRouter({ routes: [ { path: '/foo', component: { ... } }, ] });
        new Vue({ router: router }).$mount('#app');
        ```
* 4.3 실용적인 라우팅을 구현하기 위한 기능
    * URL 파라미터, 패턴 매칭
    	* <router-link to="/foo/2">foo</router-link>
        * routes: [ { path: '/foo/:id', component: { template: '<div>foo id {{ $route.params.id }}</div>' } } ],
    * 이름 가진 라우트
   		* <router-link :to="{ name: 'foo', params: { id: 3 } }">foo</router-link>
        * routes: [ { path: '/foo/:id', name: 'foo', component: { template: '<div>foo id {{ $route.params.id }}</div>' } } ],
    * 4.3.4 router.push를 사용한 페이지 이동
    * 4.3.4 훅 함수: 전역, 라우트 단위, 컴포넌트 내
        * 전역: router.beforeEach(function(to, from, next) { if(to.path === '/foo') next('/bar'); else next(); });
        * 라우트 단위: routes: [{ path: '/foo', beforeEnter: function(to, from, next) { if(to.query.bar === '1') next('/bar'); else next() }, ..., }]
        * 컴포넌트 내: beforeRouteEnter, beforeRouteLeave 
* 4.4 예제 애플리케이션 구현하기
    * created, watch
    * callback, bind, localStorage, 
* 4.5 Vue Router의 고급 기능
    * $router 인스턴스: app, mode, currentRoute, push, replace, go, back, forward, addRoutes
    * $route 객체: path, params, query, hash, fullPath, name
    * 중첩 라우팅: [{ path: 'foo', ... children: [{ path: 'bar', ... }, { path: 'fee', ... }], }]
    * 리다이렉션: [{ path: '/foo', redirect: '/bar''}]
    * 앨리어싱: [{path: '/foo', component: bar, alias: '/fee''}]
    * 히스토리: url 해시, history api


## 05장: Vue.js의 고급 기능
* 5.1 트랜지션 애니메이션
    * 래퍼 컴포넌트: <transition></transition>
    * 클래스: v-enter, v-enter-to, v-enter-active, v-leave, v-leave-to, v-leave-active
    * 훅: v-on: before-enter, enter, after-enter, enter-cancelled, before-leave, leave, after-leave, leave-cancelled
* 5.2 슬롯
    * 단일 슬롯: var foo = { template: `<span><slot>bar default</slot></span>` }, <foo>bar insert</foo>
    * 이름을 갖는 슬롯: var foo = { <div><slot name="bar"></slot><slot></slot><slot name="fee"></fee></div> }, <foo><h2 slot="bar">bar insert</h2><p>slot default insert</slot><p slot="fee">fee insert</slot></foo>
    * 슬롯의 범위: 부모 범위에 속하므로 자식 컴포넌트 데이터에 접근하려면 v-bind 로 전달
* 5.3 사용자 정의 디렉티브
    * Vue.directive('img-fail', { bind: function(el) { el.addEventListener('error', () => { el.src = '...'; }); } }); <img v-img-fail src="./foo.png" />
    * 훅: bind, inserted, update, componentUpdated, unbind
        * 인자: el, binding(name, value, expression, arg, modifiers)
* 5.4 렌더링 함수
    * jsx: babel-plugin-transform-vue-jsx
* 5.5 믹스인
    * TODO


## 06장: 단일 파일 컴포넌트를 활용한 개발
* 필요 패키지: @vue/cli, @vue/cli-service-global
* 블록: <template></template><script> import Foo from 'foo'; export default { ... }; </script><style></style>
* 테스트: vue serve foo.vue
* css 범위: 지역 <style scoped></style>, 전역 <style></style>
* css 모듈: <style module> .foo { ... } </style>, <p :class="$style.foo"></p>


## 07장: Vuex를 이용한 데이터플로 설계 및 상태 관리
* 7.1 복잡한 상태 관리
* 7.2 데이터플로 설계
    * 7.2.1 신뢰할 수 있는 유일 정보원
    * 7.2.2 ‘상태 읽고 쓰기’를 캡슐화
    * 7.2.3 단방향 데이터플로
* 7.3 Vuex를 이용한 상태 관리
    * 7.3.1 Vuex 설치하기
* 7.4 Vuex의 주요 개념
    * 7.4.1 스토어
    * 7.4.2 스테이트
    * 7.4.3 게터
    * 7.4.4 뮤테이션
    * 7.4.5 액션
* 7.5 태스크 관리 애플리케이션의 상태 관리
    * 7.5.1 애플리케이션 요구 사항 및 준비
    * 7.5.2 태스크 목록 표시하기
    * 7.5.3 새로운 태스크 생성 및 완료 처리
    * 7.5.4 레이블 기능 구현
    * 7.5.5 레이블로 필터링하기
    * 7.5.6 로컬 스토리지에서 저장 및 복원하기
    * 7.5.7 Vuex를 사용한 애플리케이션
* 7.6 스토어를 모듈 단위로 분할하기
    * 7.6.1 namespaced 옵션을 이용한 네임스페이스 분할
* 7.7 Vuex 스토어와 Vue 컴포넌트 간의 통신
    * 7.7.1 컴포넌트에서 스토어 접근하기
    * 7.7.2 스토어에 접근하는 컴포넌트를 최대한 적게 유지하라
* 7.8 Vuex와 Vue Router 연동하기


## 08장: 중규모 및 대규모 애플리케이션 개발 1 - 개발 환경 갖추기
* 8.1 Vue.js 프로젝트의 특징
    * 8.1.1 Vue.js로 본격적인 개발을 시작하기 위한 마음가짐
* 8.2 이번 장에서 만들 애플리케이션
    * 8.2.1 애플리케이션의 주요 요구 사항
    * 8.2.2 애플리케이션의 아키텍처
* 8.3 애플리케이션 개발 환경 구축하기
    * 8.3.1 개발 환경 구축 지원 도구 Vue CLI
    * 8.3.2 자바스크립트 환경 구축과 Vue CLI
* 8.4 Vue CLI로 개발 환경 구축하기
    * 8.4.1 애플리케이션 프로젝트 생성하기
    * 8.4.2 프로젝트 구조
    * 8.4.3 태스크 명령
    * 8.4.4 애플리케이션 실행 확인
    * 8.4.5 애플리케이션의 환경 변수
* 8.5 애플리케이션 빌드
    * 8.5.1 애셋 처리
    * 8.5.2 정적 분석 도구
* 8.6 테스트 환경
    * 8.6.1 단위 테스트
    * 8.6.2 E2E 테스트
* 8.7 프런트 엔드와 백 엔드 연동
    * 8.7.1 API 프락시
    * 8.7.2 백 엔드 통합
* 8.8 개발 환경 보강하기
    * 8.8.1 Vue.js 코딩 환경 구축
    * 8.8.2 Vue.js 공식 제공 정적 분석 도구 도입
    * 8.8.3 디버깅 및 프로파일링 환경 구축
    * 8.8.4 백 엔드 API 서버 환경 구축
    * 8.8.5 상태 관리 라이브러리 도입
    * 8.8.6 HTTP 클라이언트 라이브러리 도입
    * 8.8.7 단위 테스트 유틸리티 도입
    * 8.8.8 E2E 테스트 명령 등록


## 09장: 중규모 및 대규모 애플리케이션 개발 2 - 설계
* 9.1 컴포넌트 설계
    * 9.1.1 아토믹 디자인 원칙에 따른 컴포넌트 추출
    * 9.1.2 원자
    * 9.1.3 분자
    * 9.1.4 유기체
    * 9.1.5 템플릿
* 9.2 단일 파일 컴포넌트 만들기
    * 9.2.1 디렉터리 구조 생성 및 파일 배치하기
    * 9.2.2 컴포넌트 API
    * 9.2.3 KbnButton 컴포넌트의 API
* 9.3 상태 모델링 및 데이터플로 설계
    * 9.3.1 상태 모델링
    * 9.3.2 데이터플로
    * 9.3.3 데이터플로 관련 스텁 코드 작성
    * 9.3.4 액션 스텁 코드 작성
* 9.4 라우팅 설계
    * 9.4.1 라우트 플로
    * 9.4.2 라우트 정의


## 10장: 중규모 및 대규모 애플리케이션 개발 3 - 구현
* 10.1 개발 정책 확립
    * 10.1.1 애플리케이션 구현을 시작하기 전에
* 10.2 컴포넌트 구현
    * 10.2.1 KbnButton 컴포넌트
    * 10.2.2 KbnLoginForm 컴포넌트
    * 10.2.3 KbnLoginView 컴포넌트
* 10.3 데이터플로 구현
    * 10.3.1 login 액션 핸들러
    * 10.3.2 AUTH_LOGIN 뮤테이션 핸들러
    * 10.3.3 AuthAPI 모듈
* 10.4 라우팅 구현
    * 10.4.1 beforeEach 가드를 활용한 내비게이션 가드
* 10.5 개발 서버와 디버깅
    * 10.5.1 개발 서버를 사용해 개발하기
    * 10.5.2 Vue DevTools로 디버깅하기
* 10.6 E2E 테스트
    * 10.6.1 E2E 테스트 구현하기
    * 10.6.2 테스트 실행하기
* 10.7 애플리케이션 오류 처리
    * 10.7.1 자식 컴포넌트에서 발생한 오류 처리
    * 10.7.2 전역 오류 처리
* 10.8 빌드 및 배포
    * 10.8.1 애플리케이션 빌드
    * 10.8.2 애플리케이션 배포
* 10.9 성능 측정 및 개선
    * 10.9.1 성능 측정 설정 방법
    * 10.9.2 측정 가능한 처리
    * 10.9.3 렌더링 성능 개선


## 부록A: jQuery에서 이주하기
* A.1 이주 결심하기
* A.2 jQuery로 구현된 기능을 Vue.js로 옮기기
    * A.2.1 이벤트 리스너
    * A.2.2 표시/비표시 전환하기
    * A.2.3 요소 삽입 및 삭제하기
    * A.2.4 속성값 변경하기
    * A.2.5 클래스 변경하기
    * A.2.6 스타일 변경하기
    * A.2.7 폼(사용자 입력)


## 부록B: 개발 툴
* B.1 Storybook
    * B.1.1 프로젝트에 Storybook 도입하기
    * B.1.2 Storybook 실행하기
    * B.1.3 스토리 구현하기
    * B.1.4 Storybook 공개하기
* B.2 정적 타입 언어
    * B.2.1 TypeScript
    * B.2.2 TypeScript의 예제 코드
    * B.2.3 프로젝트 설정하기
    * B.2.4 컴포넌트 구현하기
    * B.2.5 에디터
    * B.2.6 라이브러리 타입 정의


## 부록C: Nuxt.js
* C.1 Nuxt.js란?
* C.2 Nuext.js의 특징
    * C.2.1 서버 사이드 렌더링 지원
    * C.2.2 바로 개발을 시작할 수 있는 개발 환경 및 확장성
    * C.2.3 정적 HTML 파일 생성 지원
* C.3 Nuxt.js 시작하기
* C.4 Nuxt.js를 사용해 정적 사이트 만들기
    * C.4.1 화면 설계
    * C.4.2 라우팅 추가하기
    * C.4.3 전역 내비게이션 컴포넌트 추가하기
    * C.4.4 레이아웃에 전역 내비게이션 추가하기
* C.4.5 개발 서버에서 동작 확인하기
* C.4.6 정적 HTML 파일 빌드하기 