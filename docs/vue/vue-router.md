# vue-router

뷰 라이터는 뷰 라이브러리를 이용해 싱글 페이지 애플리케이션을 구현할 때 사용하는 라이브러리다. 이 글은 vue cli를 이용한 프로젝트라 가정하고 코드를 작성한다.

## Table of Contents

- [vue-router](#vue-router)
  - [Table of Contents](#table-of-contents)
  - [설치](#설치)
  - [뷰 라우터 등록](#뷰-라우터-등록)
  - [기본 라우팅](#기본-라우팅)
    - [router-view](#router-view)
    - [router-link](#router-link)
  - [동적 라우팅](#동적-라우팅)
  - [중첩 라우팅](#중첩-라우팅)
  - [정리](#정리)
  - [참고 자료](#참고-자료)

## 설치

npm

```
$ npm install vue-router
```

## 뷰 라우터 등록

뷰 라우터는 `@router/index.js`위치에 작성하며 기본적인 라우팅 등록으로 아래와 같이 작성한다.

```js
// router/index.js
// 1. 컴포넌트를 정의한다.
// 컴포넌트는 import로 대체될 수 있다.
const Home = { template: "<div>Home</div>" };
const About = { template: "<div>About</div>" };
// 2. 라우트를 정의한다.
// 각 라우트는 컴포넌트에 매핑된다.
const routes = [
  { path: "/", name: "Home", component: Home },
  { path: "/about", name: "About", component: About },
];
// 3. 라우터 인스턴스를 생성하고 옵션에 위에서 정의한 라우트를 넘긴다.
const router = VueRouter.createRouter({
  // 4. URL에 해쉬값을 추가할지, 제거할지 정한다.
  history: VueRouter.createWebHashHistory(),
  routes, // `routes: routes`의 축약형이다.
});

// 5. root 인스턴스를 생성하고 마운트한다.
const app = Vue.createApp({});
// root 인스턴스에 router를 사용(use)해 라우터를 전역적으로 사용하게 한다.
app.use(router);

app.mount("#app");
```

## 기본 라우팅

### router-view

브라우저 주소 창에서 URL이 변경되면, 앞에서 정의한 routes속성에 따라 해당 컴포넌트가 화면에 렌더링된다. 이 때 렌더링되는 지점이 템플릿의 `<router-view>`이다.

```vue
<template>
  <router-view />
</template>
```

### router-link

기존 HTML의 a태그와 비슷한 역할을 하는데, SPA(Single Page App)특성에 맞게 작동하도록 만든 태그라고 생각하면 된다. a태그에서 `href`속성으로 링크를 정했는데, router-link태그에선 `to`속성으로 링크를 정할 수 있다.

```vue
<template>
  <router-link to="/">Home</router-link>
  <router-link to="/about">About</router-link>
</template>
```

## 동적 라우팅

주어진 패턴을 가진 라우트를 동일한 컴포넌트에 매핑해야 하는 경우 사용한다.
예를 들어 모든 사용자들 중에 한명의 사용자를 조회할 때 동일한 레이아웃을 가지지만 다른 사용자 `id`로 렌더링 돼야 하는 경우 사용한다.

```vue
<!-- 간단한 예시이므로 id가 1, 2인 사용자를 찾는 코드를 하드하게 작성했다. -->
<template>
  <router-link to="/users">Users</router-link>
  <router-link to="/users/1">Search User 1</router-link>
  <router-link to="/users/2">Search User 2</router-link>
  <!-- ... -->
  <router-view />
</template>
```

```js
// @router/index.js
// ...
const routes = [
  { path: "/users", name: "Users", component: User },
  { path: "/users/:id", name: "UsersId", component: UserId },
];
// ...
```

위 예시를 보면 `/uesrs/1`과 `/users/2`은 모두 같은 경로에 매핑돼 `UserId`라는 동일한 컴포넌트가 렌더링된다.

## 중첩 라우팅

실제 앱 UI는 일반적으로 여러 단계로 중첩된 컴포넌트로 이루어져 있다. URL의 새그먼트가 중첩된 컴포넌트 구조와 일치한다는 것은 매우 일반적이다.
예를 들어 전체 사용자 조회 페이지와 단일 사용자 조회 페이지에 모두 적용돼야 하는 공통 컴포넌트(레이아웃)이 있는 경우 중첩 라우팅을 사용한다.

```vue
<template>
  <router-link to="/users">Users</router-link>
  <router-link to="/users/1">Search User 1</router-link>
  <router-link to="/users/2">Search User 2</router-link>
  <!-- ... -->
  <router-view />
</template>
```

```js
// @router/index.js
// ...
const routes = [
  {
    path: "/users",
    name: "UsersLayout",
    component: UserLayout,
    children: [
      { path: "", name: "Users", component: User }, // `/users` url과 동일하게 매핑된다.
      { path: "/:id", name: "UsersId", component: UserId }, // `/users/:id` url과 동일하게 매핑된다.
    ],
  },
];
// ...
```

## 정리

```vue
<!-- App.vue -->
<template>
  <h1>Hello app!</h1>
  <nav>
    <!-- 기본 라우팅 -->
    <router-link to="/">Home</router-link>
    <!-- 이름 기본 라우팅 -->
    <router-link :to="{ name: 'Home' }">Home</router-link>
    <router-link to="/users">Users</router-link>
    <!-- 동적 라우팅 -->
    <router-link to="/users/1">Users1</router-link>
    <!-- 링크  -->
    <router-link :to="'/users/' + id">Users2</router-link>
    <!-- 이름 동적 라우팅 -->
    <router-link :to="{ name: 'usersId', params: { id: id } }"
      >Users2</router-link
    >
  </nav>
</template>
<script setup>
import { ref } from "vue";
const id = ref(2);
</script>
```

```js
// router/index.js
// 1. 컴포넌트를 정의한다.
// 컴포넌트는 import로 대체될 수 있다.
const Home = { template: "<div>Home</div>" };
const Users = { template: "<div>Users</div>" };
const UsersId = { template: "<div>Users Id</div>" };
// 2. 라우트를 정의한다.
// 각 라우트는 컴포넌트에 매핑된다.
const routes = [
  { path: "/", name: "Home", component: Home },
  {
    path: "/users",
    name: "UsersLayout",
    compoment: UsersLayout,
    // 2.1. 중첩 라우트를 정의한다.
    children: [
      { path: "", name: "Users", component: Users },
      // 2.2. 동적 라우트를 정의한다.
      { path: "/:id", name: "UsersId", component: UsersId },
    ],
  },
];
// 3. 라우터 인스턴스를 생성하고 옵션에 위에서 정의한 라우트를 넘긴다.
const router = VueRouter.createRouter({
  // 4. URL에 해쉬값을 추가할지, 제거할지 정한다.
  history: VueRouter.createWebHashHistory(),
  routes, // `routes: routes`의 축약형이다.
});

// 5. root 인스턴스를 생성하고 마운트한다.
const app = Vue.createApp({});
// root 인스턴스에 router를 사용(use)해 라우터를 전역적으로 사용하게 한다.
app.use(router);

app.mount("#app");
```

## 참고 자료

- [vue router docs](https://v3.router.vuejs.org/kr/guide/#html)
- [캡틴판교 - 뷰 라우터](https://joshua1988.github.io/vue-camp/vue/router.html#%E1%84%87%E1%85%B2-%E1%84%85%E1%85%A1%E1%84%8B%E1%85%AE%E1%84%90%E1%85%A5-%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5)
- [velog - Vue Router 정리](https://velog.io/@yjyoo/vue.js-Vue-Router-%EC%A0%95%EB%A6%AC)
