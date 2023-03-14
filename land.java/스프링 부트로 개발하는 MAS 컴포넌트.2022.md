## 1장 마이크로서비스 아키텍처
* 1.3 마이크로서비스 아키텍처 설계
* 1.4 스프링 투어의 아키텍처 변화
* 1.5 12 요소 애플리케이션
	* 1.5.1 코드베이스: 버전 관리되는 하나의 코드베이스와 다양한 배포
	* 1.5.2 의존성: 명시적으로 선언할 수 있고 분리할 수 있는 의존성
	* 1.5.3 설정: 환경 변수를 이용한 설정
	* 1.5.4 지원 서비스: 지원 서비스는 연결된 리소스로 처리
	* 1.5.5 빌드, 릴리스, 실행: 소스 빌드와 실행은 완전히 분리되어야 한다
	* 1.5.6 프로세스: 애플리케이션은 하나 이상의 무상태 프로세스로 실행되어야 한다
	* 1.5.7 포트 바인딩: 포트 바인딩을 통한 서비스 공개
	* 1.5.8 동시성: 프로세스들을 통한 수평 확장
	* 1.5.9 폐기 가능: 프로세스는 빠르게 시작해야 하고 안정적으로 종료해야 한다
	* 1.5.10 Dev 환경과 Production 환경 일치
	* 1.5.11 로그: 로그는 이벤트 스트림으로 다룬다
	* 1.5.12 admin 프로세스: 시스템 유지 보수를 위한 일회성 프로세스


## 2장 프레임워크와 스프링 부트
* 2.1 스프링 투어가 스프링 부트를 선택한 이유
* 2.2 스프링 프레임워크
* 2.3 스프링 부트 소개
* 2.4 스프링 부트 애플리케이션 시작하기
	* 2.4.3 IntelliJ의 이니셜라이저를 사용하여 프로젝트를 구성하는 방법
	* 2.4.5 @SpringBootApplication 애너테이션과 메인 클래스


## 3장 스프링 애플리케이션 기본
* 3.1 스프링 빈 사용
	* 3.1.1 @Bean 애너테이션
* 3.2 자바 설정
	* 3.2.1 @Configuration
	* 3.2.2 @ComponentScan
	* 3.2.3 @Import
* 3.3 스테레오 타입 스프링 빈 사용
	* @Component, @Controller, @Service, @Repository
* 3.4 의존성 주입
	* 3.4.2 애너테이션 기반 설정의 의존성 주입
	* 3.4.3 자바 설정의 의존성 주입
* 3.5 ApplicationContext
* 3.6 스프링 빈 스코프
* 3.7 스프링 빈 생명주기 관리
* 3.8 스프링 빈 고급 정의
	* 3.8.1 @Primary 애너테이션
	* 3.8.2 @Lazy 애너테이션


## 4장 스프링 웹 MVC 개요
* 4.1 HTTP 프로토콜
* 4.2 스프링 웹 MVC 프레임워크
	* 4.2.1 MVC 패턴
	* 4.2.2 DispatcherServlet
	* 4.2.3 서블릿 스택과 스레드 모델
	* 4.2.4 스프링 부트 설정
* 4.3 REST-API 설계
	* 4.3.1 HTTP 메서드별 REST-API 예제
	* 4.3.2 REST-API 특성과 설계
* 4.4 간단한 REST-API 예제
	* 4.4.1 @ResponseBody와 HttpMessageConverter


## 5장 스프링 MVC를 이용한 REST-API 개발
* 5.1 REST-API: GET, DELETE 메서드 매핑
	* 5.1.1 호텔 정보 조회 API 명세서
	* 5.1.2 Controller 클래스 구현
	* 5.1.3 @GetMapping 애너테이션
	* 5.1.4 @PathVariable 애너테이션
	* 5.1.5 @RequestParam 애너테이션
	* 5.1.6 @DeleteMapping 애너테이션
* 5.2 REST-API 응답 메시지 처리
	* 5.2.1 @JsonProperty와 @JsonSerialize 애너테이션: JSON 마셜링 예제
	* 5.2.2 JsonSerializer와 JsonDeserializer 예제
	* 5.2.3 @JsonFormat 애너테이션
	* 5.2.4 열거형 클래스 변환
* 5.3 REST-API POST, PUT 매핑
* 5.4 ResponseEntity 응답과 Pageable, Sort 클래스
	* 5.4.1 ResponseEntity 클래스
	* 5.4.2 페이지네이션과 정렬 파라미터를 위한 Pageable 클래스
	* 5.4.3 Pageable 자동 설정
* 5.5 REST-API 검증과 예외 처리
	* 5.5.1 JSR-303을 사용한 데이터 검증
	* 5.5.2 @Valid 애너테이션과 예제
	* 5.5.3 Validator 인터페이스를 사용한 검증
	* 5.5.4 @ControllerAdvice와 @ExceptionHandler 예외 처리
* 5.6 미디어 콘텐츠 내려받기


## 6장 웹 애플리케이션 서버 구축하기
* 6.1 웹 애플리케이션 기본 설정
	* 6.1.1 웹 애플리케이션의 설정 메커니즘
	* 6.1.2 WebMvcConfigurer를 사용한 설정
	* 6.1.3 DispatcherServlet 설정
* 6.2 HttpMessageConverter와 REST-API 설정
	* 6.2.1 HttpMessageConverter 설정
	* 6.2.2 ObjectMapper와 스프링 빈을 이용한 애플리케이션 설정
* 6.3 Interceptor와 ServletFilter 설정
	* 6.3.1 HandlerInterceptor 인터페이스
	* 6.3.2 Filter 인터페이스
* 6.4 Application.properties 설정
	* 6.4.1 @Value 애너테이션
	* 6.4.2 @ConfigurationProperties와 @ConfigurationPropertiesScan
* 6.5 Profile 설정
	* 6.5.1 Profile 변수 값 설정
	* 6.5.2 프로파일별 application.properties 설정
	* 6.5.3 @Profile 애너테이션과 스프링 빈 설정
	* 6.5.4 @Profile 애너테이션과 인터페이스를 사용한 확장
	* 6.5.5 Environment 인터페이스
* 6.6 REST-API와 국제화 메시지 처리
	* 6.6.1 message.properties 파일 설정
	* 6.6.2 MessageSource 인터페이스
	* 6.6.3 스프링 부트 프레임워크의 자동 설정 구성
	* 6.6.4 LocaleResolver와 LocaleChangeInterceptor 설정 예제
* 6.7 로그 설정
	* 6.7.1 Logger 선언과 사용
	* 6.7.2 logback-spring.xml
	* 6.7.3 중앙 수집 로그
* 6.8 애플리케이션 패키징과 실행
	* 6.8.2 도커 이미지 생성


## 7장 스프링 AOP와 테스트, 자동 설정 원리
* 7.1 스프링 AOP
	* 7.1.1 AOP 용어 정리
	* 7.1.2 어드바이스 종류와 설명
	* 7.1.3 스프링 AOP와 프록시 객체
	* 7.1.4 포인트 컷과 표현식
	* 7.1.5 JoinPoint와 ProceedingJoinPoint
	* 7.1.6 관점 클래스 예제
	* 7.1.7 애너테이션을 사용한 AOP
* 7.2 스프링 부트 테스트
	* 7.2.1 스프링 부트 테스트 설정
	* 7.2.2 Junit 사용 예제
	* 7.2.3 @SpringBootTest를 사용한 스프링 부트 테스트
	* 7.2.4 @TestConfiguration을 사용한 테스트 환경 설정
	* 7.2.5 @MockBean을 사용한 테스트 환경 설정
	* 7.2.6 테스트 슬라이스 애너테이션
	* 7.2.7 스프링 부트 웹 MVC 테스트 예제
	* 7.2.8 JPA 테스트
* 7.3 스프링 부트 자동 설정


## 8장 데이터 영속성
* 8.1 JPA
	* 8.1.1 JPA 소개
	* 8.1.2 ORM과 SQL Mapper 비교
	* 8.1.3 JPA 장단점
* 8.2 MySQL 실행 환경 설정 458
	* 8.2.1 도커를 사용한 MySQL 실행 환경 설정
	* 8.2.2 테이블 설계
* 8.3 Spring Data JPA 기능과 설정
	* 8.3.1 Spring Data JPA 기능
	* 8.3.2 Spring Data JPA 자동 설정과 필수 스프링 빈
	* 8.3.3 Spring Data JPA 설정
	* 8.3.4 Hikari DataSource 설정
* 8.4 엔터티 클래스 설계
	* 8.4.1 엔터티 클래스와 @Entity 애너테이션
	* 8.4.2 엔터티 클래스 기본 키 설정
	* 8.4.3 열거형과 @Enumerated
	* 8.4.4 Date 클래스와 @Temporal
	* 8.4.5 엔터티 클래스 속성 변환과 AttributeConverter
	* 8.4.6 엔터티 클래스 상속과 @MappedSuperClass
* 8.5 리포지터리 개발과 JpaRepository
* 8.6 Spring Data JPA의 쿼리 메서드 기능
	* 8.6.1 메서드 이름으로 쿼리 생성
	* 8.6.2 예제와 테스트 케이스
	* 8.6.3 @Query 애너테이션을 사용한 쿼리 사용
* 8.7 트랜잭션과 @Transactional
	* 8.7.1 @Transactional 애너테이션
	* 8.7.2 @Transactional의 propagation 속성
	* 8.7.3 @Transactional 애너테이션의 isolation 속성
	* 8.7.4 트랜잭션 테스트 예제
	* 8.7.5 @Transactional을 사용할 때 주의 사항
* 8.8 EntityManager
	* 8.8.1 EntityManager와 영속성 컨텍스트
	* 8.8.2 영속성 컨텍스트의 특징
* 8.9 엔터티 연관 관계 설정
	* 8.9.1 연관 관계 설계
	* 8.9.2 일대다 연관 관계 설정
	* 8.9.3 영속성 전이와 로딩, 고아 객체
	* 8.9.4 다대일 연관 관계 설정
	* 8.9.5 양방향 관계 설정
	* 8.9.6 다대다 연관 관계 설정
	* 8.9.7 일대일 연관 관계 설정
* 8.10 엔터티 상태 이벤트 처리
* 8.11 트랜잭션 생명주기 동기화 작업
	* 8.11.1 스프링 부트 프레임워크의 OSIV 설정


## 9장 애플리케이션 통합: REST-API
* 9.1 RestTemplate 클래스
	* 9.1.1 RestTemplate 구조
	* 9.1.2 RestTemplate 스프링 빈 설정
	* 9.1.3 Connection Timeout과 Read Timeout 설정
	* 9.1.4 RestTemplate 클래스
	* 9.1.5 RestTemplate 예제
	* 9.1.6 keep-alive와 Connection Pool 설정
* 9.2 WebClient


## 10장 레디스와 스프링 캐시
* 10.1 레디스 소개 및 아키텍처
	* 10.1.1 레디스 센티넬 아키텍처
	* 10.1.2 레디스 클러스터 아키텍처
	* 10.1.3 레디스 자료 구조
	* 10.1.4 레디스 유효 기간
* 10.2 Spring Data Redis 사용
	* 10.2.1 RedisAutoConfiguration 자동 설정
	* 10.2.2 레디스 도커 설정
* 10.3 Lettuce 라이브러리와 커넥션 설정
	* 10.3.1 RedisConnectionFactory 설정
* 10.4 레디스 문자열 예제와 RedisSerializer 설정
* 10.5 레디스 분산 락 사용 예제
* 10.6 레디스 Sorting 구현 예제
* 10.7 레디스 Pub-Sub 구현 예제
	* 10.7.1 토픽과 메시지 객체
	* 10.7.2 게시자 예제
	* 10.7.3 구독자 예제
	* 10.7.4 게시자와 구독자 테스트
* 10.8 스프링 프레임워크 캐시
	* 10.8.1 Cache와 CacheManager 인터페이스
	* 10.8.2 캐시 애너테이션


## 11장 스프링 스케줄링 태스크
* 11.1 스케줄링 설정
	* 11.1.1 SchedulingConfigurer를 사용한 TaskScheduler 설정
	* 11.1.2 ScheduledAnnotationBeanPostProcessor와 TaskScheduler 설정
* 11.2 스케줄링 태스크 정의
	* 11.2.1 cron 속성과 클론 표현식
	* 11.2.2 fixedDelay 속성
	* 11.2.3 fixedRate 속성
* 11.3 배치 서버 아키텍처
	* 11.3.1 단독 배치 서버 구성
	* 11.3.2. 젠킨스와 REST-API 서버군 구성
	* 11.3.3 @Scheduled와 REST-API 서버군 구성


## 12장 스프링 이벤트
* 12.1 스프링 이벤트 장점
* 12.2 사용자 정의 이벤트 처리
* 12.3 비동기 사용자 정의 이벤트 처리
* 12.4 @Async 애너테이션을 사용한 비동기 이벤트 처리
* 12.5 @EventListener
* 12.6 스프링 애플리케이션 이벤트
* 12.7 트랜잭션 시점에 구독한 이벤트 처리


## 부록 A 예제 코드 사용법
* A.1 예제 코드 실행하기
* A.2 도커 이미지 생성하기