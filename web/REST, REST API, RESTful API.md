# REST

## REST 개념

REpresentational State Transfer의 약자

월드 와이드 웹(www)과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식

REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일

REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나

한마디로 웹의 장점을 살려 활용하기 위한 하나의 네트워크 기반 어플리케이션 아키텍처 스타일

> 💡 아키텍처 스타일?  
> 스타일을 따르는 아키텍처가 지켜야하는 제약조건들의 집합

## REST 구성

자원 (Resource) : URI

- 모든 자원에 고유한 ID 존재, 자원은 Server에서 관리
- 자원을 구별하는 ID는 HTTP URI다. ([identification of resources](https://www.notion.so/REST-REST-API-RESTful-API-d2252b4b8d864208bcca05513512eba7))

행위 (Verb) : HTTP Method

- Http 프로토콜의 메소드 사용 ( GET, POST, PUT, DELETE, HEAD )

표현 (Representations)

- Client가 자원의 상태(정보)에 대한 조작을 요청하면 
Server는 이에 대한 적절한 응답(Representation)을 보낸다.
- 자원은 **JSON, XML, TEXT, RSS** 등 여러 형태의 Representation으로 나타낼 수 있음
- JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.

## REST 특징 6가지

Client-Server
- 클라이언트 - 서버 스타일은 사용자 인터페이스에 대한 관심(concern)을 데이터 저장에 대한 관심으로부터 분리함으로써 클라이언트의 이식성과 서버의 규모확장성을 개선한다.
    
Stateless    
- 클라이언트와 서버의 통신에는 상태가 없어야한다. 모든 요청은 필요한 모든 정보를 담고 있어야한다. 요청 하나만 봐도 바로 뭔지 알 수 있으므로 가시성이 개선되고, task 실패시 복원이 쉬우므로 신뢰성이 개선되며, 상태를 저장할 필요가 없으므로 규모확장성이 개선된다.
    
Cache
- 캐시가 가능해야한다. 즉 모든 서버 응답은 캐시 가능한지 그렇지 아닌지 알 수 있어야한다. 호율, 규모확장성, 사용자 입장에서의 성능이 개선된다.
    
Uniform Interface
- 구성요소(클라이언트, 서버 등) 사이의 인터페이스는 균일(uniform)해야한다. 인터페이스를 일반화함으로써, 전체 시스템 아키텍처가 단순해지고, 상호작용의 가시성이 개선되며, 구현과 서비스가 분리되므로 독립적인 진화가 가능해진다.
- 이 스타일은 다음의 네 제약조건으로 이루어진다:  
  identification of resources, manipulation of resources through representation, self-descriptive messages, hypermedia as the engine of application state
    
    > 💡 **identification of resources**
    > 자원을 식별할 수 있어야 하고 어떤 자원에 접근하는 지 명시해야 함
    > ****즉, URI를 통해서 자원을 식별할 수 있어야 한다.
    > *예)
    > 회원 등록 = POST /register-member (X) ⇒ POST /members
    > 회원 리스트 조회 = GET /view-member-list (X) ⇒ GET /members
    > 단일 회원 조회 = GET /view-member-by-id (X) ⇒ GET /members/{id}*
    > 
    > **manipulation of resources through representation**
    > 표현을 통한 자원 조작
    > ****HTTP 메소드를 통해 자원을 어떻게 조작하는 것인지 명시 (GET, POST, PUT …)
    > 
    > **self-descriptive messages**
    > URI + Method 만 보고도 어떤 기능을 하는지 파악 가능
    > 
    > **hypermedia as the engine of application state**
    > HATOAS, state는 Hyperlink를 통해 전달 되어야 함
    > 즉, 서버는 다른 사용 가능한 작업에 대해 하이퍼링크를 포함하여 응답해야 함
    
Layered System
- 계층(hierarchical layers)으로 구성이 가능해야하며, 각 레이어에 속한 구성요소는 인접하지 않은 레이어의 구성요소를 볼 수 없어야한다.
    
Code-On-Demand (Optional)    
- Code-On-Demand가 가능해야한다. 서버가 네트워크를 통해 클라이언트에 프로그램을 전달하면 그 프로그램이 클라이언트에서 실행될 수 있어야한다. (Java applet이나 Javascript 같은 것을 말함) 다만 이 제약조건은 필수는 아니다.
    

---

# REST API

## 정의
REST를 기반으로 API를 구현한 것
최근에는 Open API (무료로 공개된 API), MSA (여러 개의 작은 어플리케이션으로 쪼개서 만드는 아키텍처)등 다양한 곳에서 대부분 REST API를 제공한다.

## 특징
REST를 기반으로 제작해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 함
REST는 HTTP 표준 기반이므로,  HTTP를 지원하는 프로그램 언어로 클라이언트, 서버 구현
⇒ 클라이언트, 서버를 서로 간섭받지 않고 다양한 언어로 구현할 수 있다.

## 설계 규칙  
슬래시 구분자(/ )는 계층 관계를 나타내는데 사용한다.  
- Ex) `http://restapi.example.com/houses/apartments` 
<br/>

URI 마지막 문자로 슬래시(/ )를 포함하지 않는다.  
- URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다.  
- REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.
- Ex) `http://restapi.example.com/houses/apartments/ (X)`
<br/>

하이픈(- )은 URI 가독성을 높이는데 사용  
- 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높인다.
<br/>

밑줄(_ )은 URI에 사용하지 않는다.  
- 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 하므로 가독성을 위해 밑줄은 사용하지 않는다.
<br/>

URI 경로에는 소문자가 적합하다.  
- URI 경로에 대문자 사용은 피하도록 한다.
- RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문
<br/>

파일확장자는 URI에 포함하지 않는다.  
- REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다.
- Accept header를 사용한다.
- Ex) `http://restapi.example.com/members/soccer/345/photo.jpg (X)`
- Ex) `GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg (O)`
<br/>

리소스 간에는 연관 관계가 있는 경우  
- /리소스명/리소스 ID/관계가 있는 다른 리소스명
- Ex) `GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)`
<br/>

:id는 하나의 특정 resource를 나타내는 고유값  
- Ex) student를 생성하는 route: POST /students
- Ex) id=12인 student를 삭제하는 route: DELETE /students/12
<br/>

---

# RESTful API

### 정의

REST를 충실하게 지킨 API를 의미한다.

REST의 원리를 따르는 시스템은 RESTful하다고 할 수 있다.

### 목적

이해하기 쉽고, 직관적으로 사용할 수 있는 REST API를 만드는 것

하지만 RESTful API는 퍼포먼스 향상이 목적이 아니며, 일관적인 컨벤션을 통해 API의 이해도 및 호환성을 높이는게 주 목적이다. 따라서 퍼포먼스가 중요한 상황에서는 굳이 RESTful API로 만들 필요는 없다.

### 참고

[REST API 제대로 알고 사용하기 : NHN Cloud Meetup](https://meetup.nhncloud.com/posts/92)

[REST의 representation이란 무엇인가](https://blog.npcode.com/2017/04/03/rest의-representation이란-무엇인가/)
