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

* Node.js는 단순한 서버가 아니라, JavaScript 실행 환경(런타임)으로 인식하는게 맞다고 생각한다.

일반적으로 php나 java 같은 언어를 사용하기 위해서는 Apache, NginX, Tomcat 같은 서버가 필요한데, Node.js는 내장 HTTP 라이브러리가 있어 별도의 웹 서버 없이 동작하는 것이 가능하다.

---

## 2. Node.js 핵심구조

<pre>V8 Engine + Libuv library</pre>

### 2.1. V8 javascript engine
구글에서 개발한 오픈소스 JavaScript 엔진   
V8 엔진을 통해 Node.js는 JavaScript를 인식한다.(크롬 브라우저도 JavaScript 처리 엔진으로 V8을 사용함)

### 2.2. Libuv library
Non-blocking I/O 처리를 위해 이벤트 루프를 제공한다.   
한마디로 Node.js의 비동기 처리는 이 라이브러리를 통해 이루어지고 있다.

(Node.js에서는 이 Non-blocking 개념이 꽤나 중요한 것 같다.)

---

## 3. 싱글 스레드? Non-blocking? 이벤트 루프?
여러 글을 읽어보고 종합해보자면
<pre>
Node.js는 싱글 스레드 기반 Non-blocking I/O를 지원하는 런타임 환경
</pre>

런타임 환경은 알겠는데, 싱글 스레드가 어쨌고 Non-blocking은 무슨 소리인지 이해가 안가더라.

### 3.1. 싱글 스레드

엄밀히 따지면 V8엔진과 Libuv는 각각 다른 스레드**를 사용하고 있기 때문에 싱글 스레드가 아니다.
단지 V8 엔진의 콜 스택에서 하나의 스레드를 사용하고 있기 때문에 싱글 스레드 기반이라고 하는 것 같다.

** 스레드란? 기본적으로 CPU의 코어 당 한 번에 업무를 담당하여 처리할 수 있는데, 이 코어를 논리적으로 2개로 나눈 기술이 Intel의 Hyper Threading 기술이다.

** 예를 들어, 4개의 코어를 가지고 있는 CPU가 있다면, Hyper Threading 기술로 8개의 코어가 있는 것처럼 동작하는 것이다.(OS에서도 8개의 코어가 있는 것으로 인식한다)

** Amd는 SMT라고 부른다.

### 3.2. Non-blocking
