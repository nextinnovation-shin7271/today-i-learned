# Vuex 상태관리 라이브러리

## 설치

```npm
npm install vuex --save
```

## Vuex의 핵심 속성

```js
import { createStore } from "vuex";

export default createStore({
  state: {},
  getters: {},
  mutations: {},
  actions: {},
  modules: {},
});
```

`store`에 있는 5가지 속성에대해 알아본다.

### state

`state`는 상태(state)의 집합이다.
Vuexㄴ는 단일 상태 트리(single state tree)를 사용하기 때문에 이 집합 내에서 현재 상태를 쉽게 찾을 수 있다.

**단일 상태 트리(single state tree)**
단일 상태 트리는 vue의 애플리케이션은 하나의 `store`만 가진다는 것을 의미한다.
하나의 `store`만 가지기 때문에 현재 state의 상태(snapshot)을 쉽게 찾을 수 있다.

아래 코드는 예제이다.

```js
import Vue from "vue";
import Vuex from "vuex";

Vue.use(Vuex);

export const store = new Vuex.Store({
  state: {
    count: 0,
  },
});
```

### getters

`state`의 값을 계산(변경)시킬 때 사용한다.

`getters`를 사용하지 않고 각각의 컴포넌트에서 `state`를 증가시키면 반복 호출이 잦아져 비효율적인 로직이 된다.

`getters`는 `state`에 대한 변이를 각 컴포넌트에서 진행하는게 아니라, Vuex에서 변이를 수행하고 각 컴포넌트에서 변이된 `state`를 호출만 하게 만든다.

```js
// store/index.js
import { createStore } from "vuex";

export default createStore({
  getters: {
    increment(state) {
      return state.count++;
    },
  },
});
```

```vue
// View/index.vue
<template>
  <div>
    <button @click="increment">count + 1: {{ count }}</button>
  </div>
</template>
<script setup>
import { computed } from "vue";
import { useStore } from "vuex";
const store = useStore();
const count = computed(() => store.state.count);
const increment = () => store.getters.increment;
</script>
```

### mutations

`state`의 값을 계산(변경)시킬 때 사용한다. `state` **동기적** 변이를 다룬다.

`mutaions`와 `getters`의 차이점

- `mutaions`는 전달인자를 받을 수 있다.
- `getters`는
  - option API기준 `computed`에 등록하지만 `mutations`는 `method`에 등록한다.
  - composition API기준 `computed`으로 등록하지만 `mutations`는 `function`으로 등록한다.

```js
// store/index.js
import { createStore } from "vuex";

export default createStore({
  mutations: {
    increment(state, amount) {
      return (state.count += amount);
    },
  },
});
```

```vue
// View/index.vue
<template>
  <div>
    <button @click="increment(10)">count + 10: {{ count }}</button>
  </div>
</template>
<script setup>
import { computed } from "vue";
import { useStore } from "vuex";
const store = useStore();
const count = computed(() => store.state.count);
const increment = (amount) => store.commit("increment", amount);
</script>
```

`commit`에 추가 전달 인자를 넘길 수 있는데, 이 추가 전달 인자 부분을 `payload`라고 한다.

```js
store.commit("mutations name", "payload");
```

`payload`는 아래와 같이 객체 형태로 전달 될 수도 있다.

```js
// store/index.js
mutaions: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```

```js
// view/index.vue
store.commit("increment", {
  amount: 10,
});
```

### actions

`mutaions`는 **동기적** 변이를 다룬다고 했다.
`actions`는 그와 반대로 **비동기적** 변이를 다루는 속성이다.

## 참고 자료

- [vuex docs](https://vuex.vuejs.org/)
- [Vuex란? 개념과 예제](https://doozi0316.tistory.com/entry/Vuex-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%98%88%EC%A0%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
