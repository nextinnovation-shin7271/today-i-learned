# vue2 to vue3 migration

Vue3로 마이그레이션 하는 이유는 라이브러리, 언어, 프레임워크 등의 기술들이 진화함에따라 수정된 버그, 새로운 특징들이 새 버전으로 나오면서, 새 버전을 사용하는 것이 작업시에 이점을 주기 때문이다.

그러나 모든 프로젝트를 마이그레이션 할 필요는 없다. 하지만 시간이 지나면 Vue2는 지원이 끝날것이다. 그렇기 때문에 순차적으로 마이그레이션을 하는것이 좋다.

## Table of Contents

- [vue2 to vue3 migration](#vue2-to-vue3-migration)
  - [Table of Contents](#table-of-contents)
  - [vue2와 vue3의 차이점](#vue2와-vue3의-차이점)
    - [API style](#api-style)
  - [마이그레이션 스텝](#마이그레이션-스텝)
    - [1. Branch the Project](#1-branch-the-project)
    - [2. Update vue](#2-update-vue)
    - [3. Update Vue instance](#3-update-vue-instance)
    - [4. Update Vue library and plugin](#4-update-vue-library-and-plugin)
  - [참고 자료](#참고-자료)

## vue2와 vue3의 차이점

### API style

가장 큰 차이점은 vue2는 `Option API`를 사용해 컴포넌트를 작성하고, vue3는 `Composition API`를 사용해 컴포넌트를 작성한다. 반드시 `Composition API`로 작성해야 하는것은 아니지만, 작성하는 코드 로직에 대한 관심사가 한군데에 집중되게 되어 가독성 면에서 큰 이점이 존재하기때문에 권장하는 API Style이다.
또한 기존에 react를 사용해본 경험이 있다면 hook의 개념을 생각하면 `Composition API`를 이해하는데 도움이 될 수 있다.

## 마이그레이션 스텝

### 1. Branch the Project

마이그레이션할 프로젝트를 마이그레이션 브랜치로 생성한다.

### 2. Update vue

생성한 브랜치의 프로젝트에서 vue 버전을 업데이트한다.

### 3. Update Vue instance

Vue2 인스턴스와 컴포넌트 작성 방법을 vue3 버전에 맞게 작성한다.

### 4. Update Vue library and plugin

vue 라이브러리인 router, vuex 등을 vue3 버전에 맞게 작성한다. 이 과정에서 vue2에서는 호환이 되나, vue3는 아직 지원하지 않는 라이브러리나 플러그인들이 존재한다면 마이그레이션이 어려울 수 있다.

## 참고 자료

- [vue docs - Migration Build](https://v3-migration.vuejs.org/migration-build.html#installation)
- [freeCodeCamp - How to Migrate from Vue v.2 to Vue v.3 with a Simple Example Project](https://www.freecodecamp.org/news/migrate-from-vue2-to-vue3-with-example-project/)
- [시티즌 인사이트 - Vue2에서 Vue3.1로 마이그레이션하는 방법](https://dev.grapecity.co.kr/bbs/board.php?bo_table=Insight&wr_id=73)
