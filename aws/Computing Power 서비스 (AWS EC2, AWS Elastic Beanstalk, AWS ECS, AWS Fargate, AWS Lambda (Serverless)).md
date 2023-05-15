# Computing Power (서버)

AWS EC2, AWS Elastic Beanstalk, AWS ECS, AWS Fargate, AWS Lambda (Serverless)

## AWS EC2 (Amazon Elastic Cloud Compute)

- 가장 기본적인 형태의 클라우드 컴퓨팅 (= 클라우드 컴퓨터 한 대)
- 온디맨드
    - 선결제 금액이나 장기 약정 없이 저렴하고 유연하게 Amazon EC2를 사용하기 원하는 사용자
- **`스팟 인스턴스`**
    - 시작 및 종료 시간이 자유로운 애플리케이션 (노는 자원 활용하기)
    - 안정성이 보장되는 서버에는 사용하면 안된다
    - 보통 배치에 사용, 머신러닝에 사용
- `Saving Plans`
    - 1년 또는 3년 기간의 일정 사용량 약정을 조건으로 EC2 및 Fargate 사용량에 대해 저렴한 요금을 제공하는 유연한 요금
- 비용이 단순히 서버비 뿐만 아니라 네트워크 비용도 포함
- 그래픽카드, 스토리지등 구성 부품을 선택할 수 있다.
- 오토 스케일링을 지원한다.
    - 트래픽에 따라 자동으로 인스턴스의 개수를 관리
- 탄력적 IP
    - EC2는 재부팅할때마다 IP가 바뀌는데 이 IP를 고정으로 사용하고 싶을때 사용
- 키 페어 ( 비대칭키 )를 등록하여 인스턴스 내부에 접속할때 사용한다.

## AWS Elastic Beanstalk

- AWS 클라우드에서애플리케이션을신속하게 배포하고 관리할 수 있는 서비스 
(애플리케이션코드를 업로드하기만하면 작동)
- Elastic Beanstalk = EC2 + 배포 버전 관리 (롤백) + Elastic Load Balancer + 모니터링 + 로그 트래킹 + 오토 스케일링
- 다양한 언어 지원: .NET / PHP / Java / Ruby / Node.js / Python / Docker / Go

## Amazon Fargate

- Fargate를 사용하면 더 이상 컨테이너를 실행하기 위해 가상 머신의 클러스터를 프로비저닝, 구성 또는 조정할 필요가 없습니다. 따라서 서버 유형을 선택하거나, 클러스터를 조정할 시점을 결정하거나, 클러스터 패킹을
최적화할 필요가 없습니다.
- 이전에는 컨테이너를 실행하기 위해서는 컨테이너를 실행할 Instance(EC2)를 실행시켜야하였지만, AWS Fargate는 이러한 수고를 덜어 줌

### Fargate VS EC2

- 가격이 Fargate가 더욱 비싸다
- 2CPU + 8gb 인스턴스 기준 EC2는 0.104USD인 반면 Fargate는 약 0.226USD이다.
(CPU + 메모리 값 : 0.18624 + 0.04088)
- EC2는 칩셋의 성능을 조절할 수 있다. 반면 Fargate는 낮은 성능의 칩셋으로 고정되어 있다.
- 반면 Fargate는 Docker를 사용하다 보니 환경이 안정적이다. 또한 배포할때 편리하다는 장점이 있다.

## AWS ECR

- Amazon Elastic Container Registry
- Amazon Elastic Container Registry(Amazon ECR)는 안전하고 확장 가능하고 신뢰할 수 있는 AWS 관리형 컨테이너 이미지 레지스트리 서비스
- DockerHub를 사용하지 않아도 된다. 비슷한 서비스 중 ECR의 비용이 저렴하다.
- `RDS (DB)` = 데이터를 저장하는 장소
`S3` = 사진, 이미지 등 파일을 저장하는 장소
`ECR` = 도커 이미지를 저장하는 장소

## AWS ECS

Amazon Elastic Container Service

- ECS(Elastic Container Service)는 AWS에서 제공하는 컨테이너
- 오케스트레이션서비스로 여러 어플리케이션컨테이너를 쉽고 빠르게 실행하고, 컨테이너를 적절하게 분배 및 확장 & 축소 할 수 있도록 도와주는 서비스
- AWS EC2 와 AWS Fargate 중 원하는 환경에서 실행 가능

### 용어 정리

- Task Definition: 컨테이너의 이미지, CPU/메모리 리소스 할당 설정, port 매핑, volume 설정
- Task: Task 안에는 한 개 이상의 컨테이너들이포함되어 있으며 ECS에서 컨테이너를 실행하는 최소 단위는 Task이다. (인스턴스화)
- Service: Task 들의 Life cycle 을 관리하며, 오토스케일링과로드밸런싱을 관리
- Cluster: Task 가 배포되는 Container Instance 들은 논리적인 그룹

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/9d6322ab-a882-4f1c-b2dd-fbb5ea95f9e9)

- Task안에 여러 컨테이너가 들어가는 이유
    - 사이드카 패턴으로 메인 서버가 죽는 경우를 감지하기 위해서 모니터링용 서버를 구성한다.
    - 이를 묶어서 하나의 TASK로 묶어서 올리게 되는 것이다.
    - 하나의 Docker-compose라고 보면 된다.

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/71499141-3b2e-4b32-abb5-8713a57f47c0)

## AWS Lambda

- 서버 없이도 코드를 실행시킬 수 있는 서버리스 컴퓨팅 서비스
- 코드를 돌리기위한 리소스를 임의로 지정할 수 있으며, 사용 리소스 x 사용
- 시간에 따라 과금이 된다. (ex. 메모리 용량 / 코어 갯수)
- 최대 15분 / 최대 10GB / 최대 6개의 Core
- 사용 예시
    - 비동기 처리 (이미지 썸네일 생성)
    - 예측이 불가능 한 리소스 사용 (대용량 처리 / 머신러닝)

### Cold Start / Warm Start

- 기본적으로 EC2와 같은 인스턴스보다는 Latency가 높다.
- 콜드 스타트
    - 배포 패키지의 크기와 코드 실행 시간 및 코드의 초기화 시간에 따라 새 실행 환경으로 호출을 라우팅할 때 지연 시간이 발생하는 람다 호출 시작 (겨울에 자동차 시동 걸때에서 유래 됨)
- 5분정도 warm하게 유지, 후에 계속 warm하게 유지하기 위해선 지속적으로 사용해야 하는 방법밖엔 없음
- 일반적인 서버의 Latancy가 100ms이하이다. 반면 Lambda는 기본적으로 100ms 이상이다.

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/beaafdd9-d06a-4076-85ce-0863aea14dd4)

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/efcc4be1-06d7-49da-a080-ecf6479d93e6)

### Lambda를 사용해야 할때 예시

1. 하루에 Request가 10000개 안될때
( 많이 사용하지 않는 서비스 / API / 기능 이다. )
2. 병렬 처리 
(Youtube에 영상을 올리면 다양한 화질로 변환하는 작업 같은 것)
( SNS 이미지 크롭 )

### AWS Lambda - Serverless (프레임 워크)

- AWS, Azure, GCP 등의 서버리스 서비스를 쉽게 사용할 수 있도록 도와주는 오픈소스 프레임 워크
- 사용 가능 서버:
    - Node 계열 – ExpressJS, NestJS 등..
    - Java 계열 – Spring(Spring Cloud Function),
    - Python 계열 – FastAPI, Flask 등..
- 소규모 / 이용자가 많지 않은 서비스에서 가격 효율적으로 이용 가능

## AWS 혼자 해보기

## 프론트

s3 / cloudfront 사용해서

1. Single Page Application 서빙하기
2. 이미지 cdn 구축하기
3. NextJS와 같이 SSR을 EC2 / fargate로 진행해보기

## 백엔드

1. serverless (lambda) 사용해서 API 서버를 구축해보기 or API 서버를 aws fargate / ECR 이용해서 띄워보기
2. SNS 예시 파이프라인 구축해보기
    - s3 presigned url 이용해서 s3에 이미지 업로드 (20개)
    - 이미지가 업로드 되면 람다 트리거를 통해 image resizing 하는 로직 실행
    후 s3에 크롭된 이미지 저장
