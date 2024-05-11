## 1장. 연관관계
* 항목 1: @OneToMany 연관관계를 효과적으로 구성하는 방법
  * 항상 부모 측에서 자식 측으로 전이를 사용
  * 부모 측에 mappedBy 지정
  * 부모 측에 orphanRemoval 지정
  * 연관관계의 양측을 동기화 상태로 유지
  * equals()와 hashCode() 오버라이딩
  * 연관관계 양측에서 지연 로딩 사용
  * toString() 오버라이딩 방법에 주의
  * @JoinColumn을 사용해 조인 칼럼 지정
  * Author 및 Book 샘플 코드
* 항목 2: 단방향 @OneToMany 연관관계를 피해야 하는 이유
  * 일반적인 단방향 @OneToMany
  * @OrderColumn 사용
  * @JoinColumn 사용
* 항목 3: 단방향 @ManyToOne의 효율성
  * 특정 저자에게 새 도서 추가
  * 저자의 모든 도서 가져오기
  * 저자의 도서 페이징 처리
  * 저자의 모든 도서 가져오기와 새로운 도서 추가
  * 저자의 모든 도서 가져오기와 도서 삭제
* 항목 4: @ManyToMany 연관관계를 효과적으로 구성하는 방법
  * 관계의 오너 선택
  * 항상 List가 아닌 Set 사용
  * 연관관계의 양측 동기화 상태 유지
  * CascadeType.ALL 및 CascadeType.REMOVE 사용하지 않기
  * 조인 테이블 설정
  * 연관관계 양측에서 지연 로딩 사용
  * equals() 및 hashCode() 오버라이딩
  * toString() 오버라이딩 방법에 주의
  * Author 및 Book 샘플 코드
* 항목 5: @ManyToMany에서 Set이 List보다 나은 이유
  * List 사용
  * Set 사용
* 항목 6: CascadeType.REMOVE 및 orphanRemoval=true를 사용해 하위 엔터티 제거를 피해야 하는 이유와 시기
  * 영속성 콘텍스트에 이미 로드된 저자 삭제
  * 하나의 저자만 영속성 콘텍스트에 로드된 경우
  * 여러 저자가 영속성 콘텍스트에 로드된 경우
  * 한 저자와 관련 도서들이 영속성 콘텍스트에 로드된 경우
  * 삭제해야 할 저자와 도서가 영속성 콘텍스트에 로드되지 않은 경우 삭제
* 항목 7: JPA 엔터티 그래프를 통해 연관관계를 가져오는 방법
  * NamedEntityGraph로 엔터티 그래프 정의
  * 쿼리 메서드 오버라이딩
  * 쿼리 빌더 메커니즘 사용
  * Specification 사용
  * @Query 및 JPQL 사용
  * 애드혹 엔터티 그래프
  * EntityManager를 통한 엔터티 그래프 정의
* 항목 8: JPA 엔터티 서브그래프를 통해 연관관계를 가져오는 방법
  * @NamedEntityGraph 및 @NamedSubgraph 사용
  * 애드혹 엔터티 그래프에서 점 노테이션(.) 사용
  * EntityManager를 통한 엔터티 서브그래프 정의
* 항목 9: 엔터티 그래프 및 기본 속성 처리 방법
* 항목 10: 하이버네이트 @Where 어노테이션을 통한 연관관계 필터링 처리
* 항목 11: @MapsId를 통한 단방향/양방향 @OneToOne 최적화 방법
  * 일반적인 단방향 @OneToOne
  * 일반적인 양방향 @OneToOne
  * @OneToOne을 구원하는 @MapsId
* 항목 12: 단 하나의 연관관계만 Null이 아닌지 확인하는 방법
  * 테스트 확인


## 2장. 엔터티
* 항목 13: 엔터티의 플루언트 API 스타일 적용 방법
  * 엔터티 세터를 통한 플루언트 스타일
  * 별도 메서드를 통한 플루언트 스타일
* 항목 14: 하이버네이트 프록시를 통한 자식 측에서 부모 연관관계 채우기
  * findById() 사용
  * getOne() 사용
* 항목 15: 영속성 레이어에서 자바 8 Optional 사용 방법
  * 엔터티에서의 Optional
  * 리포지터리에서의 Optional
* 항목 16: 불변 엔터티 작성 방법
* 항목 17: 엔터티 복제 방법
  * 부모 복제와 도서에 대한 연관관계 지정
  * 부모 및 도서 복제
  * 하나로 처리
* 항목 18: 더티 트래킹을 활성화하는 이유와 방법
* 항목 19: 불리언을 Yes/No로 매핑하는 방법
* 항목 20: 애그리거트 루트로부터 최적의 도메인 이벤트 발행
  * 동기식 실행
  * 비동기식 실행


  3장. 페치
* 항목 21: 다이렉트 페치 사용 방법
  * 스프링 데이터를 통한 다이렉트 페치
  * EntityManager를 통한 다이렉트 페치
  * 하이버네이트 Session을 통한 다이렉트 페치
  * 다이렉트 페치 및 세션 수준 반복 읽기
  * ID로 여러 엔터티 다이렉트 페치
* 항목 22: 미래 영속성 콘텍스트에서 데이터베이스 변경 사항 전파를 위한 읽기 전용 엔터티의 사용 이유
  * 읽기-쓰기 모드로 Author 로드
  * 읽기 전용 모드로 Author 로드
  * Author 수정
* 항목 23: 하이버네이트 Bytecode Enhancement를 통한 엔터티 속성 지연 로딩 방법
  * 속성에 대한 지연 로딩 활성화
  * 속성 지연 로딩과 N+1
  * 속성 지연 로딩과 지연 초기화 예외
  * 지연 로드 속성에 대한 명시적 기본값 지정
  * 커스텀 Jackson 필터 제공
* 항목 24: 서브엔터티를 통한 엔터티 속성 지연 로딩 방법
* 항목 25: 스프링 프로젝션을 통한 DTO 가져오기
  * JPA 네임드 (네이티브) 쿼리 및 스프링 프로젝션 결합 사용
  * 클래스 기반 프로젝션
  * 스프링 프로젝션 재사용 방법
  * 동적 스프링 프로젝션 사용 방법
* 항목 26: 스프링 프로젝션에서 엔터티를 추가하는 방법
  * 구체화된 연관관계
  * 구체화되지 않은 연관관계
* 항목 27: 엔터티의 일부 또는 외부 가상 속성을 통한 스프링 프로젝션 보완 방법
* 항목 28: *-to-One 연관관계를 포함하는 스프링 프로젝션의 효율적 로딩 방법
  * 중첩된 닫힌 프로젝션 사용
  * 단순 닫힌 프로젝션 사용
  * 단순 열린 프로젝션 사용
* 항목 29: 연관된 컬렉션을 포함하는 스프링 프로젝션 주의 사항
  * 중첩된 닫힌 프로젝션 사용
  * 단순 닫힌 프로젝션 사용
  * DTO에서 List〈Object[]〉 변환
* 항목 30: 스프링 프로젝션을 통한 모든 속성 가져오는 방법
  * 쿼리 빌더 메커니즘 사용
  * JPQL 및 @Query 사용
  * 명시적 칼럼 목록 및 @Query와 함께 JPQL 사용
  * 네이티브 쿼리와 @Query 사용
* 항목 31: 생성자 표현식을 통해 DTO를 가져오는 방법
* 항목 32: 생성자 표현식을 통해 DTO에서 엔터티를 가져오지 말아야 하는 이유
* 항목 33: JPA Tuple을 통해 DTO를 가져오는 방법
* 항목 34: @SqlResultSetMapping 및 @NamedNativeQuery를 통해 DTO를 가져오는 방법
  * 스칼라 매핑
  * 생성자 매핑
  * 엔터티 매핑
* 항목 35: ResultTransformer를 통해 DTO를 가져오는 방법
* 항목 36: 커스텀 ResultTransformer를 통해 DTO를 가져오는 방법
* 항목 37: @Subselect를 통해 엔터티를 쿼리에 매핑하는 방법
* 항목 38: Blaze-Persistence 엔터티 뷰를 통해 DTO를 가져오는 방법
* 항목 39: 단일 SELECT로 부모와 연관관계를 효율적으로 가져오는 방법
* 항목 40: JOIN과 JOIN FETCH 결정 방법
  * 주어진 가격보다 비싼 저서를 저술한 모든 저자 가져오기
  * 모든 저서와 저자 가져오기
* 항목 41: 모든 왼쪽 엔터티를 가져오는 방법
* 항목 42: 관련 없는 엔터티로부터 DTO를 가져오는 방법
* 항목 43: JOIN문 작성 방법
  * INNER JOIN
  * LEFT JOIN
  * RIGHT JOIN
  * CROSS JOIN
  * FULL JOIN
  * MySQL에서 FULL JOIN 시뮬레이션
* 항목 44: JOIN 페이지네이션 방법
  * DENSE_RANK() 윈도우 함수 해결 방안
  * 항목 45: 결과 세트를 스트림하는 방법(MySQL) 및 Streamable 유틸리티의 사용 방법
  * 결과 세트 스트리밍(MySQL)
  * Streamable 유틸리티와 스트링 혼동하지 않기
  * 필요보다 더 많은 열을 가져와 map()을 통해 일부 삭제하지 않기
  * 필요보다 더 많은 행을 가져와 filter()을 통해 일부 삭제하지 않기
  * and()를 통한 Streamable 결합에 주의
  * 커스텀 Streamable 래퍼 타입을 반환하는 방법


## 4장. 배치 처리
* 항목 46: 스프링 부트 스타일 배치 등록 방법
  * 배치 처리 활성화 및 JDBC URL 설정
  * 배치 등록을 위한 엔터티 준비
  * 내장 saveAll(Iterable〈S〉 entities) 단점 확인 및 방지
  * 올바른 방법의 커스텀 구현
  * 테스트 확인
* 항목 47: 부모-자식 관계 배치 등록 최적화 방법
  * 배치 순서 지정
  * 항목 48: 세션 수준에서 배치 크기 제어 방법
  * 항목 49: 포크/조인 JDBC 배치 처리 방법
  * 포크/조인 배처 처리
* 항목 50: CompletableFuture를 통한 엔터티 배치 처리
* 항목 51: 배치 업데이트에 대한 효율적인 처리 방법
  * 버전이 지정된 엔터티
  * 부모-자식 관계의 배치 업데이트
  * 벌크 업데이트
* 항목 52: 효율적으로 배치 삭제하는 방법(연관관계 없이)
  * deleteAllInBatch() 내장 메서드를 통한 삭제
  * deleteInBatch(Iterable〈T〉 entities) 내장 메서드를 통한 삭제
  * deleteAll() 내장 메서드를 통한 삭제
  * delete(T entity) 내장 메서드를 통한 삭제
* 항목 53: 효율적으로 배치 삭제하는 방법(연관관계와 함께)
  * orphanRemoval=true 사용
  * deleteAllInBatch() 내장 메서드를 통한 삭제
  * deleteInBatch(Iterable〈T〉 entities) 내장 메서드를 통한 삭제
  * deleteAll(Iterable〈? extends T〉 entities)와 delete(T entity) 내장 메서드를 통한 삭제
  * SQL, ON DELETE CASCADE 사용
  * deleteAllInBatch() 내장 메서드를 통한 삭제
  * deleteInBatch(Iterable〈T〉 entities) 내장 메서드를 통한 삭제
  * deleteAll(Iterable〈? extends T〉 entities)와 delete(T entity) 내장 메서드를 통한 삭제
* 항목 54: 배치로 연관관계 가져오는 방법
  * 컬렉션 수준에서의 @BatchSize
  * 클래스/엔터티 수준에서의 @BatchSize
* 항목 55: 배치 등록에서 PostgreSQL (BIG)SERIAL을 피해야 하는 이유
  * 식별자 가져오기 프로세스 최적화
  * reWriteBatchedInserts를 통한 배치 최적화


## 5장. 컬렉션
* 항목 56: @ElementCollection 컬렉션 JOIN FETCH 방법
* 항목 57: @ElementCollection에 대한 DTO 방법
* 항목 58: @ElementCollection과 @OrderColumn을 함께 사용해야 하는 이유와 시기
  * @OrderColumn을 통한 @ElementCollection 최적화
* 항목 59: 엔터티 컬렉션 병합 방법
  * Detached 컬렉션 병합
  * 테스트 확인


## 6장. 커넥션과 트랜잭션
* 항목 60: 실제 필요 시점까지 커넥션 획득 지연 방법
* 항목 61: @Transactional(readOnly=true)의 실제 작동 방식
* 항목 62: 스프링이 @Transactional을 무시하는 이유
* 항목 63: 트랜잭션 타임아웃 설정 및 롤백이 예상대로 작동하는지 확인하는 방법
  * 트랜잭션 및 쿼리 타임아웃 설정
  * 트랜잭션이 롤백됐는지 확인
* 항목 64: 리포지터리 인터페이스에서 @Transactional을 사용하는 이유와 방법
  * 인터페이스 리포지터리의 쿼리 메서드는 기본적으로 트랜잭션 콘텍스트에서 실행되는가?
  * 그럼 해야 할 일은 서비스 메서드 수준에서 @Transactional을 추가하는 것뿐인가?
  * 그럼 일반적 해당 방법으로 항상 충분한가?
  * 알았다. 리포지터리 인터페이스로 @Transactional을 이동하자
  * 그러나 서비스 메서드에서 더 많은 쿼리 메서드를 호출하려면 어떻게 해야 할까? ACID를 잃게 될까?
  * 그럼 커넥션 획득을 지연하면 리포지터리 인터페이스에 @Transactional을 사용하지 않아도 되는가?
  * 간단하고 일반적인 3가지 시나리오

  7장. 식별자
* 항목 65: MySQL에서 하이버네이트 5 AUTO 생성자 타입을 피해야 하는 이유
* 항목 66: hi/lo 알고리듬을 통한 시퀀스 식별자 생성 최적화 방법
  * 외부 시스템 처리
* 항목 67: Pooled(-lo) 알고리듬을 통한 시퀀스 식별자 생성 최적화 방법
  * Pooled 알고리듬
  * Pooled-Lo 알고리듬
* 항목 68: equals() 및 hashCode()를 올바로 오버라이드하는 방법
  * 단위 테스트 구성
  * equals() 및 hashCode() 오버라이딩을 위한 최적의 접근 방법
  * 피해야 할 equals() 및 hashCode() 오버라이딩 방법
* 항목 69: 스프링 스타일로 하이버네이트 @NaturalId를 사용하는 방법
  * 테스트 확인
  * 복합 자연 ID
* 항목 70: 하이버네이트 @NaturalId 사용 및 엔터티 식별자 조회 생략 방법
  * @NaturalIdCache 단독으로 사용
  * @NaturalIdCache 및 @Cache 사용
* 항목 71: @NaturalId 칼럼 참조 연관관계 정의 방법
  * 테스트 확인
* 항목 72: 자동 생성 키를 얻는 방법
  * getId()를 통한 자동 생성 키 가져오기
  * JdbcTemplate을 통한 자동 생성 키 가져오기
  * SimpleJdbcInsert를 통한 자동 생성 키 가져오기
* 항목 73: 커스텀 시퀀스 ID를 생성하는 방법
* 항목 74: 복합 기본키를 효율적으로 구현하는 방법
  * @Embeddable 및 @EmbeddedId를 사용한 복합키
  * @IdClass를 사용한 복합키
  * UUID는 어떨까?
  * GenerationType.AUTO를 통한 UUID 생성
  * 직접 할당되는 UUID
  * 하이버네이트 uuid2
* 항목 75: 복합키에서 관계를 정의하는 방법
  * 테스트 확인
  * Publisher 저장
  * 2명의 Author 저장
  * 이름으로Author 조회
  * Author의 Book 삭제
  * Author 삭제
* 항목 76: 연결 테이블에 대한 엔터티 사용 방법
  * 연결 테이블에 대한 복합 기본키 정의
  * 연결 테이블에 대한 엔터티 정의
  * Author와 Book 연결


## 8장. 산출 속성
* 항목 77: 산출된 비영속 속성 매핑 방법
  * JPA 빠른 접근
  * JPA @PostLoad
  * 하이버네이트 @Formula
* 항목 78: @Generated를 통한 산출된 영속 속성 매핑 방법
  * 하이버네이트 @Generated
  * columnDefinition 항목을 통한 공식
  * CREATE TABLE을 통한 공식
  * 테스트 확인
* 항목 79: JPQL 쿼리에서 여러 파라미터와 함께 SQL 함수 사용 방법
  * SELECT 부분의 함수
  * WHERE 부분의 함수
* 항목 80: @JoinFormula를 통해 @ManyToOne 관계를 SQL 쿼리에 매핑하는 방법


## 9장. 모니터링
* 항목 81: SQL문 카운트 및 어설션 사용 이유와 방법
* 항목 82: 프리페어드 스테이트먼트 바인딩 및 추출 파라미터 로깅 방법
  * TRACE
  * Log4j 2
  * MySQL과 profileSQL=true
* 항목 83: 쿼리 상세 정보 로깅 방법
  * DataSource-Proxy 사용
  * log4jdbc 사용
  * P6spy 사용
* 항목 84: 임계치를 사용한 느린 쿼리 로그 방법
* 항목 85: 트랜잭션 및 쿼리 메서드 상세 로깅
  * 트랜잭션 상세 로깅
  * 트랜잭션 콜백을 통한 제어권 확보
  * 쿼리 메서드 실행 시간 로깅

  10장. DataSource 및 커넥션 풀 설정
* 항목 86: HikariCP 설정 커스터마이징 방법
  * application.properties를 통한 HikariCP 파리미터 최적화
  * application.properties 및 DataSourceBuilder를 통한 HikariCP 파리미터 최적화
  * DataSourceBuilder를 통한 HikariCP 파라미터 최적화
  * 다른 커넥션 풀 최적화
* 항목 87: 2개의 커넥션 풀을 갖는 2개의 데이터 소스 구성 방법
  * 테스트 확인


## 11장. 감사
* 항목 88: 생성 및 수정 시간과 엔터티 사용자 추적 방법
  * 스프링 데이터 감사 기능 활용
  * 하이버네이트 지원 기능 활용
  * 테스트 확인
* 항목 89: 하이버네이트 Envers 감사 활성화 방법
  * 엔터티 감사
  * 스키마 생성
  * 엔터티 스냅숏 쿼리
  * ValidityAuditStrategy 감사 로깅 전략
* 항목 90: 영속성 콘텍스트를 확인하는 방법
* 항목 91: 테이블 메타데이터 추출 방법


## 12장. 스키마
* 항목 92: 스프링 부트에서 Flyway 설정 방법
  * 신속한 Flyway 설정(MySQL 및 PostgreSQL)
  * Flyway를 통한 데이터베이스 생성
  * @FlywayDataSource를 통한 Flyway 설정
  * Flyway와 다중 스키마
* 항목 93: schema-*.sql을 통한 두 데이터베이스 생성과 엔터티 매칭 방법


## 13장. 페이지네이션
* 항목 94: 오프셋 페이지네이션 성능 저하 발생 시기와 이유
  * 오프셋 및 키세트 인덱스 스캔
  * 오프셋 페이지네이션 장단점
  * 스프링 부트 오프셋 페이지네이션
* 항목 95: COUNT(*) OVER 및 Page〈entity/dto〉를 사용한 오프셋 페이지네이션 최적화 방법
  * COUNT(*) OVER() 윈도우 집계
* 항목 96: SELECT COUNT 서브쿼리 및 Page〈entity/dto〉를 사용한 오프셋 페이지네이션 최적화 방법
  * SELECT COUNT 서브쿼리
* 항목 97: JOIN FETCH 및 Pageable 사용 방법
* 항목 98: HHH000104 조치 방법
  * 관리되는 엔터티 가져오기
* 항목 99: Slice〈T〉 findAll() 구현 방법
  * 신속한 구현
  * Slice〈T〉 findAll(Pageable pageable) 구현
* 항목 100: 키세트 페이지네이션 구현 방법
* 항목 101: 키세트 페이지네이션에 다음 페이지 버튼 추가 방법
* 항목 102: ROW_NUMBER()을 통한 페이지네이션 구현 방법


## 14장. 쿼리
* 항목 103: 하이버네이트 HINT_PASS_DISTINCT_THROUGH를 통한 SELECT DISTINCT 최적화 방법
* 항목 104: JPA 콜백 설정 방법
  * @EntityListeners를 통한 분리된 리스너 클래스
* 항목 105: 스프링 데이터 쿼리 빌더를 통한 결과 세트 크기 제한과 카운트 및 삭제 파생 쿼리 사용 방법
  * 결과 세트 크기 제한
  * 카운트 및 삭제 파생 쿼리
* 항목 106: 포스트 커밋에서 시간 소요가 많은 작업을 피해야 하는 이유
* 항목 107: 중복된 save() 호출을 피하는 방법
* 항목 108: N+1 문제 방지 이유와 방법
  * 하이버네이트 @Fetch(FetchMode.JOIN)과 N+1
  * FetchMode.JOIN 대신 JOIN FETCH 사용
  * FetchMode.JOIN 대신 엔터티 그래프 사용
* 항목 109: 하이버네이트 기반 소프트 삭제 지원 사용 방법
  * 하이버네이트 소프트 삭제
  * 테스트 확인
  * 유용한 쿼리
  * 현재 영속성 콘텍스트에서 Deleted 속성 업데이트
* 항목 110: OSIV 안티패턴 회피 이유와 방법
  * Hibernate5Module
  * 로드되지 않은 속성에 대한 명시적(수동) 초기화
  * 하이버네이트의 hibernate.enable_lazy_load_no_trans에 대해
* 항목 111: UTC 시간대로 날짜/시간 저장 방법(MySQL)
* 항목 112: ORDER BY RAND()를 통해 작은 결과 세트를 뒤섞는 방법
* 항목 113: WHERE/HAVING 절에서 서브쿼리를 사용하는 방법
* 항목 114: 저장 프로시저 호출 방법
  * 값(스칼라 데이터 타입)을 반환하는 저장 프로시저 호출
  * 결과 세트를 반환하는 저장 프로시저 호출
  * 항목 115: 프록시를 언프록시하는 방법
  * 프록시 객체란?
  * 엔터티 객체와 프록시 객체는 동일하지 않음
  * 프록시에 대한 언프록시
  * 엔터티 객체와 언프록시 객체는 동일함
* 항목 116: 데이터베이스 뷰 매핑 방법
* 항목 117: 데이터베이스 뷰 수정 방법
  * UPDATE문 트리거
  * INSERT문 트리거
  * DELETE문 트리거
* 항목 118: WITH CHECK OPTION을 사용하는 이유와 방법
* 항목 119: 데이터베이스 임시 순위를 행에 효율적으로 할당하는 방법
  * 쿼리와 OVER 절에 ORDER BY 절 사용
  * OVER 절에 여러 칼럼 사용
* 항목 120: 모든 그룹의 상위 N개 행을 효율적으로 찾는 방법
* 항목 121: Specification API를 통한 고급 검색 구현 방법
  * 테스트 확인
  * 장르 Anthology의 40세 이상 저자 모두 가져오기
  * 가격이 60 미만인 도서에 대한 페이지 가져오기
  * 다음 단계
* 항목 122: IN 절 파라미터 패딩을 통한 SQL 캐싱 향상 방법
* 항목 123: Specification 쿼리 페치 조인 생성 방법
  * 메모리 기반 조인 페치 및 페이지네이션
  * 데이터베이스에서 조인 페치 및 페이지네이션
* 항목 124: 하이버네이트 쿼리 실행 계획 캐시 사용 방법
* 항목 125: 스프링 QBE(Query By Example)를 통한 비영속 엔터티의 데이터베이스 존재 여부 확인 방법
  * 모든 속성의 일대일 비교
  * 일부 속성의 일대일 비교
  * 하위 속성 집합에 대한 Or 결합 적용
* 항목 126: 하이버네이트 @DynamicUpdate를 통해 수정된 칼럼만 UPDATE문에 포함하는 방법
* 항목 127: 스프링에서 네임드 (네이티브) 쿼리를 사용하는 방법
  * 네임드 (네이티브) 쿼리 참조
  * @NamedQuery 및 @NamedNativeQuery 사용
  * 속성 파일(jpa-named-queries.properties) 사용
* 항목 128: 다른 쿼리/요청에서 부모와 자식을 가져오는 가장 좋은 방법
* 항목 129: 업데이트를 사용한 병합 작업 최적화 방법
* 항목 130: SKIP LOCKED 옵션을 통한 동시 테이블 기반 큐 구현 방법
  * SKIP LOCKED 설정
  * 테스트 확인
* 항목 131: 버전 기반(@Version) OptimisticLockException 발생 후 트랜잭션 재시도 방법
  * 버전 기반 낙관적 잠금 예외
  * 낙관적 잠금 예외 시뮬레이션
  * 트랜잭션 재시도
  * 테스트 시나리오
* 항목 132: 버전 없는 OptimisticLockException의 트랜잭션 재시도 방법
  * 버전 없는 낙관적 잠금 예외
  * 낙관적 잠금 예외 시뮬레이션
  * 트랜잭션 재시도
  * 테스트 시나리오
* 항목 133: 버전 기반 낙관적 잠금 및 분리된 엔터티를 처리하는 방법
* 항목 134: 장기 HTTP 통신에서의 낙관적 잠금 메커니즘 및 분리된 엔터티 사용 방법
  * 테스트 확인
* 항목 135: 엔터티가 수정되지 않은 경우에도 잠긴 엔터티 버전을 증가시키는 방법
  * OPTIMISTIC_FORCE_INCREMENT
  * PESSIMISTIC_FORCE_INCREMENT
* 항목 136: PESSIMISTIC_READ/WRITE 작동 방식
  * PESSIMISTIC_READ
  * PESSIMISTIC_WRITE
* 항목 137: PESSIMISTIC_WRITE가 UPDATE/INSERT 및 DELETE에서 작동하는 방식
  * UPDATE 트리거
  * DELETE 트리거
  * INSERT 트리거


## 15장. 상속
* 항목 138: 단일 테이블 상속을 효율적으로 사용하는 방법
  * 데이터 저장
  * 쿼리 및 단일 테이블 상속
  * 하위 클래스 속성 Non-Nullability 이슈
  * 구분자 칼럼의 메모리 사용량 최적화
* 항목139: SINGLE_TABLE 상속 계층 구조에서 특정 하위 클래스 가져오기
* 항목140: 조인 테이블 상속의 효율적 사용 방법
  * 데이터 저장
  * 쿼리 및 조인 테이블 상속
  * JPA JOINED 상속 전략 및 전략 디자인 패턴 사용 방법
* 항목 141: 클래스별 테이블 상속의 효율적 사용 방법
  * 데이터 저장
  * 쿼리 및 클래스별 테이블 상속
* 항목142: @MappedSuperclass 효율적 사용 방법
  * 데이터 저장


## 16장. 일반 타입과 하이버네이트 타입
* 항목 143: 하이버네이트 타입 라이브러리를 통한 하이버네이트 및 미지원 타입 처리 방법
* 항목 144: CLOB 및 BLOB 매핑 방법
  * 사용 용이성(성능에 대한 트레이드오프)
  * 성능 저하 방지(트레이드오프는 사용 용이성)
* 항목 145: 자바 열거형을 데이터베이스에 효율적으로 매핑하는 방법
  * EnumType.STRING을 통한 매핑
  * EnumType.ORDINAL을 통한 매핑
  * 열거형을 커스텀 표현 방식으로 매핑
  * 열거형을 데이터베이스 Enum 타입에 매핑(PostgreSQL)
* 항목 146: JSON 자바 객체를 MySQL JSON 칼럼에 효율적으로 매핑하는 방법
  * Author 저장
  * Author 가져오기/수정하기
  * JSON 쿼리를 통한 Author 가져오기
* 항목 147: JSON 자바 Object를 PostgreSQL JSON 칼럼에 효율적으로 매핑하는 방법
  * Author 저장
  * Author 가져오기/수정하기
  * JSON 쿼리를 통한 Author 가져오기


## 부록 A. (하이버네이트) JPA 기본 사항
* 영속성 유닛이란?
* EntityManagerFactory란?
* EntityManager란?
* 엔터티 상태 전이


## 부록 B. 연관관계 효율성


## 부록 C. 하루를 절약할 수 있는 5가지 SQL 성능 팁
* WHERE 절에서의 SQL 함수 사용
* 인덱스 칼럼 순서의 중요성
* 기본키와 고유키
* LIKE와 동등(=)
* UNION과 UNION ALL 및 JOIN 형태


## 부록 D. 유용한 데이터베이스 인덱스를 만드는 방법
* JPA 2.1 @Index
* 인덱스를 추측하지 말자
* 인덱싱을 위해 가장 많이 사용되는 SQL 쿼리 우선순위 지정
* 인덱스가 필요한 중요한 SQL 쿼리
* GROUP BY 및 ORDER BY 인덱싱을 통한 정렬 작업 방지
* 고유성을 위한 인덱스 사용
* 외래키에 대한 인덱스 사용
* 인덱스 전용 액세스를 위한 칼럼 추가
* 나쁜 표준을 피하자


## 부록 E. SQL Phenomena
* Dirty Writes
* Dirty Reads
* Non-Repeatable Reads
* Phantom Reads
* Read Skews
* Write Skews
* Lost Updates


## 부록 F. 스프링 트랜잭션 격리 수준
* @Transactional(isolation=Isolation.READ_UNCOMMITTED)
* @Transactional(isolation=Isolation.READ_COMMITTED)
* @Transactional(isolation=Isolation.REPEATABLE_READ)
* @Transactional(isolation=Isolation.SERIALIZABLE)


## 부록 G. 스프링 트랜잭션 전파
* Propagation.REQUIRED
* Propagation.REQUIRES_NEW
* Propagation.NESTED
* Propagation.MANDATORY
* Propagation.NEVER
* Propagation.NOT_SUPPORTED
* Propagation.SUPPORTS


## 부록 H. 플러싱 메커니즘
* 엄격한 플러시 작업 순서
* 데이터 질의어(DQL) 실행 전 플러시: SELECT 쿼리
* 트랜잭션 커밋 전 플러시
* 자동 플러시 모드
* 코드 이야기
* 글로벌 플러시 모드
* 서비스 수준 플러시 모드
* 쿼리 수준 플러시 모드


## 부록 I. 2차 캐시
* NONSTRICT_READ_WRITE
* READ_ONLY
* READ_WRITE
* TRANSACTIONAL
* 쿼리 캐시


## 부록 J. 도구

## 부록 K. 하이버네이트 6
