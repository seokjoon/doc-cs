# CHAPTER 2 개인이 DevOps 시작하기

## 2.3 개인 환경에서 팀 환경으로 가져가기 위한 준비
* 2.3.1 Vagrant로 Local 개발 환경의 Infrastructure as Code화
* 2.3.2 Ansible로 보다 범용적으로 구축하고 다른 환경으로 전개
* 2.3.3 Serverspec으로 인프라 구축 테스트를 코드화한다
* 2.3.4 Git을 이용하여 필요한 구성 정보를 팀에 공유할 수 있도록 한다
* 2.3.5 Infrastructure as Code와 DevOps의 Goal


# CHAPTER 3 팀으로 DevOps 확대하기

## 3.2 팀으로 수행하는 작업 효율화
* 3.2.1 GitHub에서 팀 개발을 수행
* 3.2.2 Docker를 이용하여 개발을 더욱 효율적으로 진행
* 3.2.3 Jenkins를 이용하여 작업을 관리한다
* 3.2.4 지속적 통합(CI)과 지속적 딜리버리(CD)로 release 최적화


# CHAPTER 4 DevOps를 위해 구조를 바꾼다

## 4.2 어플리케이션, 아키텍처를 변경한다
* 4.2.1 The Twelve-Factor App
* 4.2.2 마이크로 서비스 아키텍처
## 4.3 인프라 아키텍처를 변경한다
* 4.3.1 Immutable Infrastructure에 의한 효율적인 인프라 관리
* 4.3.2 Blue-Green Deployment로 서비스를 전환
* 4.3.3 온프레미스 vs 퍼블릭 클라우드
* 4.3.4 SaaS
* 4.3.5 로그 수집과 분석
## 4.4 팀을 바꾼다
* 4.4.1 DevOps와 애자일 개발
* 4.4.2 티켓 구동 개발
* 4.4.3 Site Reliability Engineering
* 4.4.4 ChatOps


# CHAPTER 5 실천 Infrastructure as Code

## 5.1 실천 지속적 통합·지속적 딜리버리
* 5.1.2 GitHub와 Slack 연결 : GitHub의 이벤트를 Slack에게 통지한다
* 5.1.3 GitHub와 Jenkins 연결 : git push 하면 처리가 실행된다
* 5.1.4 Jenkins와 Slack의 연결 : Job 이벤트를 Slack에 통지한다
* 5.1.5 Jenkins와 Ansible 연결 : Job에 의해 인프라 구축을 수행
* 5.1.6 Jenkins와 Serverspec 연결 : Job에 의한 인프라 테스트를 실시
* 5.1.7 GitHub에서 Jenkins 프로비저닝을 연결

## 5.2 실천 ELK Stack
* 5.2.1 ELK Stack의 구성 요소와 연결
* 5.2.2 ELK Stack 구축
* 5.2.3 Access 로그를 가시화

## 5.3 실천 Immutable Infrastructure
* 5.3.1 Immutable Infrastructure를 실현하는 요소와 Release 프로세스
* 5.3.2 CloudFormation을 이용하여 기본이 되는 환경을 구축한다
* 5.3.3 Blue-Green Deployment를 이용한 Release 수행
* 5.3.4 장애 발생 시 인프라를 전환한다