# 섹션1 Oracle Cloud Infrastructure의 핵심 개념

## 1장 Oracle Cloud Infrastructure 소개
* 리전과 가용성 도메인
* OCI 콘솔에서 리전 관리하기
* Oracle Cloud Infrastructure 구성요소의 논리적 뷰
* 테넌시
* 부트스트랩
* 컴파트먼트
* Oracle 클라우드 식별자 (OCIDs)
* 오프박스 가상화
* 오프박스 가상화의 보안상 이점
* 폴트 도메인


## 2장 계정과 권한 관리의 이해
* 프린서펄
* 루트 사용자
* IAM 사용자/그룹
* 인스턴스 프린서펄
* 권한 부여
* 컴파트먼트를 사용하여 리소스 구성
* 설계 고려사항
* 컴파트먼트 레퍼런스 모델
* 컴파트먼트 탐색기
* 정책을 사용하여 컴파트먼트에서 리소스에 접근
* 명령
* 정책 상속
* 정책 할당
* 인스턴스 프린서펄을 사용해서 OCI API 호출
* 인스턴스 Principal 생성하기
* 써드파티 IdP를 사용하여 OCI 액세스 통합
* 통합 설정


## 3장 Oracle Cloud Infrastructure에서 네트워크 설계
* VCN의 하이레벨 아키텍처
* VCN 구성요소
* 서브넷
* VNIC
* 프라이빗 IP 주소
* 퍼블릭 IP 주소
* 인터넷 게이트웨이
* 라우트 테이블
* 다이나믹 라우팅 게이트웨이
* NAT 게이트웨이
* 서비스 게이트웨이
* 로컬 피어링(리전 내에서)
* 원격 피어링(리전을 넘어)
* 씨큐리티 리스트
* 네트워크 보안 그룹
* 스테이트풀과 스테이트리스 보안 규칙
* 기본 VCN 구성 요소
* VCN 구성 요소 검토하기
* 연결 선택
* 퍼블릭 인터넷을 통해 연결하기
* VPN을 통해 연결하기
* FastConnect를 통해 연결하기
* 로드 밸런서
* 퍼블릭 로드 밸런서
* 프라이빗 로드 밸런서
* 로드 밸런싱 정책
* 헬스 체크
* SSL 처리
* 세션 지속성
* 라우팅 요청하기 - 가상 호스트 네임 및 경로 라우팅
* VCN 플로우 로그
* VCN 플로우 로그 구성하기


## 4장 Oracle Cloud Infrastructure에서 Compute 선택
* 다양한 OCI Compute 인스턴스 종류의 소개
* 인스턴스 형태 이해하기
* Compute 인스턴스용 스토리지
* 인스턴스 부트 볼륨
* 인스턴스 운영체제 이미지 이해
  * user: opc(oracle, cent), ubuntu(ubuntu)
* 커스텀 이미지
* 이미지 내보내기와 가져오기
* 자체 이미지 가져오기 (BYOI)
* 자체 하이버파이저 가져오기 (BYOH)
* 인스턴스 구성과 인스턴스 풀을 사용하여 비슷한 인스턴스 생성
* 컴퓨트 인스턴스 메트릭
* 오토스케일링 구성
* 인스턴스 콘솔 연결을 사용해 인스턴스 연결
  * 부팅 실패시
* 맥OS나 Linux OS에서 직렬 콘솔에 연결하기


## 5장 Oracle Cloud Infrastructure에서 스토리지 옵션 이해
* OCI 블록 볼륨
* 블록 볼륨 생성하기
* 블록 볼륨 크기 변경하기
* 인스턴스에 블록 볼륨 연결하기
* 블록 볼륨의 백업 및 복구하기
* 블록 볼륨 복제하기
* 볼륨 그룹
* 블록 볼륨 작업 - 공유 멀티 연결
* OCI 파일 스토리지 서비스
* 파일시스템 생성하기
* 파일시스템 보안
* OCI 오브젝트 스토리지
* 사전 인증된 요청
* 리전간 복사하기
* 멀티파티 업로드하기


# 섹션2: Oracle Cloud Infrastructure에서 추가 레이어 이해하기

## 6장 Oracle Cloud Infrastructure에서 데이터베이스 선택 이해
* OCI 데이터베이스 선택에 대한 논의
* VM 데이터베이스 시스템
* 베어메탈 데이터베이스 시스템
* Exadata 데이터베이스 시스템
* Oracle의 자율운영 데이터베이스 서비스 관리


## 7장 Oracle Cloud Infrastructure에서 클라우드 네이티브 애플리케이션 구축
* 클라우드 네이티브 애플리케이션의 진화
* OCI 레지스트리에 애플리케이션 이미지 저장하기
* 레지스트리에서 이미지 푸시 및 풀 준비하기
* 레포지토리 생성하기
* Docker 컨테이너 이미지 생성하기
* Docker 컨테이너 이미지 푸시와 풀 하기
* OKE에 마이크로서비스 배포
* 쿠버네티스 시작하기
* 쿠버네티스용 Oracle 컨테이너 엔진 시작하기
* OKE 클러스터 생성하기
* OKE 클러스터 액세스하기
* OKE 클러스터에 샘플 웹 애플리케이션 배포하기
* OKE 클러스터의 쿠버네티스 버전 업그레이드하기
* OCI API 게이트웨이를 사용하여 마이크로서비스 노출
* 클라우드 환경 내의 API 게이트웨이
* 클라우드에서 온프레이스 모델로의 API 게이트웨이
* 하이브리드형 모델의 API 게이트웨이
* 프라이빗 클라우드 모델의 API 게이트웨이
* API 게이트웨이 개념
* API 게이트웨이 생성하기
* API 게이트웨이 배포 생성하기
* API 게이트웨이를 통해 API 엔드포인트에 액세스하기


## 8장 Oracle Cloud Infrastructure에서 서버리스 애플리케이션 실행
* 서버리스 컴퓨팅 개념 이해
* Oracle 함수의 중요성 이해하기
* Oracle 함수의 사용 사례 이해하기
* Oracle 함수의 생성 및 사용
* Oracle 함수를 깊게 알아보기
* 이벤트 기반의 Oracle 함수 사용의 이해


## 9장 Oracle Cloud Infrastructure에서 코드로 인프라 관리
* IaC의 필요성에 대한 이해
* ORM의 사용 사례에 대한 이해
* ORM 구성요소
* 기존 설정에서의 IaC 생성 학습
* ORM과 SCM을 통합하는 방법 학습


## 10장 CLI/API/SDK를 사용하여 Oracle Cloud Infrastructure와 상호작용
* OCI 리소스들과의 상호작용을 위해 OCI CLI 사용
* OCI SDK를 사용하여 OCI 작업 자동화
* OCI 관리를 위한 REST 호출을 전송을 위해 OCI API 사용


## 11장 Oracle 클라우드 VMware 솔루션을 사용하여 Oracle Cloud Infrastructure에서 하이브리드 클라우드 구축
* OCVS 솔루션의 개요 이해
* 가상 클라우드 네트워크(VCN)
* 컴퓨트 - VMware vSphere(ESXi)
* 네트워킹 -VMware NSX-T
* 스토리지 - Vmware vSAN
* OCVS 배포
* OCVS 클러스터 배포
* OCVS 클러스터 액세스
* OCVS 클러스터 인터넷에 연결
