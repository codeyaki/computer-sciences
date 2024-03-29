# JVM
## JVM이란?
- Java Virtual Machine의 줄임말로 자바를 실행하기 위한 가상 머신을 의미합니다.
- Java는 OS에 종속적이지 않다는 특징이 있는데 이를 위해서 OS와 독립적으로 JAVA를 실행시켜주는 역할을 하게 된다.


## 자바의 컴파일 과정  
![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/ce3698d6-8730-43c0-bd86-867e93318427)
- 일종의 가상 머신이다.
- 우리가 작성한 java 코드 (원시 코드)는 CPU가 인식하지 못하기 때문에 기계어로 번역을 해주어야 한다.
- JVM이 기계어로 번역해주기 때문에 JVM이 읽을 수 있는 코드인 Java Bytecode (.class)파일로 번역을 해서 JVM에 전달해주게 된다.
- 우리는 java코드만 작성하여 class 파일만 생성하면 JVM을 통해 OS에 무관하게 실행시킬 수 있는 것이다.

> ### 자바 컴파일러
> - JDK 설치하면 bin에 존재하는 javac.exe
> - javac 명령어를 통해 .java를 JVM이 읽을 수 있는 파일인 .class로 컴파일 할 수 있다.
> - 동작 순서
>   1. Parse: *.java 소스파일을 읽은 뒤 결과 토큰을 AST(Abastract Syntax Tree) 노드에 매핑한다. 
>   2. Enter:  정의된 심볼들을 심볼테이블(Symbol table) 에 저장한다. 
>   3. Process annotations: 요청된 경우 지정된 컴파일 위치에서 찾은 애너테이션을 처리합니다.
>   4. Attribute: 구문 트리에 속성을 부여하며, 이름 확인, 유형 검사 및 상수 정의가 포함된다.
>   5. Flow: 이전 단계의 트리에 대한 데이터 흐름을 분석합니다. 여기에 할당 및 도달 가능성에 대한 검사도 포함됩니다. 
>   6. Desugar: AST를 다시 작성하고 몇몇 syntactic sugar 들을 번역합니다.
>   7. Generate: *.class 파일을 생성합니다.

### JVM 특징
1. 스택 기반 가상 머신
  - 레지스터 기반으로 동작하지 않고 스택 기반으로 동작한다.
2. 심볼릭 레퍼런스
  - 명시적인 메모리 주소 기반 참조가 아니라 심볼릭 참조을 사용한다. (그 자체가 값인 기본형은 제외)
  > ### 심볼릭 레퍼런스
  > 심볼릭 레퍼런스는 참고하는 클래스의 특정 메모리 주소를 참조 관계로 구성한 것이 아니라 참조하는 대상의 이름만을 지칭한 것이다. 
3. 가비지 컬렉션
  - 클래스 인스턴스는 사용자에 의해 생성, 가비지 컬렉션에 의해 소멸
4. 기본 자료형 크기 명확
  - 전통적인 언어는 플랫폼에 따라 int형의 크기가 변화. 반면 JVM은 명확하게 크기를 정해두어 플랫폼에 독립적
5. 네트워크 바이트 오더
  - 클래스 파일은 네트워크 전송 시 사용되는 바이트 오더 사용 (빅 엔디안)

> ### 빅 엔디안 vs 리틀 엔디안
> - 바이트 오더란? 메모리 주소를 부여하는 순서를 말한다. 
> - 빅 엔디안: 낮은 주소에 데이터의 높은 바이트(MSB, Most Significant Byte)부터 저장, 평소 사람이 사용하는 선형 방식과 같아서 메모리에 저장된 그대로 읽기 가능.
> - 리틀 엔디안: 낮은 주소에 데이터의 낮은 바이트(LSB, Least Significant Byte)를 저장하는 방식. 반대로 읽어어 한다.
> - ex) 
>   <div style={'dispaly:flex;'}>
>
>     ![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/a4049db9-6832-4f45-bef3-16e62b3222ec)
>     ![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/13b14151-0a5c-469b-a8c3-429dd93bd4f5)
>
>   </div>

### JIT 컴파일러
- 자바 바이트 코드는 기계가 바로 이해할 수 있는 언어가 아니다. (인간이 보기 편한 형태로 기술 된 것)
- JVM은 기계어로 번역하기 위해 인터프리터 사용했었다.
- JIT는 인터프리터의 단점을 보안하기 위해서 추가되었다. 인터프리터 방식으로 동작하다가 적절한 시점에 바이트 코드 전체를 네이티브 코드로 바꾸는 작업을 한다.
  그 다음부터는 네티이브 코드로 컴파일된 코드를 바로 사용한다.  
- 네이티브 코드를 실행하는 것이 하나씩 인터프리팅 하는 것보다 빠르고, 네이티브 코드는 캐시에 보관하기 때문에 한 번 컴파일된 코드는 계속 빠르게 수행된다.
- JIT 컴파일러가 컴파일하는 과정은 바이트코드를 하나씩 인터프리팅하는 것보다 훨씬 오래걸리기에 만약, 한 번만 실행되는 코드라면 컴파일 하지 않고 인터프리팅하는게 유리하다. 
  따라서 컴파일러를 사용하는 JVM들은 내부에서 해당 메소드의 수행빈도를 확인 후 일정 정도를 넘을 때 컴파일을 수행한다. 
  ![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/6b9b9a7f-5fc4-4120-bb48-314d1504859f)
  ![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/05d8176e-d558-4433-a133-51b62aaa719c)
 

## 참고자료
- [[1주차] JVM은 무엇이며 자바 코드는 어떻게 실행하는 것인가.](https://catsbi.oopy.io/df0df290-9188-45c1-b056-b8fe032d88ca)
- [JVM 이해하기 - 1 (JVM 특징 이해하기)](https://happy-coding-day.tistory.com/entry/JVM-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-1)
