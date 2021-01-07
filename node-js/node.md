# Node.js

## 1. Node.js 란?
<pre>
JavaScript로 확장성 있는 네트워크 애플리케이션 개발에 사용되는 소프트웨어 플랫폼이다. (출저 wiki)
</pre>

기존 JavaScript는 브라우저에서 웹 페이지가 동작하는 것 즉, Front-End의 영역이었지만, Node.js로 Back-End 개발이 가능하다.

Node.js를 서버 구축 등의 코드를 실행할 수 있게 해주는 런타임 환경(Runtime Environment)* 이라고도 하는데, 이 표현이 정확한 듯 하다.

* 런타임 환경(Runtime Environment)   
컴퓨터가 실행되는 동안 프로세스나 프로그램을 위한 SW 서비스를 제공하는 가상 머신의 상태, OS 자체에 속하는 경우도 있고 OS에서 동작하는 SW를 뜻할 수도 있다.(출저: wiki)

* 한 마디로, 프로그래밍 언어가 구동되는 환경이다. JavaScript의 측면에서 런타임은 Node.js(혹은 Browser)라는 뜻   
Node.js의 측면에서 런타임은 Node.js를 설치한 PC

일반적으로 php나 java 같은 언어를 사용하기 위해서는 Apache, NginX, Tomcat 같은 서버가 필요한데, Node.js는 내장 HTTP 라이브러리가 있어 별도의 웹 서버 없이 동작하는 것이 가능하다.

---

## 2. Node.js 구조

<pre>V8 Engine + libuv</pre>

### 2.1. V8 Engine
구글에서 개발한 오픈소스 JavaScript 엔진, 크롬 브라우저도 JavaScript 처리 엔진으로 V8을 사용한다.

### 2.2. Libuv
이벤트 루프 라이브러리