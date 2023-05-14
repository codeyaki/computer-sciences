# AWS Aurora

- 오로라도 RDS에 속함
- 오로라 플랫폼은 AWS만의 관계형 데이터베이스로써 기존의 소스를 커스터마이징 하여 AWS에 최적화 시킨 것
(RDS가 커피라면, AUrora는 TOP)
- RDS에서 사용하는 EBS 대신 NVMe SSD 드라이브 위에 구축되어 훨씬 빠름
- 서버리스 기능과 Auto Scaling을 기본적으로 지원
- 대신 좀 비싸다
    - r6g.2xlarge 기준 MySQL: $1.02 / Aurora: $1.253
- 지원 언어가 한정적이다 ( MySQL, PostgreSQL )
- 서버가 없고 리퀘스트 단위로 혹은 연결을 해서 데이터를 가져올 수 있다. ( 운영비 X )
