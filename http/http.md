# HTTP
_Hyper Text Transfer Protocol, 웹 페이지 전송 규약_   
즉, 웹 페이지를 전송하기위해 고안 된 통신 규약이다.

웹 브라우저에서(클라이언트) 웹 서버로 요청을 하거나 응답을 받는데 이 정보들을 **HTTP 메세지**라고 한다.

## 1. HTTP Message
> GET https://github.com HTTP/1.1   
> User-Agent: Mozilla/5.0 ...   
> Upgrade-Insecure-Requests: 1   
> (본문)

시작줄
> GET https://github.com HTTP/1.1

헤더
> User-Agent: Mozilla/5.0 ...   
> Upgrade-Insecure-Requests: 1   

그리고 마지막으로 본문으로 구성된다.

---

## 2. HTTP Method
- **GET** : 웹 서버에 해당 주소로 요청을 보낼 때 사용하는 메서드
- **POST** : 예를 들어, 게시글을 작성하거나 할 때 사용하는 메서드
- **PUT** : 전체 수정
- **PATCH** : 부분 수정
- **DELETE** : 제거 요청
- **OPTIONS** : OPTIONS 요청 시 요청한 주소에서 지원하는 메서드 응답(GET, POST 등), 서버가 어떤 메서드를 지원하는지 알아볼 때 사용
- **HEAD** : HEAD 요청 시 응답 HTTP Message의 헤더 정보만 가져옴
- **CONNECT**
- **TRACE**

REST는 주소를 자원이라고 보고, 메서드를 동사라고 보는 개발 방식

---

## 3. 공통 헤더
요청과 응답 모두 사용되는 헤더, Content 시리지는 엔티티 헤더라고 함.

- **Date**   
HTTP Message가 만들어진 시각

- **Connection**   
기본적으로 Keep-alice로 되어 있는데 의미 없음   
HTTP/2 에서 사라짐

- **Cache-Control**

- **Content-Length**   
요청/응답 본문 크기를 바이트로 표시

- **Content-Type**   
콘텐츠 타입(MIME)과 문자열 인코딩을 명시할 수 있음   
Accept 헤더, Accept-Charset 헤더와 대응

- **Content-Encoding**   
콘텐츠 압축 방식, 용량이 줄어들기 때문에 권장(요청/응답 전송 속도 증가, 데이터 소모량 감소)

---

## 4. Request Header

- **Host**   
서버와 도메인 네임(포트 포함)으로 구성, 반드시 하나는 존재

- **User-Agent**   
사용자 클라이언트(OS, Browser 정보 등) 정보 표시   
헤더 정보는 변경 가능하기 때문에 무조건적인 신뢰는 위험   
하지만 대부분 일반 사용자는 조작하지 않기 때문에 접속자 통계 등에서 활용

- **Accept**   
Request를 보낼 때 해당 타입(MIME)을 요청할 때 사용   
예를 들어, text/html(HTML 형식 응답을 처리)   
콤마로 여러 타입을 동시에 적용: image/png, image/gif, text/*   
와일드카드 적용 시 모두 받곘다는 의미: text/*

- **Authorization**   
인증 토큰을 서버로 보낼 때 사용하는 헤더, 주로 API 요청에 사용   
보통 "Basic" 또는 "Bearer" 종류의 토큰을 알리고 토큰 명시

- **Origin**   
POST 메서드 같은 요청의 시작 주소   
예를 들어, 폼 작성 페이지의 주소가 Origin이 됨   
요청을 보낸 주소가 받는 주소가 다르면 **CORS 문제 발생**

- **Refere**   
이전에 접속한 페이지의 주소   

---

## 5. Response Header

- **Access-Control-Allow-Origin**   
요청 프론트엔드 주소에서 받는 백엔드 주소가 서로 다르면 CORS Error 발생   
이 헤더에 프론트엔드 주소를 적어 주어야 됨   
프로토콜, 서브도메인, 도메인, 포트 중 하나만 달라도 CORS Error 발생

- **Allow**   
Access-Control-Allow-Methods와 비슷하지만, CORS 요청 외에도 적용 된다는 점에서 차이가 있음   
즉, GET 요청은 가능하나 POST 요청은 허용하지 않는 경우   
405 Method Not Allowed 에러를 응답하면서 헤더로 "Allow: GET"을 응답하면 됨(GET 요청만 받겠다는 의미)

- **Content-Disposition**   
응답 본문을 브라우저가 어떻게 표시해야 할지 알려주는 헤더   
inline 경우 웹 페이지 화면에 표시   
attachment 경우 다운로드   
다운로드 되길 원하는 파일은 attachment 값 설정, filename 옵션으로 파일명까지 지정 가능   
파일용 서버인 경우 자주 사용하는 태그

- **Location**   
300 응답이나 201 Created 응답일 때 어느 페이지로 이동할지 알려주는 헤더   
HTTP/1.1 302 Found   
Location: /   
이런 응답이 왔다면 브라우저는 / 주소로 redirect

- **Content-Security-Policy**   
다른 외부 파일들을 불러오는 경우, 차단할 소스와 불러올 소스를 명시할 수 있음(js, stylesheets, font 등)   
XSS 같은 해킹을 방지하기 위해 허용할 외부 소스만을 지정   
default-src 'self' (자신의 도메인 파일만 혀용)   
default-src https: (https를 통해서만 파일을 가져올 수 있음)   
default-src 'none' (가져올 수 없음)   
그 밖에 옵션들
https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy

---

## HTTP Cookie & Cache header

웹 자원을 효율적으로 쓰기 위해서는 ***캐싱***이 중요, 같은 데이터를 계속해서 내려 받을 필요가 없기 때문

***쿠키***는 프론트엔드와 백엔드 간 데이터를 주고 받는 가장 간단한 방법 중 하나

---

### Cache

보통 캐싱은 GET 요청에 사용, 일반적으로 200(성공), 301(다른 주소로 이동 후 가져옴), 404(가져올 게 없음) 상태 코드로 온 응답을 캐싱할 수 있음

- Cache-Control
    - Cache-Control: no-store   
    아무것도 캐싱하지 않음   
    no-cache, no-store, must-revalidate로 'no' 시리즈를 붙여 사용

    - Cache-Control: no-cache   
    모든 캐시를 쓰기 전에 서버에 확인

    - Cache-Control: must-revalidate   
    만료된 캐시만 서버에 확인

    - Cache-Control: public (or private)   
    public이면 공유 캐시(또는 중개 서버)에 저장 가능   
    private이면 특정 사용자 환경에만 저장 가능

    - Cache-Control: public, max-age=3600   
    max-age로 캐시 유효 시간을 줄 수 있음(초 단위)

옵션들은 혼합해서 상용 가능(콤마로 구분)   
Cache-Control은 응답/요청으로 둘 다 헤더로 사용 가능

- Age   
캐시 응답 때 나타나는데, max-age 시간 내에서 얼마나 흘렀는지 초 단위로 알려줌

- Expires   
Cache-Control과 별개로, 응답 컨텐츠가 언제 만료되는지 나타냄   
max-age가 있을 경우 이헤더는 무시 됨

- ETag   
HTTP 컨텐츠가 바뀌었는지 검사할 수 있는 태그   
같은 주소(자원)의 응답 본문이 달라졌다면 ETag 헤더 값도 변경되어, 이를 기반으로 캐시를 지우고 새로 컨텐츠를 내려받을 수 있게 할 수 있음

- If-None-Match   
서버에서 ETag가 달라졌는지 검사, 헤더 값이 다를 경우에만 컨텐츠를 새로 받음   
만약 ETag가 같다면 서버는 304 Not Modified를 응답, 캐시를 그대로 사용

---

### Cookie

브라우저에 저장되는 작은 데이터 조각으로, 임시 데이터 보관 또는 웹 페이지 개인화 등에 사용

- Set-Cookie   
서버에서 브라우저에 쿠키를 저장하는 명령으로 응답 헤더   
Set-Cookie: key=value; options...   

    - Expires: 쿠키 만료 날짜
    - Max-Age: 쿠키 수명(Expires는 무시)
    - Secure: https에서만 쿠키 전송
    - HttpOnly: 자바스크립트에서 쿠키 접근 금지, XSS 요청을 막으려면 활성화 추천
    - Domain: 도메인이 일치하는 요청에서만 쿠키 전송, 도메인이 다른 쿠키의 경우 써드 파티 쿠키로 사용자를 추적하고 있는 쿠키
    - Path: 패스와 일치하는 요청에서만 쿠키 전송

예를 들면,

Set-Cookie: key=value; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly

쿠키는 XSS, CSRF 공격 등에 취약하기 떄문에 HttpOnly 옵션을 사용, 백 엔드에서 검증하는 로직을 꼭 마련해두는 것이 좋음

- Cookie   
클라이언트 -> 백엔드 쿠키를 보낼 때 이 요청 헤더에 담아 보냄   
Cookie: key=value; key2=value2; ...   
서버는 이 쿠키 헤더를 파싱해서 사용

---

## HTTP X Header

사용자가 임의로 정의한 헤더라는 의미로 prefix로 X-를 사용(2012년 임의라는 의미는 사라짐)

X- 규칙은 사라졌지만 아직 몇몇 헤더들은 사용 중, 대표적으로 아래와 같음

### X-Forwarded

- X-Forwarded-For
- X-Forwarded-Host
- X-Forwarded-Proto

요청이 어디서부터 건너왔는지 알려주는 헤더   
실제 클라이언트(요청) - 서버(응답)와 같은 2단 구조보다는   
클라이언트(요청) - 중개서버 - 중개서버 - ... 이런 다단 구조가 더 많기 때문에   
헤더들이 변조되고, 요청을 어디서 보냈는지 애매해짐

X-Forwarded 헤더 시리즈는 원래 요청이 어디서 왔는지 밝혀 줌

> X-Forwarded-For: 1.2.3.4, 5.6.7.8, 9.10.11.12

For는 현재까지 거쳐온 서버의 IP에 대한 정보를 콤마로 구분하여 나타냄   
1.2.3.4가 원래 IP라면 나머지는 중개서버 IP가 됨

> X-Forwarded-Host: github.com

Host는 원래 서버의 호스트명

> X-Forwarded-Proto: https

Proto는 원래 서버의 프로토콜

사실 Forward 헤더는 표준으로, 위 세 가지를 모두 처리할 수 있음

> Forwarded: for=1.2.3.4; host=github.com; proto=https; by=5.6.7.8, 9.10.11.12

### X-Frame-Options

frame, iframe, object 태그 안에서 페이지를 렌더링하는 것을 막을 수 있음   
프레임 태그를 쓰지 않는다면 아래와 같은 옵션으로 막아두는 것이 보안에 좋음
> X-Frame-Options: DENY

클릭재킹(내가 무언가를 눌렀는데 실제로는 다른게 눌리는 해킹 방법)을 방지

만약 사이트 자체를 iframe 등으로 불러오는 경우에는

> X-Frame-Options: SAMEORIGIN

으로 자신의 페이지를 불러오는 것은 허용할 수 있음   
특정 사이트를 불러오는 것 만 허용한다면

> X-Frame-Options: ALLOW-FROM https://github.com

### X-Content-Type-Options

서버에서 보내온 Content-Type 헤더가 잘못 되었다고 판단되는 경우, 브라우저 자체에서 컨텐츠 타입을 추론   
예를 들어, css 파일이지만 Content-Type 헤더가 text/html인 경우,   
브라우저 자체적으로 text/css로 추론할 수 있음

하지만 이런 임의적 행동은 예상치 못한 행동이기 때문에 위험할 수 있음

> X-Content-Type-Options: nosniff

브라우저가 서버가 보낸 컨텐츠 타입을 따르도록 강제하는 헤더의 옵션