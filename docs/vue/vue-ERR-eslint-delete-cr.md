# vue ERR eslint delete cr

## case

vue 프로젝트 설정 시 eslint, prettier 사용으로 생성.
SFC 방식으로 vue파일을 작성했을 때 `ERR eslint delete 'cr'`이라는 에러메시지가 발생

## solution

1. visual studio에서 `crtl+shift+p`로 명령 파레트 열고 `change end of line sequence(줄 시퀀스의 끝 변경)`에서 `CRLF`를 `LF`로 변경

   > 파일마다 설정을 해줘야 하므로 제대로 된 해결방법은 아니다.

2. 프로젝트 루트에서 `.eslintre.js(json)`파일을 열고 `rules`에 아래 코드 추가

넣어야 하는 코드

```js
  "prettier/prettier": [
    "error",
    {
    endOfLine: "auto",
    },
  ]
```

rules에 넣은 전체 코드

```js
  code...
  rules: {
    code...
    "prettier/prettier": [
      "error",
      {
        endOfLine: "auto",
      },
    ],
  },
```

## 참고 자료

- [https://stackoverflow.com/questions/53750853/visual-studio-code-eslint-delete-cr-prettier-prettier-on-windows](https://stackoverflow.com/questions/53750853/visual-studio-code-eslint-delete-cr-prettier-prettier-on-windows)
