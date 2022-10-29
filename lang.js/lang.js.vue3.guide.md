## 마이그레이션
* https://v3.ko.vuejs.org/guide/migration/introduction.html
* filter
	* 삭제됨, method 혹은 computed 로 대체
* fragment
* app
	* import { createApp } from 'vue'; const app = createApp({})
* v-model
	* 명칭 변경
		* prop: value => modelValue
		* event: input => update:modelValue
	* .sync, model 제거
		* v-model 로 대체
	* 다중 v-model 바인딩 가능
	* <Foo v-model:foo="bar" @update:foo="bar = $event" />
* v-if 우선순위가 v-for 에 우선


# https://v3.ko.vuejs.org/guide


##
* computed
	* getter, setter
* 리스트 렌더링
	* 배열 변경 감지
		* 변이(래핑된) 메소드: push, pop, shift, unshift, splice, sort, reverse
		* 배열 교체: filter concat, slice
* 폼 입력 바인딩: https://v3.ko.vuejs.org/guide/forms.html
	* v-model
		* text, textarea: value 속성, input 이벤트
		* checkbox, radio: checked 속성, change 이벤트
		* select: value 를 prop 로, change 이벤트
		* 수식어
			* .lazy: input 이벤트 대신 change 이벤트 이후 동기화
			* .number: 숫자 형변환
			* .trim: 앞뒤 공백 제거

## 컴포넌트
* 동적 컴포넌트
	* <component :is="foo" />
		* 이미 등록된 컴포넌트 이름
* 다중 v-model 바인딩
	* <foo v-model:bar="bar" v-model:bee="bee" />
* provide, inject
* 동적 & 비동기 컴포넌트
	* 캐시, 렌더링되지 않은 경우에도 상태 유지
		* <keep-alive><component :is="foo" /></keep-alive>
	* 비동기
		* import { defineAsyncComponent } from 'vue'
		* const foo = defineAsyncComponent(() => import('./bar.vue'))
	* suspense