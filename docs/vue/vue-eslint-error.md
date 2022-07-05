# vue-eslint-error

## case

`no babel config file detected for ~`와 같은 에러가 발생하면서 화면랜더링이 제대로 안되는 상황이 발생했다.

## solution

1. `no babel config file detected for`키워드로 에러 해결 방법을 검색

   - 프로젝트 폴더가 루트가 아닌 경우 나타나는 경로 문제, settings.json파일에 옵션 추가하면 해결 가능

2. vcs 설정 파일 변경
   `ctrl+shift+p`로 명령 파레트 연 후 settings.json를 검색해 `기본 설정: 설정 열기(json)`로 들어가 파일에 아래 코드 추가

```json
"eslint.workingDirectories": [
        {"mode": "auto"}
    ]
```
