# AWS란?

## On-premise vs Cloud Computing

- On-premise
    
    온프레미스란기업의 서버를 클라우드 같은 원격 환경에서 운영하는 방식이 아닌, 자체적으로 보유한 전산실 서버에 직접 설치해 운영하는 방식
    
- Cloud Computing
    
    클라우드 컴퓨팅은 인터넷을 통하여 데이터를 저장하거나 데이터베이스, 서버, 네트워킹, 소프트웨어와같은 도구, 애플리케이션등 다양한 서비스를 제공하는 방식
    

## Cloud Computing을 쓰는 이점

- 점점 증가하는 서버 인스턴스의 수를 온프레미스로 감당하기엔 점점 벅참 (공간적, 비용적 문제)
    - 이를 클라우드 컴퓨팅을 통해 해결
- 글로벌 서비스를 제공하려면 각 국가에 데이터 센터를 직접 구축해야하는 것을 대신 AWS를 통해 해결
- 예로 카프카의 클러스터 규모를 살펴보면 (2022년 8월 운영환경 기준)
    - 카프라 클러스트 27개
    - 브로커 162대
    - 파티션 약 24,000개
    - 초당 평균 50만건, 최대  140만건 메시지 유입
- 다른 클라우드 보다 AWS를 사용하는 이유는 선점효과덕분이라고 볼 수 있다. 
하지만 머신러닝과 같은 특수한 경우는 다른 플랫폼을 사용하는 경우가 많다.
- 다양한 서비스가 제공되어 상황에 알맞게 골라서 사용할 수 있다.
![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/a3322a2c-9880-4b69-8b58-5f934ad124bc)

## AWS 서비스의 전체적인 모습

1. 인프라 관련 요소들
    - AWS API Gateway, AWS S3, AWS ELB, AWS CloudFront, AWS Secret Manager, 스냅샷
2. 컴퓨팅 파워 (서버)
    - AWS EC2, AWS Elastic Beanstalk, AWS ECS, AWS Fargate, AWS Lambda (Serverless)
3. Message Queue
    - AWS SQS, AWS MSK, AWS Kinesis
4. Database
    - AWS RDS, AWS DynamoDB, AWS ElastiCache
