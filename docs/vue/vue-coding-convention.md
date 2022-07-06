# Vue Coding Convention

## Priority A Rules

### 1. Multi-word component names

컴포넌트 이름은 항상 복수의 단어로 구성돼야 한다. `App`컴포넌트와 Vue의 내장 컴포넌트인 `<transition>`과 `<component>`는 제외된다.

이것은 기존에 존재하는 HTML 앨리먼트와의 충돌을 예방하기 위한것이다.

### 2. Component data

컴포넌트 `data`속성은 반드시 함수여야 한다. 객체를 반환하는 함수여야 한다.

### 3. Prop definitions

`prop` 정의는 가능한 자세하게 해야한다. 간결하게 하고 싶다면 적어도 `prop`의 `type`은 명시해줘야 한다.

### 4. Keyed `v-for`

`v-for`디렉티브를 이용할 때는 항상 `key`를 같이 써야 한다. 하위 트리에서 내부 컴포넌트의 상태를 유지하려면 컴포넌트에서 `v-for`와 `key`를 항상 같이 써야한다.

### 5. Avoid `v-if` with `v-for`

절대 `v-if`를 `v-for`가 있는 앨리먼트에 같이 사용하지 마라.
같이 사용해야 하는 경우가 있다면 `computed`속성을 이용해 `v-for`에 계산된 값을 넣어라.

### 6. Component style scoping

애플리케이션에서 최상위 컴포넌트인 `App`컴포넌트와 `layout`컴포넌트의 스타일(CSS)는 아마 `global` scope를 가질 것이다. 하지만 모든 다른 컴포넌트의 스타일은 `local` scope(scoped)를 가져야 한다.

위 규칙은 SFC(Single-File Components)에 적합하며, 이외의 경우 CSS modules나 BEM, 라이브러리 컨벤션이 있다면 해당 규칙에 따르면 된다.

그러나 컴포넌트 라이브러들은 scoped 속성을 사용하는 대신 class 기반이어야 한다.

이것은 내부 스타일 덮어쓰기를 쉽게 만든다. 즉, 스타일 충돌이 적게 일어난다.

### 7. Private property names

모듈 범위 지정을 사용해 외부에서 개인 함수에 액세스 할 수 없게 하라.
이것이 가능하지 않다면, 항상 공용 API로 간주되면 안되는 플러그인, 믹스인 등의 사용자 지정 개인 속성에 `$_`접두사를 사용해라.

## 참고 자료

- [vue2 docs - Style Guide](https://v2.vuejs.org/v2/style-guide/)
