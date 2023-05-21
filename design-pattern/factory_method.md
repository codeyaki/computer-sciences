# Factory Method Pattern
## 팩토리 메서드 패턴이란?
- 팩토리 메서드 패턴은 부모(상위)클래스에 알려지지 않은 추상 클래스를 생성하는 패턴으로 자식(하위)클래스가 직접 어떤 객체를 생성할지 결정하도록 하는 패턴! 
- 즉, 객체 생성을 위한 패턴으로 생성과 사용의 분리를 통해서 유연하게 객체를 생성할 수 있게 된다.
- 또한 객체 생성에 필요한 과정들을 템플릿처럼 정해놓고 각 과정을 구<img width="640" alt="image" src="https://github.com/5onchangwoo/computer-sciences/assets/96860725/8064d1c2-8af3-43a0-a7e2-1b69a6cf11fc">현할 수 있다.
![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/59a35a1c-0ebf-4040-a275-47b96222266d)

## 왜 사용하나요?
- 생성자 (Creator)와 구현 객체(concrete product)의 강한 결합을 피함
- 객체가 생성될때 반복적으로 할 일을 수행시킬 수 있음
- 캡슐화, 추상화를 통해 생성되는 객체의 구체적인 타입 은닉
- 단일 책임 원칙 (SRP) 준수
  - 객체 생성 코드를 한 곳 (패키지, 클래스 등)으로 이동시켜 코드를 유지보수하기 쉽게할 수 있으므로 원칙을 만족
- 개방 폐쇄 원칙 (OCP) 준수
  - 기존 코드를 수정하지 않고 새로운 유형의 제품 인스턴스를 프로그램에 도입할 수 있음 (확정성 증가)
- 생성에 대한 인터페이스 부분과 생성에 대한 구현 부분을 따로 나뉘었기 때문에 패키지 분리하여 개별로 여러 개발자가 협업을 통해 개발가능
  ![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/c9cfd969-db81-4703-9222-6fb61b05add1)
  
## 언제 사용하나요?
- 클래스의 생성과 사용 로직 분리로 결합도를 낮춰야 할때
- 캡슐화를 통해 정보 은닉이 필요한 경우
- 사용자가 구성요소를 확장할 수 있도록 제공해야 할때(라이브러리, 프레임워크 만들때 유용)
- 기존 객체를 재구성하는 대신 기존 객체를 재사용하여 리소스 절약하고자 할 때

## 문제점
- 각 제품 구현체마다 팩토리 객체들을 생성해야하기 때문에, 구현체가 늘어날때 마다 팩토리 클래스가 증가 (서브 클래스 증가)
- 코드 복잡성 증가

## 구현 방법 (자바)
- ![UML](https://github.com/5onchangwoo/design-pattern/blob/main/src/com/example/dessignpattern/creational/factorymethod/PizzaFactory.png)
- [자바 코드 보러가기](https://github.com/5onchangwoo/design-pattern/tree/main/src/com/example/dessignpattern/creational/factorymethod)

