# Vue Lifecycle

라이프사이클 훅은 import를 사용해 직접적으로 `onX`함수에 등록할 수 있다.

```js
import { onMounted, onUpdated, onUnmounted } from "vue";

const MyComponent = {
  setup() {
    onMounted(() => {
      console.log("mounted!");
    }),
      onUpdated(() => {
        console.log("updated!");
      }),
      onUnmounted(() => {
        console.log("unmounted!");
      });
  },
};
```

![vue2, 3 lifecycle diff](./img/vue2_3_lifecycle_diff.png)

> setup은 beforeCreate, created 라이프사이클 훅 사이에 실행되는 시점이므로(`beforeCreate()`가 `setup()` 직전에 호출되고 `created()`가 `setup()` 직후에 호출되는 타이밍을 가짐), 명시적으로 정의할 필요가 없다. 다시말해, 위 두 훅에서 작성되는 모든 코드는 `setup()` 내부에 직접 작성해야한다.

## 참고 자료

- [vue docs - 라이프사이클 훅](https://v3.ko.vuejs.org/guide/composition-api-lifecycle-hooks.html)
