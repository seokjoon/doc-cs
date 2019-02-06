## 목록
```
2. AWS 기본 개념 살펴보기 
3. AWS 계정 생성하기 
4. 가상 서버를 제공하는 EC2 
5. Security Group으로 방화벽 설정하기
6. 고정 IP를 제공하는 Elastic IP 
7. EC2 인스턴스 접속을 위한 키 쌍 
8. AMI 
9. API와 툴 사용을 위한 액세스 키 생성하기
10. AWS 리소스의 상태를 모니터링하는 CloudWatch 
11. HTTP 프로토콜과 연동되는 스토리지 S3 
12. 전 세계에 콘텐츠를 배포하는 CDN 서비스인 CloudFront 
13. 확장 가능한 관계형 데이터베이스를 제공하는 RDS 
14. 확장 가능한 NoSQL 분산 데이터베이스를 제공하는 DynamoDB 
15. 확장 가능한 분산 인 메모리 캐시를 제공하는 ElastiCache 
16. 사용자와 그룹을 생성하여 접근제어 및 권한관리를 제공하는 IAM 
17. AWS 리소스와 연동 가능한 DNS 서비스 Route 53 
18. 부하 분산과 고가용성을 제공하는 ELB 
19. 자동으로 EC2 인스턴스를 생성하여 서비스를 확장하는 Auto Scaling 
20. 가상 네트워크를 제공하는 VPC 
21. 데이터 보관 및 백업을 위한 매우 저렴한 스토리지 서비스 Glacier 
22. 서버 구성을 자동화하는 CloudFormation 
23. 간편하게 사용하는 애플리케이션 플랫폼 서비스 Elastic Beanstalk 
24. 애플리케이션 구성과 배포를 자동화하는 OpsWorks 
25. 검색 서비스를 제공하는 CloudSearch 
26. 푸시 알림 서비스 SNS 
27. 이메일 전송 서비스 SES 
28. 메시지 큐를 제공하는 SQS 
29. 동영상 인코딩 서비스 Elastic Transcoder 
30. AWS API, CLI 활용하기 
31. 글로벌 사진 사이트 구축하기 
32. 자동 확장 가능한 콘서트 티켓 예매 사이트 구축하기 
33. 자동 확장 가능한 모바일 게임 서버 구축하기
34. 부록 
```

## 2. AWS 기본 개념 살펴보기 
* 리전, 지역 
* 가용 영역 
* 에지 로케이션

## 3. AWS 계정 생성하기 

## 4. 가상 서버를 제공하는 EC2 
* EC2 인스턴스 유형 
* EC2 인스턴스 구매 옵션 
* EC2 인스턴스 생성하기 
* EC2 인스턴스에 접속하기 
* 가상 스토리지를 제공하는 EBS 
* EBS 스냅샷 활용하기 
* 인스턴스 스토리지를 Root 장치로 사용하는 EC2 인스턴스 생성하기 
* EC2 기타 설정 및 기능

## 5. Security Group으로 방화벽 설정하기

## 6. 고정 IP를 제공하는 Elastic IP 
* Elastic IP 할당받기 
* Elastic IP 연결하기
        
## 7. EC2 인스턴스 접속을 위한 키 쌍 
* 키 쌍 생성하기 
* 외부 키 쌍 파일 사용하기 
* 이미 생성된 EC2 인스턴스에서 공개 키 바꾸기
        
## 8. AMI 
* AWS Marketplace 
* EC2 인스턴스로 AMI 생성하기 
* AMI를 다른 리전으로 복사하기 
* 인스턴스 스토리지를 Root 장치로 사용하는 EC2 인스턴스 생성하기
        
## 9. API와 툴 사용을 위한 액세스 키 생성하기
    
## 10. AWS 리소스의 상태를 모니터링하는 CloudWatch 
* CloudWatch 알람 생성하기 
* CloudWatch 커스텀 측정치 사용하기
        
## 11. HTTP 프로토콜과 연동되는 스토리지 S3 
* S3 버킷 생성하기 
* S3 버킷에 파일 올리기/받기 
* S3 세부 설정하기
            
## 12. 전 세계에 콘텐츠를 배포하는 CDN 서비스인 CloudFront 
* CloudFront 배포 
* S3와 CloudFront 연동하기 
* CloudFront 커스텀 오리진 사용하기 
* Signed URL로 CloudFront 콘텐츠 사용 제한하기 
* Invalidation으로 CloudFront 콘텐츠 갱신하기
        
## 13. 확장 가능한 관계형 데이터베이스를 제공하는 RDS 
* RDS DB 인스턴스 클래스 
* RDS 예약 인스턴스 
* RDS 데이터베이스 엔진과 라이선스 모델 
* RDS DB 인스턴스 생성하기 
* RDS DB 인스턴스 Security Group 생성 및 설정하기 
* RDS DB 인스턴스 사용하기 
* RDS DB 스냅샷 활용하기 
* RDS를 특정 시점으로 복구하기 
* RDS DB 인스턴스 Read Replica 생성하기 
* RDS DB 인스턴스 성능 확장하기 
* RDS 기타 설정 및 기능
        
## 14. 확장 가능한 NoSQL 분산 데이터베이스를 제공하는 DynamoDB 
* DynamoDB의 데이터 모델 
* DynamoDB에 맞는 데이터 구조 설계하기 
* DynamoDB 테이블 생성하기 
* DynamoDB 테이블에 데이터 추가하기 
* DynamoDB 데이터 쿼리하기 
* DynamoDB 기타 설정 및 기능
        
## 15. 확장 가능한 분산 인 메모리 캐시를 제공하는 ElastiCache 
* ElastiCache 캐시 노드 유형 
* ElastiCache 예약 캐시 노드 
* ElastiCache Memcached 클러스터 생성하기 
* ElastiCache Memcached 클러스터 Security Group 생성 및 설정하기 
* ElastiCache Memcached 클러스터에 캐시 노드 추가하기 
* ElastiCache Redis 클러스터 생성하기 
* ElastiCache Redis 클러스터 Security Group 생성 및 설정하기 
* ElastiCache Redis 클러스터 스냅샷 활용하기 
* ElastiCache Redis 클러스터 Read Replica 생성하기
        
## 16. 사용자와 그룹을 생성하여 접근제어 및 권한관리를 제공하는 IAM 
* IAM 그룹 생성하기 
* IAM 사용자 생성하기 
* IAM 사용자로 AWS 콘솔에 접속하기 
* IAM 역할 활용하기 
* IAM 기타 설정 및 기능
        
## 17. AWS 리소스와 연동 가능한 DNS 서비스 Route 53 
* Route 53 Hosted Zone 생성하기 
* Route 53 A 레코드 생성하기 
* Route 53와 S3 연동하기 
* Route 53와 CloudFront 연동하기 
* Route 53 DNS Failover 활용하기 
* Route53 Latency Based Routing, Weighted Round Robin, Geo Routing 설정하기 
* Route 53에서 도메인 구입하기
        
## 18. 부하 분산과 고가용성을 제공하는 ELB 
* ELB 로드 밸런서 생성하기 
* EC2 인스턴스에 웹 서버 실행하기 
* ELB 로드 밸런서 Sticky Session 기능 사용하기
        
## 19. 자동으로 EC2 인스턴스를 생성하여 서비스를 확장하는 Auto Scaling 
* Auto Scaling에 사용할 AMI 생성하기 
* EC2 생성 옵션 설정과 Auto Scaling 그룹 생성하기
        
## 20. 가상 네트워크를 제공하는 VPC 
* VPC 생성하기 
* VPC 서브넷 생성하기 
* VPC 인터넷 게이트웨이 생성하기 
* VPC 기타 설정 및 기능
        
## 21. 데이터 보관 및 백업을 위한 매우 저렴한 스토리지 서비스 Glacier 
* Glacier 볼트 생성하기 
* Glacier 볼트에 파일 올리기 
* Glacier 볼트에서 파일 받기
        
## 22. 서버 구성을 자동화하는 CloudFormation 
* CloudFormation 템플릿 기본 구조 
* EC2 인스턴스를 생성하는 CloudFormation 템플릿 
* EC2 인스턴스를 생성하고 웹 서버를 설치, 실행하는 CloudFormation 템플릿 
* EC2 인스턴스를 생성하고 Security Group을 설정하는 템플릿 
* CloudFormation 템플릿으로 CloudFormation 스택 생성하기
        
## 23. 간편하게 사용하는 애플리케이션 플랫폼 서비스 Elastic Beanstalk 
* Elastic Beanstalk으로 Node.js 애플리케이션과 환경 생성하기 
* AWS 콘솔에서 Elastic Beanstalk Node.js 애플리케이션 배포하기 
* Git으로 Elastic Beanstalk Node.js 애플리케이션 배포하기 
* Elastic Beanstalk 환경 URL 교체로 무중단 배포하기
        
## 24. 애플리케이션 구성과 배포를 자동화하는 OpsWorks 
* OpsWorks 스택 생성하기 
* OpsWorks PHP 레이어 생성하기 
* OpsWorks PHP 인스턴스 생성하기 
* OpsWorks PHP App 생성하기 
* OpsWorks PHP App 배포하기 
* OpsWorks 커스텀 Chef 레시피 사용하기
        
## 25. 검색 서비스를 제공하는 CloudSearch 
* CloudSearch 검색 인스턴스 유형 
* CloudSearch 검색 도메인 생성하기 
* CloudSearch 검색 도메인에 데이터 올리기 
* CloudSearch 검색 도메인에서 검색하기 
* CloudSearch 검색 도메인 엔드포인트 주소 활용하기
        
## 26. 푸시 알림 서비스 SNS 
* SNS 토픽과 이메일 구독 생성하기 
* SNS 토픽에 메시지 보내기 
* SNS로 구글 안드로이드에 푸시 알림 보내기 
* SNS로 애플 iOS에 푸시 알림 보내기
        
## 27. 이메일 전송 서비스 SES 
* 이메일 주소 인증하기 
* 도메인 인증하기 
* 프로덕션 액세스 권한 얻기 
* SES로 테스트 메일 보내기 
* SES SMTP로 메일 보내기
        
## 28. 메시지 큐를 제공하는 SQS 
* SQS 큐 생성하기 
* SQS 처리 실패 큐 생성하기 
* SQS 큐에 메시지 보내기/받기
        
## 29. 동영상 인코딩 서비스 Elastic Transcoder 
* Elastic Transcoder 파이프라인과 작업 생성하기
        
## 30. AWS API, CLI 활용하기 
* Node.js용 AWS SDK 설치하기 
* AWS CLI 설치하기 
* EC2 
* CloudWatch 
* ELB 
* Auto Scaling 
* S3 
* CloudFront 
* DynamoDB 
* CloudSearch 
* SNS 
* SES 
* SQS
        
## 31. 글로벌 사진 사이트 구축하기 
* 이미지, 소스 저장용 S3 버킷 생성하기 
* 이미지 정보 저장용 RDS DB 인스턴스 생성하기 
* 이미지 처리용 SQS 큐 생성하기 
* S3, SQS 접근용 IAM 역할 생성하기 
* 웹 서버용 ELB 로드 밸런서 생성하기 
* 웹 서버, 이미지용 CloudFront 배포 생성하기 
* Route 53로 도메인 연결하기 
* Node.js로 웹 서버 작성하기 
* 웹 서버 AMI 생성하기 
* 웹 서버 Auto Scaling 설정하기 
* Node.js로 이미지 변환 서버 작성 및 구축하기 
* 사진 사이트 동작 확인하기
        
## 32. 자동 확장 가능한 콘서트 티켓 예매 사이트 구축하기 
* 소스 저장용 S3 버킷 생성하기 
* 좌석 데이터 저장용 RDS DB 인스턴스 생성하기 
* 좌석 상태 갱신용 ElastiCache 캐시 클러스터 생성하기 
* S3 접근용 IAM 역할 생성하기 
* 웹 서버용 ELB 로드 밸런서 생성하기 
* 웹 서버용 CloudFront 배포 생성하기 
* Route 53로 도메인 연결하기 
* Node.js로 웹 서버 작성하기 
* 웹 서버 AMI 생성하기
* 웹 서버 Auto Scaling 설정하기 
* 티켓 예매 사이트 동작 확인하기
        
## 33. 자동 확장 가능한 모바일 게임 서버 구축하기
* 소스 저장용 S3 버킷 생성하기 
* 순위 산출용 ElastiCache 캐시 클러스터 생성하기 
* 게임 데이터 저장용 RDS DB 인스턴스 생성하기 
* 로그 저장용 DynamoDB 테이블 생성하기 
* S3, DynamoDB 접근용 IAM 역할 생성하기 
* 게임 서버용 ELB 로드 밸런서 생성하기 
* Route 53로 도메인 연결하기 
* Node.js로 게임 서버 작성하기 
* 게임 서버 AMI 생성하기 
* 게임 서버 Auto Scaling 설정하기기 
* 게임 서버 동작 확인하기
        
## 34. 부록 
* 요금 계산기 
* Windows EC2 인스턴스 사용하기
* S3을 s3fs로 파일시스템처럼 사용하기 
* S3을 s3cmd로 관리하기 
* Auto Scaling 그룹의 EC2 인스턴스에 소스 배포하기 
* AWS Visual Studio 툴킷 
* AWS Eclipse 툴킷 
* 요금 절약하기
