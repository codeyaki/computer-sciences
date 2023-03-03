# **HTTP(HyperText Transfer Protocol)**

하이퍼텍스트 문서 간 링크를 통해 전송

HTTP 메시지에 모든 것을 전송한다

-   HTML, TEXT
-   IMAGE, 음성, 영상, 파일
-   JSON, XML(API)
-   거의 모든 형태의 데이터 전송 가능함
-   서버 간에 데이터를 주고받을 때도 대부분 HTTP 사용한다.

## **역사**

-   HTTP/0.9 (1991년): GET 메서드만 지원, HTTP 헤더 X
-   HTTP/1.0 (1996년): 메서드, 헤더 추가
-   HTTP/1.1 (1997년): 가장 많이 사용하는 버전 - **TCP 사용**  
    \- RFC2068 (1997) > RFC2616(1999) > RFC7230~7235(2014)
-   HTTP/2 (2015년): 성능 개선 - **TCP사용**
-   HTTP/3 (2020년~): TCP대신 **UDP사용**

## **특징**

-   클라이언트 서버 구조
-   무상태 프로토콜(스테이스 리스), 비연결성
-   HTTP 메시지
-   단순함, 확장 가능함.

#### 1\. 클라이언트 서버 구조

-   Request Response 구조
-   클라이언트는 서버에 요청, 응답을 대기
-   서버가 요청에 대한 결과를 만들어서 응답
-   클라이언트와 서버를 분리했기 때문에 각각 발전이 가능(클라이언트는 UI 관련, 서버는 비즈니스 로직 관련)  
    서로 변경하여도 영향을 주지 않는다.

#### 2\. 무상태 프로토콜 (스테이스 리스, Stateless)

-   stateful은 상태를 보관한다. 서버가 바뀔 경우 상태가 초기화된다. 따라서 같은 서버로만 응답을 해야 한다.
-   무상태 프로토콜(stateless)은 서버에 클라이언트의 상태를 저장하지 않는다.
-   상태를 관리하지 않기 때문에 클라이언트가 급격히 증가해도 서버를 증설하기 쉽다.
-   한계  
    \- 모든 것을 무상태로 설계할 수 없는 경우도 있다.  
    예) 로그인한 사용자의 경우 로그인했다는 상태를 서버에 유지시켜야 함.  
     >> 쿠키와 세션 등을 사용해서 상태를 유지한다.  
    \- 많은 데이터를 전송해야 한다.
-   상태 유지는 최소한으로 사용하는 것이 좋다.

#### 3\. 비 연결성(connectionless)

-   연결을 유지하는 모델은 모든 클라이언트와 연결을 유지해야 한다. 최초 요청으로 연결 후 요청이 없어도 일정 시간 연결을 유지한다.  
    즉, 불필요한 자원이 많이 소모된다.
-   반면 HTTP는 요청, 응답을 주고받을 때만 연결을 잠깐 하여 불필요한 자원 소모를 줄일 수 있다.
-   일반적으로 초 단위 이하의 빠른 속도로 응답한다.
-   1시간 동안 수천 명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십 개 이하로 매우 작다.
-   따라서 서버 자원을 매우 효율적으로 사용할 수 있다.
-   한계  
    \- TCP/IP 연결을 매번 새로 맺어야 한다. >>> 3 way handshake 시간이 추가된다.  
    \- 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 추가 이미지 등 수많은 자원이 함께 다운로드된다.  
    \- 현재는 HTTP 지속 연결(Persistent Connections)로 문제 해결  
    \- HTTP/2, HTTP/3에서 더 많은 최적화.

---

## **HTTP 메시지**

##### 구조(RFC7230)

### **1\. start-line (시작 라인)**

-   start-line = request-line(요청) / status-line(응답)

#### request-line(요청)

-   **request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)**
-   HTTP method(메서드)  
    \- 종류 : GET, POST, PUT, DELETE...  
    \- 서버가 수행해야 할 동작을 지정
-   request-target  
    \- absolute-path\[?query\] (절대 경로\[? 쿼리)  
    \- 절대 경로: "/"로 시작하는 경로  
    (참고: \*, http://...?x=y 와 같이 다른 유형의 경로 지정 방법도 있음)
-   HTTP-version

#### status-line(응답)

-   **status-line = HTTP-version SP status-code SP reason-phrase CRLF (SP:공백 문자)**
-   HTTP-version
-   status-code (상태 코드)  
    \- 200: 성공  
    \- 400: 클라리언트 요청 오류  
    \- 500: 서버 내부 오류
-   reason-phrase (이유 문구)  
    \- 간단한 설명 문구(사람이 이해하도록 도움)

### **2\. header (헤더)**

-   **header-field = field-name":" OWS field-value OWS (OWS: 띄어쓰기 허용)**
-   filed-name은 대소문자 구분 없음
-   HTTP 전송에 필요한 모든 부가정보  
    예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청, 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보...
-   표준 헤더가 많음
-   필요시 임의의 헤더 추가 가능

### **3\. empty line (공백 라인, CRLF)**

-   필수적으로 한 줄의 공백 라인을 넣어야 한다.

### **4\. message body (메시지)**

-   실제 전송할 데이터
-   HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능

ex) HTTP 요청 메시지

| GET /search?q=hello&hl=ko HTTP/1.1   host: [www.google.com](http://www.google.com/)                                                      |
| --- |

HTTP 응답 메시지

| HTTP/1.1 200 OK   Content-Type: text/html;charset=URF-8   Content-Length: 3423                                                         <html>       <body> ... </body>   </html> |
| --- |

---
