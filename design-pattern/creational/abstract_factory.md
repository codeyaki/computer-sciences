# 추상 팩토리 패턴(abstract factory pattern)

## 추상 팩토리 패턴이란?
추상 팩토리 패턴은 관련된 여러 객체를 일관된 방식으로 생성하는 인터페이스를 제공하는 패턴입니다.  
즉, 관련성 있는 여러 종류의 객체를 생성하는 경우 사용됩니다. 추상 팩토리 패턴을 사용하면 구체적으로 어떤 클래스의 인스턴스를 사용하는지 클라이언트에게 감출 수 있습니다.

이 추상 팩토리 패턴을 이해하기 위해서는 팩토리 메서드 패턴을 이해해야 합니다. 왜냐면 팩토리 메서드 패턴에서 발전한것이 추상 팩토리 패턴이기 때문입니다.  
[ --> 팩토리 메서드 패턴 학습하러 가기](https://github.com/5onchangwoo/computer-sciences/blob/main/design-pattern/factory_method.md)

<img width="1197" alt="image" src="https://github.com/5onchangwoo/computer-sciences/assets/96860725/652739fc-73fe-497c-9ea7-e0587a14c77f"/>
<br/>
<br/>

> 팩토리 메서드 vs 추상 팩토리
> ||팩토리 메서드|추상 팩토리|
> |---|---|---|
> |의도|단일 유형 객체 생성|관련 유형 객체 관리|
> |구현 방법|추상 클래스|인터페이스|
> 
> 다만 구현방법은 달라질 수 있기때문에 기본적인것은 이렇다는 것만...
> 결국 추상 팩토리방법은 팩토리 메서드 여러개를 동시에 관리하기 위해서 사용하는 걸로 이해된다.

## 왜 사용하나요?
- 팩토리 메서드에서의 장점 그대로 사용
- 팩토리 메서드에서 유형간 관련있는 것들을 묶어 관리하고자 사용

## 문제점
- 코드 복잡성 증가

## 구현 방법 (자바)
[코드 보러가기](https://github.com/5onchangwoo/design-pattern/tree/main/src/com/example/dessignpattern/creational/abstractfactory)
