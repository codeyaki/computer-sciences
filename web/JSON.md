# JSON
## 개념
JSON(JavaScript Object Notation)은 사람이 읽고 쓰기 쉽고 기계가 구문 분석하고 생성하기 쉬운 경량 데이터 교환 형식  
JSON 구문은 JavaScript 구문에서 영감을 받았지만 JavaScript에 국한되지 않는다.  
웹 서버와 웹 브라우저를 포함하여 서로 다른 시스템 간에 데이터를 전송하는 데 사용되는 텍스트 기반 형식이다.  
JSON은 개체 및 배열과 같은 데이터 구조를 지원하는 모든 프로그래밍 언어와 함께 사용 가능하다.  

## 사용 유형 
1.사용자 생성 데이터로부터 JSON 객체 생성  
2.시스템 간 데이터 전송  
3.애플리케이션용 데이터 구성  
4.복잡한 데이터 모델 간소화하기  

## 구조  
객체 (키 - 쌍의 모음) + 배열 (정렬된 값의 목록)  
JSON의 값은 숫자, 문자열, 부울, null, 개체 및 배열을 비롯한 모든 데이터 유형 사용 가능

예시
<pre>
 <code>
  {
    "이름": "Son" ,
    "나이": 30,
    "isStudent": true,
    "취미": ["읽기", "달리기", "여행"],
    "주소": {
      "거리": "123 메인 스트리트",
      "시": "마을",
      "상태": "CA",
      "zip": "12345"
    }
  }
  </code>
</pre>


[메인화면](https://github.com/5onchangwoo/computer-sciences)
[이전 스텝](https://github.com/5onchangwoo/computer-sciences/blob/main/web/REST%2C%20REST%20API%2C%20RESTful%20API.md)
[다음 스템]()
