## **HTTP 메서드**

HTTP API를 만든다고 가정해보자.

따라서 회원 정보 관리 API를 만들어 보았다.

-   회원 목록 조회 (/read-member-list)
-   회원 조회 (/read-member-by-id)
-   회원 등록 (/create-member)
-   회원 수정 (/update-member)
-   회원 삭제 (/delet-member)

해당 방법처럼 만드는 경우가 있는데 위의 방법은 좋지 않은 방법이다.

#### **URI는 리소스 식별!!, URI 계층 구조를 활용해야 한다.**

-   리소스란?  
    \- 회원을 등록하고 수정하고 조회하는 것이 리소스가 아님.  
    \- 회원이라는 개념 자체가 바로 리소스
-   리소스를 식별하는 방법  
    \- 회원을 등록하고 수정하고 조회하는 것을 모두 배제  
    \- 따라서 회원이라는 리소스만 식별하면 된다. -> 회원 리소스를 URI에 매핑

이 내용을 토대로 회원 정보 관리 API의 URI를 만들면

-   회원 목록 조회 (/members)
-   회원 조회 (/members/{id})
-   회원 등록 (/mebers/{id})
-   회원 수정 (/members/{id})
-   회원 삭제 (/members/{id})

하지만 해당 방법으로 만들면 조회, 등록, 수정, 삭제를 구별할 수가 없는 것처럼 보인다.

이를 해결하기 위해 메서드를 사용해야 한다.

#### **행위(동작)를 구분하기 위해서는 메서드를 사용하자.**

-   URI는 리소스만 식별
-   리소스와 해당 리소스를 대상으로 하는 행위를 분리  
    \- 리소스: 회원  
    \- 행위: 조회, 등록, 삭제, 변경
-   리소스는 명사, 행위는 동사
-   메서드(행위)를 구별하기 위해서 GET, POST를 사용한다

### **주요 메서드**

-   **GET**: 리소스 조회
-   **POST**: 요청 데이터 처리, 주로 등록에 사용
-   **PUT**: 리소스를 대체, 해당 리소스가 없으면 생성
-   **PATCH**: 리소스 부분 변경
-   **DELETE**: 리소스 삭제

### **기타 메서드**

-   **HEAD**: GET과 동일하지만 메시지 부분을 제외, 상태 줄과 헤더만 반환.
-   **OPTIONS**: 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명. (주로 CORS에서 사용)
-   **CONNECT**: 대상 지원으로 식별되는 서버에 대한 터널을 설정.
-   **TRACE**: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행.

#### **1\. GET**

-   **리소스 조회에 주로 사용**
-   서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달.
-   메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음.

#### **2\. POST**

-   **요청 데이터 처리**
-   메시지 바디를 통해 서버로 요청 데이터 전달
-   서버는 요청 데이터를 처리  
    \- 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행함.
-   주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용
-   스펙: POST 메서드는 대상 리소스가 리소스의 고유한 의미 체계에 따라 요청에 포함된 표현을 처리하도록 요청합니다.  
    1\. HTML 양식에 입력된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공  
      _예) HTML, FORM에 입력한 정보로 회원가입, 주문 등에서 사용_  
    2\. 게시판, 뉴스, 그룹, 메일링 리스트, 블로그 또는 유사한 기사 그룹에 메시지 게시  
      _예) 게시판 글쓰기, 댓글 달기_  
    3\. 서버가 아직 식별하지 않은 새 리소스 생성  
      _예) 신규 주문 생성_  
    4\. 기존 자원에 데이터 추가  
      _예) 한 문서 끝에 내용 추가하기._  
    즉, 이 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함.  
        -----> 정해진 것이 없음

-   **정리  
    ****1\. 새 리소스 생성(등록)  
    ****2\. 요청 데이터 처리**  
        **- 단순히 데이터를 생성, 변경을 넘어 프로세스를 처리해야 하는 경우 (컨트롤 URI)**  
        **_(예 - 주문에서 결제 완료 > 배달 시작 > 배달 완료로 변경되는 것과 같이 프로세스의 상태가 변경되는 경우)_****3\. 다른 메서드로 처리하기 애매한 경우**

#### **3\. PUT**

-   두 가지 동작  
    \- 리소스가 있으면 대체 (주의: 기존 리소스는 삭제되고 전송한 내용이 그대로 저장됨)  
    \- 리소스가 없으면 생성
-   ★★클라이언트가 리소스를 식별★★  
    \- 클라이언트가 리소스 위치를 알고 URI 지정 (POST는 클라이언트가 위치를 모름)
-   ex) /members/100에 { "username": "young", "age": 20 } 리소스가 이미 저장되어 있을 때  
    
    | PUT **/members/100** HTTP/1.1   Content-Type: application/json      {       "age": 50   } |
    | --- |
    
    \- "/members/100"위치를 지정을 해주는 것에 주의  
    \- "/members/100"의 내용이 { "age": 50 }로 변경이 됨. >> 주의!! PATCH과의 차이점.

#### **4\. PATCH**

-   리소스 부분 변경
-   ex) /members/100에 { "username": "young", "age": 20 }이 저장되어 있는 상황에 age의 값만 변경  
    
    | PATCH /members/100 HTTP/1.1   Content-Type: application/json      {       "age": 50   } |
    | --- |
    
    \- age의 값만 50으로 변경이 됨.

#### **5\. DELETE**

-   리소스 제거
-   ex) /member/100 리소스를 제거  
    
    | DELETE /members/100 HTTP/1.1   Host: localhost:8080       |
    | --- |
    

---

### **HTTP메서드 속성**

#### **1\. 안전(Safe Methods)**

-   호출해도 리소스를 변경하지 않는다.  
    (해당 리소스만 고려/ 반복해서 호출하여 발생하는 장애는 고려하지 않는다.)

#### **2\. 멱등(Idempotent Methods)**

-   f(f(x)) = f(x)
-   한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다.
-   멱등 메서드  
    \- **GET**: 한 번 조회하든, 두 번 조회하든 같은 결과가 조회된다.  
    \- **PUT**: 결과를 대체한다. 따라서 같은 요청을 여러 번 해도 최종 결과는 같다.  
    \- **DELETE**: 결과를 삭제한다. 같은 요청을 여러 번 해도 삭제된 결과는 똑같다.
-   활용  
    \- 자동 복구 메커니즘  
    \- 서버가 TIMEOUT 등으로 정상 응답을 못주었을 때, 클라이언트가 같은 요청을 다시 해도 되는가? 에 대한 판단 근거
-   주의)  
    \- 멱등은 외부 요인으로 중간에 리소스가 변경되는 것은 고려하지 않는다.  
    (즉, 중간에 다른 메서드가 포함되지 않는 경우만 고려)

#### **3\. 캐시 가능(Cacheable Methods)**

-   응답 결과 리소스를 캐시 해서 사용 가능
-   캐시 가능 메서드  
    \- GET, HEAD, POST, PATCH  
    ※실제로는 GET, HEAD만 캐시로 사용함. POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데 쉽지 않다.

요약표

![image](https://user-images.githubusercontent.com/96860725/222736760-9c6faf04-4f2e-4322-96b0-af20c8041908.png)

---

## **HTTP 메서드 활용**

### **클라이언트에서 서버로 데이터 전송**

: 데이터 전달 방식은 크게 2가지가 있다.

**1\. 쿼리 파라미터를 통한 데이터 전송**

-   GET
-   주로 정렬 필터를 넣을 때 사용 (검색어)

**2\. 메시지 바디를 통한 데이터 전송**

-   POST, PUT, PATCH
-   회원 가입, 상품 주문, 리소스 등록, 리소스 변경할 때 주로 사용

#### **데이터 전송 4가지 상황**

1.  **정적 데이터 조회 ([https://www.google.com/search)](https://www.google.com/search))**  
    \- 이미지, 정적 텍스트 문서  
    \- 조회 GET 사용  
    \- 정적 데이터는 일반적으로 **쿼리 파라미터 없이** 리소스 경로로 단순하게 조회 가능하다.
2.  **동적 데이터 조회 ([https://www.google.com/search?q=hello&hl=ko)](https://www.google.com/search?q=hello&hl=ko))**  
    \- 주로 검색, 게시판 목록에서 정렬 필터(검색어)  
    \- 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용  
    \- 조회는 GET사용, **쿼리 파라미터 사용**해서 데이터 전달
3.  **HTML Form을 통한 데이터 전송**  
    \- 회원 가입, 상품 주문, 데이터 변경에 사용 (POST 사용)  
    \- Content-Type: application/x-www-form-urlencoded 사용  
        ▶ form의 내용을 메시지 바디를 통해서 전송(key=value, 쿼리 파라미터 형식)  
        ▶ 전송 데이터를 url encoding처리 (abc김 -> abc%EA%B9%80  
    \- HTML, Form은 GET전송도 가능 (쿼리 파라미터로 전송됨)  
    \- Content-Type: multipart/form-data  
        ▶ 파일 업로드 같은 바이너리 데이터 전송 시 사용  
        ▶다른 종류의 여러 파일과 폼의 내용 함께 전송 가능   
    \- GET, POST 이외의 메서드는 지원하지 않는다.  
      
    \- 예시  
    ~~~
    <form action="/save" method="POST">
      <input type="text" name="username" />
      <input type="text" name="age" />
      <button type="submit">전송</button>
    </form> 
    ~~~
    
    전송 시 웹 브라우저가 생성하는 요청 HTTP 메시지  
    
    ~~~
    POST /save HTTP/1.1
    Host: localhost:8080
    Content-Type: application/x-www-form-urlencoded

    username=kim&age=20
    ~~~
    
4.  **HTTP API를 통한 데이터 전송**  
    
    ~~~
    POST /members HTTP/1.1
    Content-Type: application/json

    {
    "username": "young",
    "age": 20
    }
    ~~~
    
    \- 회원 가입, 상품 주문, 데이터 변경  
    \- 서버 to 서버: 백엔드 시스템 통신  
    \- 앱 클라이언트: 아이폰, 안드로이드  
    \- 웹 클라이언트(Ajax)  
        \* HTML에서 Form 전송 대신 자바 스크립트를 통한 통신에 사용(Ajax 통신)  
        예) React, VueJs 같은 웹 클라이언트와 API통신  
    \- POST, PUT, PATCH: 메시지 바디를 통해 데이터 전송  
    \- GET: 조회, 쿼리 파라미터로 데이터 전달  
    \- Content-Type: application/json을 주로 사용 (그 외 TEXT, XML 등이 있음)

### **HTTP API 설계 예시**

-   HTTP API - 컬렉션  
    \- POST 기반 등록 (예 - 회원 관리 API 제공)
-   HTTP API - 스토어  
    \- PUT 기반 등록 (예 - 정적 콘텐츠 관리, 원격 파일 관리)
-   HTML FORM 사용  
    \- 웹 페이지 회원 관리  
    \- GET, POST만 지원

---

#### **API 설계 - POST 기반 등록**

-   **회원** 목록 /members -> GET
-   **회원** 등록 /members -> POST
-   **회원** 조회 /members/{id} -> GET
-   **회원** 수정 /members/{id} -> PATCH, PUT, POST
-   **회원** 삭제 /members/{id} -> DELETE

**\- POST 기반 등록 특징**

-   클라이언트는 등록될 리소스의 URI를 모른다  
    \- 회원 등록 /members -> POST  
    \- POST /members
-   서버가 새로 등록된 리소스 URI를 생성해준다.  
    \- HTTP/1.1 201 Created  
      Location: /members/100
-   **컬렉션 ( Collection)**  
    \- 서버가 관리하는 리소스 디렉터리  
    \- 서버가 리소스의 URI를 생성하고 관리  
    \- 대부분에서 사용  
    \- 예시에서 컬렉션은 /members

---

#### **API 설계 2 - PUT 기반 등록**

-   **파일** 목록 /files -> GET
-   **파일** 등록 /files/{filename} -> PUT
-   **파일** 조회 /files/{filename} -> GET
-   **파일** 삭제 /files/{filename} -> DELETE
-   **파일** 대량 등록 /files -> POST

**\- PUT 기반 등록 특징**

-   클라이언트가 리소스 URI를 알고 있어야 한다.  
    \- 파일 등록 /files/{filename} -> PUT  
    \- PUT /files/star.jpg
-   클라이언트가 직접 리소스의 URI를 지정한다.  
    **※**※****※****※**POST 기반과의 차이점. 서버가 URI를 생성 vs 클라이언트가 URI를 생성**※****※****※****
-   **스토어(Store)**\- 클라이언트가 관리하는 리소스 저장소  
    \- 클라이언트가 리소스의 URI를 알고 관리  
    \- 사용하는 비중이 적다.  
    \- 예시에서 스토어는 /files가 된다.

---

#### **API 설계 3 - HTML FORM 사용**

HTML FORM은 GET, POST ☞ 제약이 있다.

AJAX와 같은 기술을 사용해서 해결 가능

-   회원 목록      /members -> GET
-   회원 등록 폼  /members/new -> GET
-   회원 등록      /members/new, /members -> POST
-   회원 조회      /members/{id} -> GET
-   회원 수정 폼  /members/{id}/edit -> GET
-   회원 수정      /members/{id}/eidt, /members/{id} -> POST
-   회원 삭제      /members/{id}/delete -> POST

**\- HTML FORM 기반 등록 특징**

-   HTML FORM은 GET, POST만 지원
-   **컨트롤 URI**  
    \- GEt, POST만 지원 (제약이 있음)  
    \- 제약을 해결하기 위해 동사로 된 리소스 경로 사용  
    \- POST의 /new, /edit, /delete가 컨트롤 URI  
    \- HTTP 메서드로 해결하기 애매한 경우 사용 (HTTP API 포함)  
    \- 최대한 안 쓰고 구현을 하는 것이 바람직함.

### **참고** 

#### URI 설계 개념([https://restfulapi.net/resource-naming](https://restfulapi.net/resource-naming))

-   **문서(document)**  
    \- 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)  
    \- 예) /members/100, /files/star.jpg
-   **컬렉션(collection)**  
    \- 서버가 관리하는 리소스 디렉터리  
    \- 서버가 리소스의 URI를 생성하고 관리  
    \- 예) /members
-   **스토어(store)**  
    \- 클라이언트가 관리하는 자원 저장소  
    \- 클라이언트가 리소스의 URI를 알고 관리  
    \- 예) /files
-   **컨트롤러(controller), 컨트롤 URI**  
    \- 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행  
    \- 동사를 직접 사용  
    \- 예) /members/{id}/delete
