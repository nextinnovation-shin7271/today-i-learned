# 웹팩 (webpack)

## 1. 웹팩의 4가지 주요 속성

웹팩의 빌드(파일변환) 과정을 이해하기 위해서는 아래 4가지 주요 속성에 대해 알고 있어야 한다.

- entry
- output
- loader(module)
- plugin

### 1.1. entry

`entry` 속성은 웹팩에서 웹 자원을 변환하기 위해 필요한 **최초 진입점**이자 **자바스크립트 파일 경로** 이다.

```js
// webpack.config.js
module.export = {
  entry: "./src/index.js",
};
```

```js
// webpack.config.js
module.export = {
  entry: {
    main: "./src/index.js",
    login: "./src/login.js",
  },
};
```

### 1.2. output

`output` 속성은 웹팩을 빌드한 결과물의 파일 경로를 의미한다.

```js
// webpack.config.js
module.export = {
  output: {
    filename: "bundle.js",
  },
};
```

```js
// webpack.config.js

const path = require("path");

module.export = {
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "./dist"),
  },
};
```

위 속성을 살펴보면,

- `filename`: 웹팩으로 빌드한 파일의 이름
- `path`: `filename에` 해당하는 파일의 경로

> path속성에 사용된 `path.resolve()`함수는 인자로 넘어온 경로들을 조합해 유효한 파일 경로를 만들어주는 Node.js API이다.

### 1.3. loader

로더(Loader)는 웹팩이 웹 애플리케이션을 해석할 때 자바스크립트 파일이 아닌 **웹 자원(HTML, CSS, Images, font 등)** 들을 변환할 수 있도록 도와주는 속성이다.

로더는 아래와 같이 적용한다.

```js
module.exports = {
  module: {
    rules: [{}],
  },
};
```

예를 들어 빌드할 `js` 파일에 `css` 파일을 임포트한다면 에러가 발생하면서 빌드에 실패하는데, `css` 파일을 해석하기 위한 적절한 로더를 추가해야만 문제없이 빌드된다.

```js
// app.js
import "./common.css";
console.log("css loader");
```

```css
/* common.css */
p {
  color: red;
}
```

```js
// webpack.config.js
module.exports = {
  entry: "./app.js",
  output: {
    filename: "bundle.js",
  },
};
```

#### CSS Loader 적용하기

위에서 `css` 파일을 빌드 파일에 포함시켰을 때 에러가 발생했는데, 웹팩 설정을 통해 정상적으로 빌드되게 해결할 수 있다.

```sh
npm i css-loader -D
```

```js
// webpack.config.js
module.exports = {
  entry: "./app.js",
  output: {
    filename: "bundle.js",
  },
  module: {
    rulss: [
      {
        test: /\.css$/,
        use: ["css-loader"],
        exclude: /node_modules/,
      },
    ],
  },
};
```

위 `module`쪽 코드에서 `rules` 배열에 객체 한 쌍을 추가했다. 객체의 내용으로 2개의 속성이 들어가 있는데 각각 아래와 같은 역할을 한다.

- `test`: 로더를 적용할 파일 유형(일반적으로 정규식 사용)
- `use`: 해당 파일에 적용할 로더의 이름
- `exclue`: 트랜스파일 대상에 포함시키지 않을 파일명(정규식)

정리하면 위 코드는 해당 프로젝트의 모든 `css` 파일에 대해서 `css` 로더를 적용하겠다는 의미이다.

#### 자주 사용되는 로더 종류

앞서 살펴본 css로더 이외에도 실제 서비스를 만들 때 자주 사용되는 로더의 종류는 다음과 같다.

- Babel Loader
- Sass Loader
- File Loader
- Vue Loader
- TS Loader

여러 로더를 적용할 땐 아래와 같이 객체를 추가해주면 된다.

```js
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: "css-loader" },
      { test: /\.ts$/, use: "ts-loader" },
      // ...
    ],
  },
};
```

#### 로더 적용 순서

특정 파일에 대해 여러 개의 로더를 사용하는 경우(ex - scss, css) 로더가 적용되는 순서에 주의해야 한다. 로더는 기본적으로 **오른쪽에서 왼쪽 순서로 적용**된다.

```js
module: {
  rules: [
    {
      test: /\.scss$/,
      use: ["css-loader", "sass-loader"],
    },
  ];
}
```

위 코드는 scss 파일에 대해 먼저 sass 로더로 전처리(scss 파일을 css 파일로 변환)를 한 다음 웹팩에서 css 파일을 인식할 수 있게 CSS 로더를 적용하는 코드이다.

### 1.4. plugin

플러그인(plugin)은 웹팩의 기본적인 동작에 추가적인 기능을 제공하는 속성이다. 로더랑 비교하면 로더는 파일을 해석하고 변환하는 것이고, 플러그인은 해당 결과물의 형태를 바꾸는 역할을 하는 차이점이 있다.

플러그인은 아래와 같이 선언한다.

```js
// webpack.config.js
module.exports = {
  plugins: [],
};
```

플러그인의 배열에는 생성자 함수로 생성한 객체 인스턴스만 추가될 수 있다.

```js
// webpack.config.js
const webpack = require("webpack");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  plugins: [new HtmlWebpackPlugin(), new webpack.ProgressPlugin()],
};
```

- HtmlWebpackPlugin: 웹팩으로 빌드한 결과물로 HTML 파일을 생성해주는 플러그인
- 웹팩의 빌드 진행율을 표시해주는 플러그인

### 1.5. 웹팩 속성 정리

![webpack properties](https://joshua1988.github.io/webpack-guide/assets/img/diagram.519da03f.png)

1. Entry: 웹팩을 실행한 대상 파일. 진입점
2. Output: 웹팩의 결과물에 대한 정보를 입력하는 속성. 일반적으로 `filename`과 `path`를 정의
3. Loader: CSS, 이미지 같은 비 자바스크립트 파일을 웹팩이 인식할 수 있게 추가하는 속성. 한 파일에 로더가 여러개인 경우 오른쪽에서 왼쪽 순으로 적용
4. Plugin: 웹팩으로 변환한 파일에 추가적인 기능을 더하고 싶을 때 사용하는 속성. 웹팩 변환 과정 전반에 대한 제어권을 갖고 있음

> 위 속성 이외에도 resolve, devServer, devtool 등 속성이 존재하므로 알아두면 좋다.

## 참고 자료

- [캡틴판교 - 웹팩 핸드북](https://joshua1988.github.io/webpack-guide/guide.html)
