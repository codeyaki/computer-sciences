# AWS 인프라

## AWS VPC

Virtual Private Cloud

- 최초에 구축하는 사람이 아니라면 거의 만질일이 없다. (devops 전담팀이 따로 있을 정도)
- 가상 네트워크 서비스로 퍼블릭 네트워크와 프라이빗 네트워크를 분리하고 모니터링할 수 있도록 해주는 서비스
- 네트워크 구성과 관련된 사실상 모든 기능을 담당하며, 자체 데이터 센터에서 운영하는 기존 네트워크와 매우 유사한 형태
- private 서브넷은 외부와의 인터넷은 연결이 안되는데 Nat게이트웨이를 사용하면 연결 가능
![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/3d09d93c-d077-4879-a8cf-ebc77dabb8d9)

## AWS API Gateway

- 어떤 규모에서든 개발자가 API를 손쉽게 생성, 게시, 유지 관리, 모니터링 및 보안 유지할 수 있도록 하는 완전관리형 서비스
- 서버의 “대문”과 같은 역할
- API Gateway가 할 수 있는 것들:
    
    트래픽 관리 (제한), CORS 지원, 권한 부여 및 액세스 제어, 제한, 모니터링, API 버전 관리, 인증관련 등…
    
- 무조건 써야하는 것은 아니다. 하지만 사용해서 관리하면 좀더 체계적인 관리 가능

## AWS ARN

- 아마존 리소스 네임으로 AWS 서비스에서 다른 서비스를 연결할때 많이 사용한다.

## AWS ELB

Elastic Load Balancing (ELB)

- 다수의 컴퓨팅 리소스(EC2, Lambda, 등)를 부하 분산시켜주는 아주 중요한 서비스
- 총 3가지 종류의 Balancer (Application Load Balancer, Gateway Load Balancer,
Network Load Balancer) 가 있으며, Application Load Balancer가 일반적인 상황에서
가장 많이 쓰임
- 브라우저에서 ELB의 주소로 접속하게 되면 ELB에서 설정된 가중치에 따라 트래픽을 분산처리해주게 됨.
- API 게이트웨이와 ELB
    - API 게이트웨이는 부하 분산처리 목적이 아니다.
    - 두 서비스는 완전 다른 기능을 가지고 있다.
    - 이 두가지를 동시에 쓰면 API 게이트웨이가 먼저 처리된다.
- 라운드 로빈 방식으로 처리

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/7d3792b9-f6eb-415a-8133-ad822d06ab61)
![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/f3fe8854-1286-45e4-9666-5cb953a47f23)

## AWS S3

Simple Storage Service(S3)

- 가장 오래된 AWS 서비스중 하나로 엄청난 내구성과 가용성을 자랑하며 이미지,동영상, 오디오 파일과 같은 정적파일들을 용이하게 관리하도록 돕는 스토리지 서비스
- S3에 트리거를 걸어두면 람다를 실행하여 따로 로직을 실행할 수 있다. ( 파일 압축, 섬네일, 자막 생성… )
- Presigned URL을 이요해서 서버를 거치지 않고 사용자를 다이렉트로 업로드할 수 있다.
- 단순 파일의 저장 공간을 넘어서서 데이터를 저장하는 스토리지 플랫폼
ex)
    - 데이터 처리: S3에 저장되는 Trigger를 이용해 람다를 실행 시킬 수도 있음
    - 로그: AWS 안에서 이뤄지는 대부분의 로그는 S3에 저장 됨
    - 쿼리 지원: AWS Athena를 통하여 S3에 저장된 파일을 쿼리할 수도 있음
    - 호스팅: Single Page Application (React)를 호스트 할 수도 있음

### Presigned URL

- 서버에 부하를 덜 일으키기 위해 presigned URL을 통해서 클라이언트에서 바로 업로드를 시키도록 할 수 있다.
- 맘대로 S3에 파일을 업로드할 수 없기 때문에 서버에서 인증/인가를 통해서 검증된 사용자에게 파일을 업로드할 수 있는 URL을 생성하여 전달
- 파일을 업로드할 수 있는 시간을 제한할 수 있다.

## CloudFront

- 이미지를 사용하는 99%의 경우 사용하게 된다.
- 가장 가까운 곳으로 이용자 요청을 받는다
- 전 세계에 있는 AWS 엣지 로케이션을 통하여 CDN 서비스를 제공 함
- 현재 48개국 90개가 넘는 도시에서 410개가 넘는 접속 지점 (엣지 로케이션
400개 이상, 리전별 중간 티어 캐시 13개)로 구성된 글로벌 네트워크를 지원
- 속도는 높이고, 가격은 내리며, 서버 부하는 줄일 수 있음

![스크린샷 2023-05-15 오후 3.14.29.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f2d136ee-3684-46db-b923-a079817985bb/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-05-15_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_3.14.29.png)

## Secrets Manager

Amazon Secret Manager / Parameter Store

- 데이터베이스 보안 인증 정보 및 API 키와 같은 보안 정보를 안전하게 암호화하고 중앙 집중식으로 감사할 수 있도록 도와주는 서비스
- .env 파일을 서버 별로 따로 관리하기 보다는 한 곳에서 집중적으로 관리
- DB 정보와 같은 민감한 정보는 암호화가 지원이 되는 Secret Manager에 저장
- 간단한 정보 (ex. Endpoint)는 Parameter Store에 저장하여 사용
- 리전별로 관리할 수 있다.
