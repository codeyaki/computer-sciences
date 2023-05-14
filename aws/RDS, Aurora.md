# AWS RDS & Aurora
## AWS RDS란?

- 클라우드 관계형 데이터베이스를 간편하게 설정, 운영 및 확장할 수 있는 관리형 서비스 모음
- RDS는 EC2위에서 동작하는 서비스 ( DB를 사용하기 위해서는 인스턴스가 필요하기 때문)
굳이 그렇게 하지 않는 이유는 DB를 좀더 손쉽게 관리, 모니터링 하기 위해서 RDS를 사용
- RDS를 왜 사용? → 주요 기능들 때문
    - RDS 백업: 자동 백업, DB 스냅샷
    - 멀티 AZ: 두 개 이상의 AZ에 걸쳐 DB를 구축하고 원본과 다른 DB(standby)를 자동으로 동기화(Snyc), 읽기 전용 복제본
    - CloudWatch 연동: DB인스턴스의 모니터링 (디테일 모니터링, CPU, Storage 사용량, 그 이외의 Error Log 등) → 클라우드 워치에 익숙해져야 한다. (특히 람다 서비스는 클라우드 와치를 통해서 봐야한다.)

## AWS Aurora
- 오로라도 RDS에 속함
- 오로라 플랫폼은 AWS만의 관계형 데이터베이스로써 기존의 소스를 커스터마이징 하여 AWS에 최적화 시킨 것
(RDS가 커피라면, AUrora는 TOP)
- RDS에서 사용하는 EBS 대신 NVMe SSD 드라이브 위에 구축되어 훨씬 빠름
- 서버리스 기능과 Auto Scaling을 기본적으로 지원
- 대신 좀 비싸다
    - r6g.2xlarge 기준 MySQL: $1.02 / Aurora: $1.253
- 지원 언어가 한정적이다 ( MySQL, PostgreSQL )
- 서버가 없고 리퀘스트 단위로 혹은 연결을 해서 데이터를 가져올 수 있다. ( 운영비 X )

## RDS / AURORA 구조 차이
### RDS 구조

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/0973153c-f150-4076-93c9-bbefba1de7e3)
- EBS는 데이터 저장소
- M: 마스터
S: 슬레이브
- 자동으로 다른 곳에서도 싱크에 맞춰 동시에 진행된다. (2개 이상의 AZ)
- 읽기 전용 복제 RDS또한 가능 (비동기)

### Aurora 구조

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/942756dc-1786-4976-a954-5f93c3f74e66)
- 복사본이 여러군데 나눠져 있어 병목현상 X

### 속도 차이

![image](https://github.com/5onchangwoo/computer-sciences/assets/96860725/910cd0d2-153d-4559-8376-b90da6b6a5e9)
- 볼륨 시스템으로 인해 속도가 많이 차이나게 된다. (쓰기에서 엄청난 속도 차이)
- MySQL 최신 버전에서는 다른 결과가 나올 수 있다.

