# Message Queue

AWS SQS, AWS Kinesis

## Queue?

[https://www.codenary.co.kr/architecture/list?category=실시간 스트리밍](https://www.codenary.co.kr/architecture/list?category=%EC%8B%A4%EC%8B%9C%EA%B0%84%20%EC%8A%A4%ED%8A%B8%EB%A6%AC%EB%B0%8D)

[https://www.codenary.co.kr/architecture/list?category=Event Driven](https://www.codenary.co.kr/architecture/list?category=Event%20Driven)

[https://www.codenary.co.kr/architecture/list?category=대용량 처리](https://www.codenary.co.kr/architecture/list?category=%EB%8C%80%EC%9A%A9%EB%9F%89%20%EC%B2%98%EB%A6%AC)

- 비동기로 이벤트를 처리하기 위해 사용

## AWS SQS

Amazon Simple Queue Service

- 마이크로서비스, 분산 시스템 및 서버리스 애플리케이션을 위한 완전관리형 메시지 대
기열
- `표준 대기열`
    - 무제한 처리량 / 최소한 한 번 전달 (여러번 전달 될 수도 있음) / 최선 노력 순서
    - 보통 표준 대기열 보다는 키네시스를 많이 사용
    
    ![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/18db875b-8759-4966-88a4-91262dc05e0c)
    
- `FIFO(First-In-First-Out) 대기열`
    - 초당 최대 300개의 메시지 / 정확히 한 번 처리 / 선입선출 전달
    
    ![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/e6ebcbca-6b5f-451c-8190-7d32e75b0286)
    

### 구조 (예시)

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/16955277-7ffc-4e51-b027-bdc599ef8ff6)

- Dead Letter Queue를 통해 실패한 작업을 따로 모아두고 나중에 사용할 수 있음

## AWS Kinesis

- Amazon Kinesis는 모든 규모의 스트리밍 데이터를 비용 효율적으로 처리할 수 있는 핵심 기능과 더불어 애플리케이션 요구 사항에 가장 적합한 도구를 선택할 수 있는 유연성을 제공
- 예시
    - 실시간으로 비디오 및 데이터 스트림을 손쉽게 수집, 처리 및 분석
    - 모든 규모에서 쉽게 데이터 스트리밍
    - 안정적으로 실시간 스트림을 데이터 레이크, 웨어하우스, 분석 서비스에 로드
    - 스트리밍 데이터에서 실행 가능한 인사이트 확보
    - 로그 수집

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/4543b854-e62d-4336-b0e1-c38c2471c678)

- 특이하게 Shard라는 것을 사용한다.
    - 프로듀서가 생산한 하나의 메시지가 하나의 샤드를 통해서 컨슈머한테 전달한다.
    - 샤드를 한개로 하면 순서가 보장된다.
    - 샤드가 여러개면 그만큼 대역폭이 넓어지지만 순서가 보장되지 않을 수 있다.
    - 보통 Log 시스템을 구성할때 많이 사용된다.

## SQS vs Kinesis

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/bcab1ccd-0ba4-4158-8cd4-3fdc469d0485)

|  | Kinesis | SQS |
| --- | --- | --- |
| Record Size | 1MB | 256KB |
| Independancy | Shard 레벨에서 나뉨 | 메세지 별로 independent |
| Auto-scale | 수동 | 자동 |
| Retention | 최대 7일 | 최대 14일 |
| DLQ | 지원 X | 기본 지원 O |
| 잔류 | Queue 잔존 | 소모되면 Queue에서 삭제 |
