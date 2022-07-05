# npm

**npm is the world's largest software registry.** 라고 npm documentation에서 소개하고 있듯이 npm은 자바스크립트 프로그래밍 언어를 위한 패키지 관리자이다. yarn또한 npm과 같이 js 패키지 매니저이다.

## global vs local

npm을 이용하여 모듈을 설치할 때 전역(global)혹은 지역(local)설치를 할 수 있다. 전역은 어느 프로젝트, 어느 디렉토리에서 전부 사용할 수 있는 것이고, local은 해당 프로젝트의 디렉토리에서만 설치되는 것이다.

- 전역(global) 설치

  - 장점: 해당 모듈을 설치 후 따로 설정할 작업 없이 npm run을 안붙여주고 바로 사용할 수 있다.
  - 단점: 전역으로 설치된 모듈이 많아질수록 pc가 무거워지고 모듈간 충돌이 일어날 확률이 높아진다.

- 지역(local) 설치

  - 장점: 프로젝트마다 필요로 하는 모듈을 따로 설치하기 때문에 모듈 관리가 편하다. 향후 pc가 무거워지는 것을 방지할 수 있다.
  - 단점: package.json 설정이 필요하다. 명령어 입력 시 앞에 npm을 붙여줘야 한다.

terminal에 `npm install 패키지`를 실행한 경우

```npm
# 지역 설치
npm install cowsay
```

package.json 파일에 추가되는 항목

```json
"dependencies": {
  "cowsay": "^1.5.0"
}
```

## dependencies

dependencies는 일반적인 경우, 의존하고 있다는 것을 알려준다.
현재 프로젝트를 npm에서 가져온 외부(External) 패키지로 확장할 수 있다.
패키지 매니저를 사용하는 가장 큰 이유 중 하나로서, 강력한 종속성 관리(dependency management)를 가능하게 한다. 서로 다른 컴퓨터에서 프로젝트를 설정할 때 마다 모든 종속성을 수동으로 확인하지 않고 package.json 파일의 dependencies 섹션의 목록을 보고 모든것을 자동으로 설치한다.

```npm
npm install [패키지명]
npm install cowsay
```

--save 옵션을 줘(생략가능) dependencies에 추가한 경우 json파일에는 아래와 같이 종속성이 추가된다.

```json
  "dependencies": {
    "cowsay": "^1.5.0"
  }
```

## devDependencies

devDependencies는 development dependencies의 약자로서, 개발 모드일 때만 의존하고 있다는 것을 알려준다. 실제로 배포할 때는 필요없는 테스트 도구나 webpack, babel, eslint, prettier 같은 것들이 devDependencies에 들어간다.

```npm
npm install [패키지명] --save-dev[or -D]
npm install cowsay --save-dev
```

--save-dev, -D 옵션을 줘 devDependencies에 추가한 경우 json파일에는 아래와 같이 개발 종속성이 추가된다.

```json
  "devDependencies": {
    "cowsay": "^1.5.0"
  }
```

`--save`, `--save-dev`는 플러그인이 dependencies 항목에 저장 되는지 아니면 devDependencies에 저장 되는지를 선택하는 것이다.
devDependencies는 개발모드에서만 활용 되는 플러그인을 저장한다. `--save`는 기본값이기 때문에 생략 가능하다.

## 참고자료

- [package.json의 개념](https://helloinyong.tistory.com/85)
- [https://www.bottlehs.com/vue/vue-js-router-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%84%A4%EC%A0%95/](https://www.bottlehs.com/vue/vue-js-router-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%84%A4%EC%A0%95/)
- [https://jinyisland.kr/post/npm/](https://jinyisland.kr/post/npm/)
- [웹팩 핸드북(캡틴판교)](https://joshua1988.github.io/webpack-guide/build/npm-module-install.html#npm-%EC%84%A4%EC%B9%98-%EB%AA%85%EB%A0%B9%EC%96%B4)
