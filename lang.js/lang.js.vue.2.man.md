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
    * <p v-if="isFoo">foo</p>: dom 구현
    * <p v-show="isFoo">foo</p>: display 속성 변경
    * <p b-bind:class="{foo: isFoo, bar: isBar}"></p>
    * <p b-bind:class="{error: !(isFoo)}"></p>
    * <p b-bind:class="{items}"></p>
        * computed: { items: () => ({}) }
    * <p b-bind:style=""></p>

## component

## hook(lifecycle)

## event

## route


# DATA

## mixin

## store


