# vue-router

## 기본 라우팅

```vue
<!-- App.vue -->
<template>
  <h1>Hello app!</h1>
  <nav>
    <!-- basic routing -->
    <router-link to="/">Home</router-link>
    <!-- named basic routing -->
    <router-link :to="{ name: 'Home' }">Home</router-link>
    <router-link to="/about">About</router-link>
    <!-- dynamic routing -->
    <router-link to="/about/1">About1</router-link>
    <router-link to="'/about'+id">About2</router-link>
    <!-- named dynamic routing -->
    <router-link :to="{ name: 'AboutId', params: { id: id } }"
      >About2</router-link
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
// 1. Define route components.
// These can be imported from other files
const Home = { template: "<div>Home</div>" };
const About = { template: "<div>About</div>" };
// 2. Define some routes
// Each route should map to a component.
// We'll talk about nested routes later.
const routes = [
  { path: "/", name: "Home", component: Home },
  { path: "/about", name: "About", component: About },
  { path: "/about/:id", name: "AboutId", component: About },
];
// 3. Create the router instance and pass the `routes` option
// You can pass in additional options here, but let's
// keep it simple for now.
const router = VueRouter.createRouter({
  // 4. Provide the history implementation to use. We are using the hash history for simplicity here.
  history: VueRouter.createWebHashHistory(),
  routes, // short for `routes: routes`
});

// 5. Create and mount the root instance.
const app = Vue.createApp({});
// Make sure to _use_ the router instance to make the
// whole app router-aware.
app.use(router);

app.mount("#app");
```
