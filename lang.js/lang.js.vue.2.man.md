# CONFIG

## vue-cli
* install: npm i -g @vue/cli
* init: vue create foo
* plugin
    * install: vue add foo
    * router, vuex

## build
* npm run serve
* npm run build

## config
* package.json
    * console on: "eslintConfig": { ..., "rules": { "no-console": "off" }, ... }
    * no-unused-vars off: "eslintConfig": { ..., "rules": { "no-unused-vars": "off" }, ... }

## structure

## entry point
* main.js
* App.vue


# COMPONENT

## data
* data: 객체 or 함수 값, UI 상태, 변경시 리렌더링, 템플릿에서 참조
    * data: () => ({ ctr: 0 }); created () { this.ctr++; }, <div>{{ctr}}</div>
* computed: 함수로 구현, 참조는 속성처럼, this로 참조, 캐시
    * computed: { foo: function() { return this.v1 + this.v2; } }
        * data: () => ({ v1: 1, v2: 2, });
* method
    * methods: { bar: function($event, foo) { console.log($event); console.log(foo); } }
        * <button @click="bar($event, 'foo')" >bar</button>

## display 
* template
    * mustache: {{ foo }}
    * directive: <div v-bind:attr></div>
* filter
    * filters: { f1: () => (), f2: () => (), }
        * <div>{{ foo | f1 | f2 }}</div>
* directive
    * 분기
        * <p v-if="isFoo">foo</p>: dom 구현
        * <p v-show="isFoo">foo</p>: display 속성 변경
    * 스타일
        * <p v-bind:class="{foo: isFoo, bar: isBar}">foo</p>
        * <p v-bind:class="{foo: !(isBar)}">foo</p>
        * <p v-bind:class="foo">foo</p>
            * computed: { foo: function() { return { c1: this.$data.isBar, c2: this.$data.isBar } } }
        * <p v-bind:style="{color: 'green'}">foo</p>
        * <p v-bind:style="{border: (isBar ? '1px solid red' : ''), color: 'red'}">foo</p>
        * <p v-bind:style="foo">foo</p>
            * computed: { foo: function() { return { border: (this.isBar) ? '1px solid green' : '', color: 'green' } } }
        * 생략표기: 'v-bind:' 를 ':'로: <button :disabled="isBar">foo</button>
    * 반복
        * <ul> <li v-for="(v) in ['foo', 'bar']" v-bind:key="v">{{v}}</li> </ul>
        * <ul> <li v-for="(v, k) in ['foo', 'bar']" v-bind:key="k">{{k}} | {{v}}</li> </ul>
        * <ul> <li v-for="(v) in [{'foo': 'foo'}, {'foo': 'bar'}]" v-bind:key="v.foo">{{v.foo}}</li> </ul>
    * 이벤트: v-on
        * <input type="number" v-on:input="foo.ctr = $event.target.value" v-bind:value="foo.ctr" /> <span>{{ foo.ctr }}</span>
        * <input type="number" v-on:change="foo.ctr = $event.target.value" v-bind:value="foo.ctr" /> <span>{{ foo.ctr }}</span>
        * 생략표기: 'v-on:'을 '@'으로: <button @click="foo.ctr++">foo</button>
    * 폼 입력 바인딩: v-model: 양방향 데이터 바인딩
        * <input type="number" v-model="foo.ctr" min="0" />
        * <ul> <li v-for="(v) in foo.items" v-bind:key="v.k"> <input type="text" v-model="v.k" /> | {{ v.k }} </li> </ul>
            * data: () => ({ foo: { items: [{'k':'v1'}, {'k':'v2'}] } });

## hook(lifecycle)
    * beforeCreate() {}, created() {}, beforeMount() {}, mounted() {}, beforeUpdate() {}, updated() {}, beforeDestroy() {}, destroyed() {}
    * created: dom 미연결, vuex 미사용시 api, 타이머 등
    * mounted: dom 조작 및 이벤트 리스너
    * beforeDestroy: mounted 에서 등록한 것들 뒷정리

## component
* event
    * 부모-자식 간 데이터 전달: props
        * 부모: <ComponentChild v-bind:foo="foo" v-bind:bar="bar"></ComponentChild>
            * data: () => ({ foo: 'foo', bar: [ { k: 1 }, { k: 2 } ], })
        * 자식: props: { foo: { type: String, default: 'foo', required: true, validator: () => true, }, bar: { type: Array, }
            * <div>{{ foo }}</div> <ul><li v-for="(v) in bar" v-bind:key="v.k">{{v.k}}</li></ul>
    * 자식-부모 간 데이터 전달: on(리스닝), emit(트리거)
        * 자식: <input type="text" @input="fooChild = $event.target.value" :value="fooChild" /> | <button v-on:click="setFoo">setFoo</button>
            * data: () => ({ fooChild: '' }), props: { foo: {} }, methods: { setFoo() { this.$emit('setFoo', this.fooChild); } }
        * 부모: <ComponentChild v-bind:foo="foo" v-on:setFoo="setFoo"></ComponentChild><div>{{ foo }}</div>
            * data: () => ({ foo: 'foo', }), methods: { setFoo(v) { this.foo = v; } }

## route
* router/index.js, main.js, App.vue
* <router-link to="/foo">foo</router-link> <router-view>
* <button @click="foo">foo</button>
    * methods: { foo() { router.push({ name: 'Foo', params: { bar: 'bar' } }); }, },
* hook
    * 전역: router/index.js
        * router.afterEach((to, from) => {});
        * router.beforeEach((to, from) => { if(to.path === '/foo') next('/bar'); else next(); });
    * 라우트단위: const routes = [... { beforeEnter: (to, from, next) => { next(); }, component: Foo, path: '/foo', } ...];
    * 컴포넌트 내부
        * beforeRouteEnter: (to, from, next) => { console.log(to, from); next(vm => { vm.foo(); }); }, methods: { foo() {}; }
        * beforeRouteLeave: (to, from, next) => { next(); }
        * beforeRouteUpdate: (to, from, next) => { next(); }

# DATA

## mixin

## store


