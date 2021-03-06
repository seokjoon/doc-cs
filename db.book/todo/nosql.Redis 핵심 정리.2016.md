## 1장. 시작하기 (기초 단계)
* 설치
* Hello Redis(커맨드라인 인터페이스 예제)
* 노드 설치
* 속성 자바스크립트 문법 가이드
* 노드와 레디스를 이용한 Hello World
* 레디스 데이터 타입
	* 문자열
    * 리스트
    * 해시

## 2장. 고급 데이터 타입(검은 띠 따기)
* 셋
* 정렬된 셋
* 비트맵
* 하이퍼로그로그

## 3장. 시계열(관찰 집합)
* 기초 구축
* 해시로 최적화
* 정렬된 셋과 하이퍼로그로그를 사용한 유일한 엘리먼트 추가

## 4장. 커맨드(괴물들이 사는 나라)
* Pub/Sub
* 트랜잭션
* 파이프라인
* 스크립트
    * 루아 기본 문법
    * 레디스, 루아를 만나다
* 기타 커맨드
    * INFO
    * DBSIZE
    * DEBUG SEGFAULT
    * MONITOR
    * CLIENT LIST와 CLIENT SETNAME 커맨드
    * CLIENT KILL
    * FLUSHALL
    * RANDOMKEY
    * EXPIRE와 EXPIREAT
    * TTL과 PTTL
    * PERSIST
    * SETEX
    * DEL
    * EXISTS
    * PING
    * MIGRATE
    * SELECT
    * AUTH
    * SCRIPT KILL
    * SHUTDOWN
    * OBJECT ENCODING
* 데이터 타입의 최적화
    * 문자열
    * 리스트
    * 셋
    * 해시
    * 정렬된 셋
    * 메모리 사용 측정

## 5장. 선호하는 언어의 클라이언트(여러 언어로 레디스 다루기)
* PHP
    * PHP의 기본 커맨드
    * PHP의 블로킹 커맨드
    * PHP의 파이프라인
    * PHP의 트랜잭션
    * PHP에서의 스크립트 사용
* 파이썬
    * 파이썬의 기본 커맨드
    * 파이썬의 블로킹 커맨드
    * 파이썬의 파이프라인
    * 파이썬의 트랜잭션
    * 파이썬에서의 스크립트 사용
* 루비
    * 루비의 기본 커맨드
    * 루비의 블로킹 커맨드
    * 루비의 파이프라인
    * 루비의 트랜잭션
    * 루비에서 스크립트의 사용

## 6장. 일반적인 실수(실수 피하기)
* 작업에 대한 잘못된 데이터 타입
    * 셋을 이용한 접근 방식
    * 비트맵을 이용한 접근 방식
* 다중 레디스 데이터베이스
* 스왑 사용
* 메모리를 적절하게 설정하지 않기
* 부적절한 저장 전략

## 7장. 보안 기술(데이터 보호하기)
* 기본적인 보안
    * 중요한 커맨드를 알기 어렵게 하기
* 네트워크 보안
    * 방화벽 규칙으로 레디스 보호
    * 루프백 네트워크 인터페이스로 레디스 실행
    * 가상 사설 클라우드에서 레디스 실행
* 클라이언트와 서버 간의 통신 암호화
    * 클라이언트와 서버에서 stunnel 실행하기
    * 서버에서의 stunnel 실행 및 SSL을 지원하는 레디스 클라이언트 사용

## 8장. 레디스 확장하기(싱글 인스턴스 넘어서기)
* 저장
    * 레디스 데이터베이스(RDB)
    * AOF
    * RDB 대 AOF
* 복제
* 파티셔닝
    * 범위 파티셔닝
    * 해시 파티셔닝
    * 미리 샤딩하기
    * 일관적 해싱
    * 태깅
    * 데이터 저장소 대 캐시
    * 레디스 파티셔닝의 구현
* 트웸프록시로 자동 샤딩하기
    * 트웸프록시를 사용한 다른 아키텍처

## 9장. 레디스 클러스터와 레디스 센티널(집단 지성)
* CAP 정리
* 레디스 센티널
    * 기본 센티널 설정
    * 센티널에 연결
    * 네트워크 파티션(스플릿-브레인)
* 레디스 클러스터
    * 해시 슬롯
    * 해시 태그
    * 기본 클러스터의 생성
    * 노드 검색과 리디렉트
    * 설정
    * 다른 레디스 클러스터 아키텍처
    * 클러스터 관리
    * * 클러스터 생성
    * * 슬레이브/복제본 추가
    * * 슬레이브 노드를 이용해 읽기 확장
    * * 노드 추가
    * * 노드 삭제
    * * redis-trib 툴을 이용한 레디스 클러스터 관리
