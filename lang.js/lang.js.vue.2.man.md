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
    * 반복
        * <ul> <li v-for="(v) in ['foo', 'bar']" v-bind:key="v">{{v}}</li> </ul>
        * <ul> <li v-for="(v, k) in ['foo', 'bar']" v-bind:key="k">{{k}} | {{v}}</li> </ul>
        * <ul> <li v-for="(v) in [{'foo': 'foo'}, {'foo': 'bar'}]" v-bind:key="v.foo">{{v.foo}}</li> </ul>
    * 이벤트: v-on
        * <input type="number" v-on:input="foo.ctr = $event.target.value" v-bind:value="foo.ctr" /> <span>{{ foo.ctr }}</span>
        * <input type="number" v-on:change="foo.ctr = $event.target.value" v-bind:value="foo.ctr" /> <span>{{ foo.ctr }}</span>
        * 생략표기: 'v-on:'을 '@'으로: <button @click="foo.ctr++" :disabled="isBar">foo</button>
    * 폼 입력 바인딩: v-model: 양방향 데이터 바인딩
        * 

## component

## hook(lifecycle)

## event

## route


# DATA

## mixin

## store


