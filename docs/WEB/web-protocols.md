# Web Protocol

## 1. URL (Uniform Resourece Locator)

웹 프로토콜을 알아보기 전에 먼저 URL 개념을 알아야 한다. 웹 프로토콜을 통해 데이터를 요청할 때 URL이 필요하기 때문이다. 웹에서 웹 페이지를 정의하고 접근하기 위해 URL을 사용한다.

아래는 URL의 일반적인 형식이다.

```http
protocol://domain_name:port/document_name?parameters
```

위 형식에서 각 단위의 역할은 아래와 같다.

- protocol: 문서를 접근하기 위해 사용하는 프로토콜 이름
  - ex) http, https, ftp
- domain_name: 문서가 있는 컴퓨터의 도메인 이름
  - ex) naver.com, google.com
- port: 서버가 어떤 포트 숫자를 바라보고 있는지 (선택사항)
  - ex) 8080, 8000
- document_name: 서버 컴퓨터에 있는 특정 문서의 이름
  - ex) product, product/shirts
- parameter: 페이지에 넘기는 변수, `?`로 시작하며 여러 파라미터가 존재하는 경우 `&`로 이어서 표현한다. (선택사항)
  - ex) ?query=keyword, ?query=keyword&page=2

각 역할을 살펴봤을 때 아래는 실제 url의 예시이다.

```http
https://developer.mozilla.org/en-US/search?q=URL
```

위 URL을 해석하면 `https` **프로토콜**을 이용하고, `developer.mozilla.org`의 이름을 갖는 **컴퓨터(서버)** 에서 `en-US/search` **문서**에서 `q`라는 **파라미터**에 `URL`이라는 **값**을 전달한다.

### 1.2. DNS (Domain Name Server)

DNS는 숫자로 돼있는 IP주소(ex 123.456.789)를 우리가 기억하기 쉽게 문자(ex google.com)로 매핑해주는 시스템이다.

URL을 표시할 때 해당 Resource가 존재하는 위치에 접근하려면 원래 숫자로 돼있는 IP 주소로 접근해야 한다. 하지만 DNS를 통해 우리가 익숙히 아는 문자 주소로 접근할 수 있는것이다.

DNS의 동작 원리는 사용자가 접근하려는 IP의 Domain name을 요청하면 DNS를 통해 IP주소로 리다이렉팅시켜 사용자가 해당 IP에 접근할 수 있게 하는 것이다.

예를 들어 유저가 `google.com`으로 가는 IP주소를 몰라도 도메인 이름인 `google.com`을 입력해서 해당 사이트에 접근할 수 있다.

## 2. HTTP (Hyper Text Transfer Protocol)

HTTP는 인터넷상에서 데이터를 주고 받기 위한 서버/클라이언트 모델을 따르는 프로토콜이다. 여기서 프로토콜은 통신 규악을 의미한다.

HTTP는 애플리케이션 레벨의 프로토콜이고, TCP/IP 위에서 작동한다.

HTTP로 보낼 수 있는 데이터는 HTML문서, 이미지, 동영상, 오디오, 텍스트 문서 등 여러 종류가 존재한다.

### 2.1. HTTP 요청

HTTP 요청은 한 컴퓨터가 뭔가 전달하기 위해 다른 컴퓨터로 보내는 **정보 패킷** 이다.
실제 사용을 예로 들면 클라이언트가 서버로 보내는 이진 데이터 패킷이다.

HTTP 요청은 다음과 같은 부분을 포함한다.

- 요청(Request) 라인, 요청 라인에는 `요청 형식(method)`, `url`, `HTTP version`이 포함된다.
  - 여기서 version 이 중요한데, 이유는 클라이언트와 서버 모두 이해 가능한 버전으로 맞추어 호환하기 때문이다.
  - ex) `Request Line: GET /item HTTP/1.1`
- 요청에 0개 이상의 요청 헤더(header)
- 요청의 선택적(optional) 본문(body)

HTTP 4가지 요청 형식(method)은 아래와 같다.

- GET : 문서를 요청. 서버가 클라이언트에 상태 정보와 복제된 문서를 보냄으로써 응답을 함. (조회)
- POST : 데이터를 서버로 송신. 서버는 해당 데이터를 특정 아이템에 덧붙인다. (생성)
- PUT : 데이터를 서버로 송신. 서버가 특정 아이템을 완전히 대체한다. (수정)
- DELETE : 데이터 삭제를 요청. 서버가 특정 아이템을 삭제한다. (삭제)

### 2.2. HTTP GET 요청 동작과정

URL 에 사이트 주소를 입력하고 확인을 누르면, 브라우저에서 GET 요청으로 서버에 페이지를 요청한다. GET 요청을 받은 서버에서는 응답 헤더, 빈 줄, 요청한 문서를 클라이언트로 보낸다. 이 때 GET 의 요청 형식은 다음과 같다.

```http
GET /item version CRLF
```

위 형식을 해석해보면,

- item : 요청한 문서의 URL
- version : 프로토콜의 버전을 의미. 보통은 HTTP/1.0 이나 HTTP/1.1 이다.
- CRLF : 텍스트 줄의 끝을 의미하는 2 개의 아스키 코드를 의미 (Carriage Return : 커서를 행의 맨 좌측 이동, Line Feed : 커서를 다음 행으로 이동)

### 2.3. HTTP 응답 헤더

HTTP 응답 헤더의 일반적인 형태는 아래와 같다.

```http
HTTP/1.0 status_code status_string CRLF
Server: server_identification CRLF
Last-Modified : date_document_was_changed CRLF
Content-Length : datasize CRLF
Content-Type : document_type CRLF
CRLF
```

위 형식을 해석해보면,

- status_code : 상태를 나타내는 숫자 값
- status_string : 사람이 식별 가능한 상태 문자 값
- server_identification : 서버정보 설명
- datasize : 데이터의 크기 (바이트 단위)
- document_type : 문서 유형 (html 문서는 text/html, jpeg 파일은 image/jpeg)

> HTTP 요청, 응답 헤더는 `브라우저 검사도구 - Network - Fetch/XHR - Headers` 에서 확인할 수 있다.

## 3. 다양한 프로토콜 종류

### 3.1. FTP (File Transfer Protocol)

브라우저에서 파일을 다운로드 받을 때 사용하는 FTP 프로토콜이다.
파일이 문서, 이미지, 프로그램 등 다양한 형태의 데이터를 갖고 있을 수 있기 때문에 컴퓨터 간의 파일 교환시에 호환성을 보장하는 프로토콜이 필요하다. 컴퓨터 간의 호환성이라는 것은 예를 들어, 한 컴퓨터에서는 JEPG 이미지가 `.jpg`로 저장되지만 다른 컴퓨터에서는 `.jpeg`로 저장될 수 있다. 또한 어떤 컴퓨터는 파일 경로를 탐색할 때 `/`를 사용하지만 다른 컴퓨터는 `\`를 사용할 수도 있다. 이렇기 때문에 파일 전송에 대한 규약인 프로토콜을 이용해 상호 컴퓨터간에 파일 전송이 가능하다.

FTP의 특성은 다음과 같다.

- 어떤 형태의 데이터든 전송이 가능하다.
- 파일을 다운로드 & 업로드 할 수 있다.
- 파일에 대한 권한을 설정할 수 있다.
- ASCII 문자로 메시지가 교환된다.
- 파일을 검색하고 조회할 수 있다.

### 3.2. SMTP (Simple Mail Transfer Protocol)

메일 전송 프로그램이 서버로 메일을 보낼 때 사용하는 프로토콜이다.
오직 텍스트만 전송이 가능한 것이 특징이고, 스트림 방식을 이용하여 전송한다. SMTP는 한 개의 메시지를 해당 서버의 여러 수신자에게 보낼 수 있다는 특징이 있다.

### 3.3. MIME (Multi-purpose Internet Mail Extensions)

SMTP 로 전송시 이메일에 텍스트 밖에 포함하지 못하는 단점을 보완하여, 메시지 안에 텍스트 이외의 데이터를 전송할 수 있는 프로토콜이다. 즉, MIME 은 이메일 메시지 안의 헤더에 추가 정보를 포함하여 비 텍스트 형의 데이터가 전송될 수 있도록 하는 프로토콜이다.
또한 첨부된 데이터는 출력 가능한 형태의 문자열로 인코딩 되어 있고, 각 첨부 앞에 separator 로 구분되어 있다.

## 4. 참고 자료

- [캡틴판교 - 웹 개발자를 위한 Web Protocols 정리](https://joshua1988.github.io/web-development/web-protocols/)
- [MDN - HTTP 개요](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)
