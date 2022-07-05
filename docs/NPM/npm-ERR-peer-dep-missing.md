# npm-ERR-peer-dep-missing.md

## case

```npm
npm ERR! peer dep missing: webpack@>=2, required by babel-loader@8.2.5
npm ERR! peer dep missing: openapi-types@>=7, required by @apidevtools/swagger-parser@10.0.2
```

## solution

peer dep missing 패키지를 설치하거나, npm을 업그레이그 한 뒤 `npm install`을 실행

```
npm install webpack@>=2
npm install openapi-types@>=7

or

npm update -g npm
npm install
```

## 참고자료

-[https://stackoverflow.com/questions/69618191/how-to-fix-npm-err-peer-dep-missing](https://stackoverflow.com/questions/69618191/how-to-fix-npm-err-peer-dep-missing)
