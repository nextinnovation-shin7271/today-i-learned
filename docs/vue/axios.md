# Axios

액시오스(Axios)는 브라우저와 node.js에서 사용할 수 있는 Promise 기반 HTTP 클라이언트 라이브러리이며, Vue에서 권고하는 HTTP 통신 라이브러리다.
액시오스는 상대적으로 다른 HTTP 통신 라이브러리들에 비해 문서화가 잘돼있고 API가 다양하다.

## Table of Contents

- [Axios](#axios)
  - [Table of Contents](#table-of-contents)
  - [설치](#설치)
  - [사용방법](#사용방법)
  - [액시오스 응답 제어](#액시오스-응답-제어)
    - [`.then`](#then)
    - [`.catch`](#catch)
  - [HTTP 요청 주요 메소드](#http-요청-주요-메소드)
    - [axios.get(url[, config]) - read](#axiosgeturl-config---read)
    - [axios.post(url[, data[, config]]) - create](#axiosposturl-data-config---create)
    - [axios.put(url[, data[, config]]) - update](#axiosputurl-data-config---update)
    - [axios.delete(url[, config]) - delete](#axiosdeleteurl-config---delete)
  - [HTTP 요청 Config 옵션](#http-요청-config-옵션)
    - [url](#url)
    - [method](#method)
    - [baseURL](#baseurl)
    - [headers](#headers)
    - [params](#params)
    - [data](#data)
    - [timeout](#timeout)
    - [responseType](#responsetype)
  - [참고 자료](#참고-자료)

## 설치

npm

```sh
$ npm install axios
```

cdn

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

## 사용방법

라이브러리를 설치하고 나면 `axios`라는 변수에 접근 가능하다. `axios`변수를 이용해 아래와 같이 HTTP GET요청을 날릴 수 있다.

```js
// 저수준 API
axios({
  method: "get",
  url: "https://jsonplaceholder.typicode.com/users",
}).then((response) => {
  console.log(response);
});
// or
// 요청 메소드 명령어
axios.get("https://jsonplaceholder.typicode.com/users").then((response) => {
  console.log(response);
});
```

위는 간단한 조회(GET) 요청을 한 예시이고, axios에 존재하는 모든 요청 명령어를 통해 추가(POST), 수정(PUT, PATCH), 삭제(DELETE)등의 CRUD모두 가능하다.

저수준 API

- `axios(config)`
- `axios(url[, config])`

요청 메소드 명령어

- `axios.request(config)`
- `axios.get(url[, config])`
- `axios.delete(url[, config])`
- `axios.head(url[, config])`
- `axios.options(url[, config])`
- `axios.post(url[, data[, config]])`
- `axios.put(url[, data[, config]])`
- `axios.patch(url[, data[, config]])`

axios함수의 반환값이 프로미스이기 때문에 기본적인 방법으로 프로미스를 사용해도 되지만, `async` & `await`를 사용해서 보다 가독성있게 코드를 작성 가능하다.

promise

```js
axios
  .get(url)
  .then((response) => {
    console.log(response);
  })
  .catch((error) => {
    console.log(error);
  });
```

async & await

```js
const fetchData = async () => {
  try {
    const response = await axios(url);
    console.log(response);
  } catch (error) {
    console.log(error);
  }
};
```

## 액시오스 응답 제어

### `.then`

비동기 통신이 성공했을 경우, `.then()`은 콜백을 인자로 받아 결괏값을 처리한다. 첫 번째 인자로 `response`를 받으며 호출에 대한 응답을 의미한다.

### `.catch`

`.catch()`를 통해 오류를 처리한다. 첫 번째 인자로 `error`를 받으며 오류에 대한 주요 정보를 확인할 수 있다.

## HTTP 요청 주요 메소드

액시오스에서 자주 사용되는 HTTP 요청 메서드를 예시와 함께 알아본다.

### axios.get(url[, config]) - read

서버에서 데이터를 가져(read)올 때 사용하는 메서드이다. 두 번째 파라미터 `config`객체에는 헤더(header), 응답 초과시간(timeout), 인자 값(params), 인자 값(params) 등의 요청 값을 같이 넘길 수 있다.

```js
axios.get("users/1");
```

### axios.post(url[, data[, config]]) - create

서버에 데이터를 새로 생성(create)할 때 사용하는 메서드이다. 두 번째 파라미터 `data`에 생성할 데이터를 넘긴다.

```js
axios.post("/users", {
  email: "test@test.com",
  username: "test",
  password: "1234",
});
```

### axios.put(url[, data[, config]]) - update

특정 데이터를 수정(update)할 때 사용하는 메서드이다. `put`은 새로운 리소스를 생성하거나, 이미 존재하는 데이터를 대체(덮어쓰기)할 때 사용된다.

`post`와 다른 점은 `post`는 여러 번 호출할 경우, 새로운 데이터가 지속적으로 추가된다. 반면, `put`은 한 번 요청을 하거나 여러 번 요청해도 결괏값이 동일하다.

아래 코드를 해석하면, `id`가 1인 user의 email과 username을 수정한다.

```js
axios.put("users/1", {
  email: "test2@test.com",
  username: "test2",
  password: "1234",
});
```

### axios.delete(url[, config]) - delete

특정 데이터나 값을 삭제할 때 요청하는 메서드이다.

```js
axios.delete("users/1");
```

## HTTP 요청 Config 옵션

액시오스 요청을 할 때 config 설정이 가능하다.

### url

`url`은 액시오스 요청에 사용될 서버의 URL을 의미한다.

```
url: "/users"
```

### method

`method`는 요청을 할 때 사용할 요청 메서드이다. `method`의 기본값은 get이다.

```
method: "get"
```

### baseURL

`baseURL`은 액시오스 인스턴를 생성할 때, 인스턴스의 기본 URL 값을 정할 수 있는 속성이다. 보통 `http://mysite.com/api/v1/`처럼 API 서버의 기본 도메인을 설정하고, 인스턴스 별로 URL을 뒤에 추가하여 사용한다.

```
baseURL: "https://도메인.com/api/"
```

### headers

`headers`는 헤더를 수정해서 보내야 할 때 사용한다.

```
headers: {'X-Requested-With': 'XMLHttpRequest'}
```

### params

`params`는 HTTP 요청에 붙일 URL 파라미터를 의미한다. 예를 들어, 아래 예시 코드는 URL이 `https://domain.com`이라 할 때, URL로 HTTP 요청을 보냈을 때 `https://domain.com?id=123`으로 전달하는 것과 같은 효과를 가진다. 중요한 점은 `params`의 값이 `null`, `undefined`인 경우 파라미터가 조합되지 않는다.(무시된다.)

```
params: {
  id: 123
}
```

### data

`data`는 HTTP 요청 BODY에 실어서 보낼 데이터를 의미한다. 주로 데이터를 조작해야 하는 `PUT`, `POST`, `DELETE`, `PATCH`등의 메서드에서 사용한다.

```
// 기본적인 data 속성의 사용법
data: {
  firstName: "Christine"
}

// 아래의 data config 설정은 POST 메서드에서만 사용이 가능하다.

data: "Age=26&City=New York"
```

### timeout

`timeout`은 HTPP 요청을 보내고 응답을 받기까지의 제한 시간을 설정하는 속성이다.
요청 시간이 지정된 값을 초과하면 에러가 발생한다.

```
// 단위(millisecond)
timeout: 5000
```

### responseType

`responseType`은 서버로부터 어떠한 데이터 형식으로 응답받을지 지정하는 것이다. 옵션으로는 arraybuffer, document, json, text, stream이 가능하다. 기본 값은 json이다.

```
responseType: 'json'
```

자세한 요청 config는 [액시오스 공식 문서](https://axios-http.com/kr/docs/req_config)를 확인

## 참고 자료

- [Axios docs](https://axios-http.com/kr/docs/intro)
- [Axios 액시오스 - 캡틴판교](https://joshua1988.github.io/vue-camp/vue/axios.html)
