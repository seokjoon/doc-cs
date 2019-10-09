## 01장 검색 시스템 이해하기
* 1.1 검색 시스템의 이해
    * ES/RDB 비교: 인덱스/데이터베이스, 시드/파티션, 타입/테이블, 문서/행, 필드/열, 매핑/스키마, QueryDSL/SQL
* 1.2 검색 시스템과 엘라스틱서치
* 1.3 실습 환경 구축

## 02장 엘라스틱서치 살펴보기
* 2.1 엘라스틱서치를 구성하는 개념
    * 2.1.3 클러스터, 노드, 샤드
* 2.2 엘라스틱서치에서 제공하는 주요 API
    * 스키마리스 단점: 동적 매핑 사용하지 말고 명시적 매핑 설정 사용
    * 2.2.1 인덱스 관리 API: 매핑 변경 불가
        * put /foo { "mappings": { "_doc": { "bar": { "type": "text" } } } }
        * delete /foo
    * 2.2.2 문서 관리 API
        * single: index, get, delete, update
            * post /foo/_doc/1 { "bar": "test" }
                * post /foo/_doc { "bar": "test" }: _id 자동 지정: 관리 어려움으로 RDB pk와 맞춤이 유리
            * get /foo/_doc/1
            * delete /foo/_doc/1
        * multi: get, bulk, delete, update, reindex
    * 2.2.3 검색 API
        * 2개 방식: uri 파라미터를 uri에 추가, 혹은 restful/queryDSL/request body에 질의 포함 
        * 혼합: get /foo/_doc/_search?q=bar:test&pretty=true { "sort": { "bar": { "order": "asc" } } } 
        * uri 
            * 키 질의: get /foo/_doc/1?pretty=true 
            * 일치 질의 
                * time_out 설정 가능, 결과에 _score 포함 
                * 모든 필드: post /foo/_search?q=test 
                * 특정 필드: post /foo/_search?q=bar:test
        * request body 
            * post /foo/_search { "query": { "bar": "test" } } 
                * size: 기본값 10 
                * from: 기본값 0 
                * _source: 특정 필드만 반환 
                * sort: 특정 필드 기준 정렬: asc, desc 
                * query: 검색될 조건 정의 
                * filter: 결과 내 재검색
    * 2.2.4 집계 API
        * post /foo/_search?size=0 { "aggs": { "out": { "terms": { "field": "bar" } } } }
        * 중첩: post /foo/_search?size=0 { "aggs": { "out": { "terms": { "field": "bar" }, { "aggs": { "outSub": { "terms": { "field": "..." } } } } } } }
        * 타입 4가지: 조합 가능
            * 버킷: 문서 필드 기준
            * 매트릭: 문서 추출 값 Sum, Max, Min, Avg
            * 매트릭스: 행렬값 곱, 합
            * 파이프라인: 집계 결과를 다시 집계

## 03장 데이터 모델링
* 3.1 매핑 API 이해하기
    * 3.1.1 매핑 인덱스 만들기
        * put foo { "settings": { ... }, "mappings": { "_doc": { "properties": { "bar": "type": "text", "analyzer": "standard" } } } }
    * 3.1.2 매핑 확인
        * get foo/_mappings
    * 3.1.3 매핑 매개변수
        * analyzer: 형태소 분석, text 타입은 기본적으로 사용해야, 기본값 standard analyzer
        * normalizer: term query 분석, 예를 들어 keyword 타입, asciifolding 필터로 대소문자/언어별 차이 정규화 등
        * boost: 필터에 가중치 부여: 최신 버전에서 색인시 boost 설정 불가로 변경
        * coerce: 자동(타입)변환 허용여부
        * copy_to: 지정된 필드로 복사, 예를 들어 keyword 타입을 text 타입 필드로 복사해서 개별 처리
        * format: 날짜/시간 문자열 변경시 포맷 지정: basic_date, basic_date_time, ...
        * ignore_above: 문자열 지정 크기 초과하면 (해당 크기만큼이 아닌)빈 값으로 저장
        * ignore-malformed: 잘못된 데이터 타입 색인시 해당 필드만 무시하고 문서는 색인 가능하게
        * index: 필드값 색인 여부, 기본값 true
        * fields: multi_field 설정 옵션, 필드안에 또 다른 필드 정보 추가 가능
            * ... "foo": { "type": "text". "fields": { "bar": { "type": "keyword" } } }
        * norms: 문서 _score 값 계산에 필요한 정규화 인수 사용 여부, 기본값 true, 단순 필터 등 필요없을 경우 false
        * null_value: 색인시 문서값 null 이더라도 필드 생성
        * position_increment_gap: 배열 데이터 검색시 단어 사이 간격(slop) 허용
        * properties: object 혹은 nested 타입 스키마 정의시 사용
        * search_analyzer: 색인시 분석기와 다른 분석기를 검색시 사용
        * similaity: 유사도 측정 알고리즘 지정, 기본 BM25, classic(tf/idf), boolean
        * store: 필드 값 저장해서 검색 결과에 값 포함(디스크 더 사용)
        * term_vector: 루씬 분석 용어 정보 포함 여부: no, yes, ...
* 3.2 메타 필드
    * 3.2.1 _index 메타 필드: 해당 문서가 속한 인덱스 이름 정보
        * post foo/_search { "size": 0, "aggs": { "indices": { "terms": { "field": "_index", "size": 10 } } } }: 인덱스별 카운트 정보
    * 3.2.2 _type 메타 필드: 해당 문서가 속한 매핑의 타입 정보
    * 3.2.3 _id 메타 필드: 문서를 식별하는 유일한 키 값
        * post foo/_search { "size": 0, "aggs": { "indices": { "terms": { "field": "_id", "size": 10 } } } }: 키 값 대응 모든 문서 표시
    * 3.2.4 _uid 메타 필드: 특수 목적 식별키("#" 태그 사용해 _type 와 _id 값 조합)
    * 3.2.5 _source 메타 필드: 문서 원본 데이터 제공
    * 3.2.6 _all 메타 필드
    * 3.2.7 _routing 메타 필드: 특정 문서를 특정 샤드에 저장
* 3.3 필드 데이터 타입
    * 3.3.1 Keyword 데이터 타입: 분석기 거치지 않고 원문대로 색인, 필터링/정렬/집계 항목
    * 3.3.2 Text 데이터 타입: 분석기가 문자열 데이터로 인식/분석, 전문 검색 가능, 전체 텍스트 토큰화되어 특정 단어 검색 가능, 정렬/집계 필요시 text 타입과 keyword 타입의 멀티 필드로 설정
    * 3.3.3 Array 데이터 타입: 모두 같은 타입으로 구성, 객체 배열 가능: 매핑 설정시 Array 로 명시 정의하지 않음
    * 3.3.4 Numeric 데이터 타입: long, integer, ...
    * 3.3.5 Date 데이터 타입
    * 3.3.6 Range 데이터 타입: 숫자/IP 범위 
    * 3.3.7 Boolean 데이터 타입
    * 3.3.8 Geo-Point 데이터 타입
    * 3.3.9 IP 데이터 타입
    * 3.3.10 Object 데이터 타입
    * 3.3.11 Nested 데이터 타입
* 3.4 엘라스틱서치 분석기
    * 3.4.1 텍스트 분석 개요
    * 3.4.2 역색인 구조
    * 3.4.3 분석기의 구조
    * 3.4.4 전처리 필터
    * 3.4.5 토크나이저 필터
    * 3.4.6 토큰 필터
    * 3.4.7 동의어 사전
* 3.5 Document API 이해하기
    * 3.5.1 문서 매개변수
    * 3.5.2 Index API
    * 3.5.3 Get API
    * 3.5.4 Delete API
    * 3.5.5 Delete By Query API
    * 3.5.6 Update API
    * 3.5.7 Bulk API
    * 3.5.8 Reindex API

## 04장 데이터 검색
* 4.1 검색 API
    * 4.1.1 검색 질의 표현 방식
    * 4.1.2 URI 검색
    * 4.1.3 Request Body 검색
* 4.2 Query DSL 이해하기
    * 4.2.1 Query DSL 쿼리의 구조
    * 4.2.2 Query DSL 쿼리와 필터
    * 4.2.3 Query DSL의 주요 파라미터
* 4.3 Query DSL의 주요 쿼리
    * 4.3.1 Match All Query
    * 4.3.2 Match Query
    * 4.3.3 Multi Match Query
    * 4.3.4 Term Query
    * 4.3.5 Bool Query
    * 4.3.6 Query String
    * 4.3.7 Prefix Query
    * 4.3.8 Exists Query
    * 4.3.9 Wildcard Query
    * 4.3.10 Nested Query
* 4.4 부가적인 검색 API
    * 4.4.1 효율적인 검색을 위한 환경설정
    * 4.4.2 Search Shards API
    * 4.4.3 Multi Search API
    * 4.4.4 Count API
    * 4.4.5 Validate API
    * 4.4.6 Explain API
    * 4.4.7 Profile API

## 05장 데이터 집계
* 5.1 집계
    * 5.1.1 엘라스틱서치와 데이터 분석
    * 5.1.2 엘라스틱서치가 집계에 사용하는 기술
    * 5.1.3 실습 데이터 살펴보기
    * 5.1.4 Aggregation API 이해하기
* 5.2 메트릭 집계
    * 5.2.1 합산 집계
    * 5.2.2 평균 집계
    * 5.2.3 최솟값 집계
    * 5.2.4 최댓값 집계
    * 5.2.5 개수 집계
    * 5.2.6 통계 집계
    * 5.2.7 확장 통계 집계
    * 5.2.8 카디널리티 집계
    * 5.2.9 백분위 수 집계
    * 5.2.10 지형 경계 집계
    * 5.2.11 지형 중심 집계
* 5.3 버킷 집계
    * 5.3.1 범위 집계
    * 5.3.2 날짜 범위 집계
    * 5.3.3 히스토그램 집계
    * 5.3.4 날짜 히스토그램 집계
    * 5.3.5 텀즈 집계
* 5.4 파이프라인 집계
    * 5.4.1 형제 집계
    * 5.4.2 부모 집계
* 5.5 근삿값(Approximate)으로 제공되는 집계 연산
    * 5.5.1 집계 연산과 정확도
    * 5.5.2 분산 환경에서 집계 연산의 어려움

## 06장 고급 검색
* 6.1 한글 형태소 분석기 사용하기
    * 6.1.1 은전한닢 형태소 분석기
    * 6.1.2 Nori 형태소 분석기
    *     * 6.1.2.1 nori_tokenizer 토크나이저
    * 6.1.3 트위터 형태소 분석기
* 6.2 검색 결과 하이라이트하기
* 6.3 스크립트를 이용해 동적으로 필드 추가하기
* 6.4 검색 템플릿을 이용한 동적 쿼리 제공
* 6.5 별칭을 이용해 항상 최신 인덱스 유지하기
* 6.6 스냅숏을 이용한 백업과 복구

## 07장 한글 검색 확장 기능
* 7.1 Suggest API 소개
    * 7.1.1 Term Suggest API
    * 7.1.2 Completion Suggest API
* 7.2 맞춤법 검사기
    * 7.2.1 Term Suggester API를 이용한 오타 교정
    * 7.2.2 한영/영한 오타 교정
* 7.3 한글 키워드 자동완성
    * 7.3.1 Completion Suggest API를 이용한 한글 자동완성
    * 7.3.2 Suggest API를 이용한 한글 자동완성의 문제점
    * 7.3.3 직접 구현해보는 한글 자동완성
* 7.4 자바카페 플러그인
    * 7.4.1 한글 유니코드의 이해
    * 7.4.2 한글 자모 분석 필터(javacafe_jamo)
    * 7.4.3 한글 초성 분석 필터(javacafe_chosung)
    * 7.4.4 영한 오타 변환 필터(javacafe_eng2kor)
    * 7.4.5 한영 오타 변환 필터(javacafe_kor2eng)
    * 7.4.6 스펠링 체크 필터(javacafe_spell)

## 08장 엘라스틱서치 클라이언트
* 8.1 엘라스틱서치 클라이언트 이해하기
    * 8.1.1 클라이언트 모듈 소개
    * 8.1.2 자바 클라이언트 모듈
* 8.2 Transport 클라이언트
    * 8.2.1 Transport 클라이언트 연결
    * 8.2.2 매핑 API 사용하기
    * 8.2.3 문서 API 사용하기
    * 8.2.4 검색 API 사용하기
    * 8.2.5 집계 API 사용하기
    * 8.2.6 Query DSL API 사용하기
* 8.3 High Level REST 클라이언트
    * 8.3.1 REST 클라이언트 연결
    * 8.3.2 매핑 API 사용하기
    * 8.3.3 문서 API 사용하기
    * 8.3.4 검색 API 사용하기

## 09장 엘라스틱서치와 루씬 이야기
* 9.1 클러스터 관점에서 구성요소 살펴보기
    * 9.1.1 클러스터
    * 9.1.2 노드
    * 9.1.3 인덱스
    * 9.1.4 문서
    * 9.1.5 샤드
    * 9.1.6 레플리카
    * 9.1.7 세그먼트
* 9.2 엘라스틱서치 샤드 vs. 루씬 인덱스
* 9.3 엘라스틱서치가 근실시간 검색을 제공하는 이유
    * 9.3.1 색인 작업 시 세그먼트의 기본 동작 방식
    * 9.3.2 세그먼트 불변성
    * 9.3.3 세그먼트 불변성과 업데이트
    * 9.3.4 루씬을 위한 Flush, Commit, Merge
    * 9.3.5 엘라스틱서치를 위한 Refresh, Flush, Optimize API
    * 9.3.6 엘라스틱서치와 NRT(Near Real-Time)
* 9.4 고가용성을 위한 Translog의 비밀
    * 9.4.1 Translog의 동작 순서
    * 9.4.2 Translog가 존재하는 이유
* 9.5. 엘라스틱서치 샤드 최적화
    * 9.5.1 운영 중에 샤드의 개수를 수정하지 못하는 이유
    * 9.5.2 레플리카 샤드의 복제본 수는 얼마가 적당할까?
    * 9.5.3 클러스터에서 운영 가능한 최대 샤드 수는?
    * 9.5.4 하나의 인덱스에 생성 가능한 최대 문서 수는?

## 10장 대용량 처리를 위한 시스템 최적화
* 10.1 노드 실행환경과 JVM 옵션
    * 10.1.1 엘라스틱서치 릴리스 노트
    * 10.1.2 실행 시 자바 8 이상을 사용해야 하는 이유
    * 10.1.3 항상 최신 버전의 엘라스틱서치를 사용해야 하는 이유
    * 10.1.4 자바 8에서 제공하는 JVM 옵션
    * 10.1.5 엘라스틱서치에 적용된 JVM 옵션
* 10.2 힙 크기를 32GB 이하로 유지해야 하는 이유
    * 10.2.1 엘라스틱서치와 힙 크기
    * 10.2.2 Ordinary Object Pointer
    * 10.2.3 Compressed Ordinary Object Pointer
    * 10.2.4 엘라스틱서치에서 힙 크기 설정하기
    * 10.2.5 엘라스틱서치에서 Compressed OOP 사용하기
* 10.3 엘라스틱서치와 가상 메모리
    * 10.3.1 가상 메모리
    * 10.3.2 JVM을 위한 가상 메모리
    * 10.3.3 엘라스틱서치를 위한 vm.max_map_count 설정
* 10.4 분산환경에서의 메모리 스와핑
    * 10.4.1 메모리 스와핑
    * 10.4.2 엘라스틱서치에서 스와핑을 비활성화해야 하는 이유
* 10.5. 시스템 튜닝 포인트
    * 10.5.1 애플리케이션에서 튜닝 가능한 리소스
    * 10.5.2 ulimit 명령어를 이용한 유저 레벨의 튜닝
    * 10.5.3 sysctl 명령어를 이용한 커널 레벨의 튜닝
    * 10.5.4 엘라스틱서치 노드 레벨의 튜닝

## 11장 장애 방지를 위한 실시간 모니터링
* 11.1 클러스터 Health 체크
    * 11.1.1 클러스터 레벨의 Health 체크
    * 11.1.2 인덱스 레벨의 Health 체크
    * 11.1.3 샤드 레벨의 Health 체크
    * 11.1.4 Health 체크 활용하기
* 11.2 물리적인 클러스터 상태 정보 조회
    * 11.2.1 클러스터 레벨의 물리 상태 조회
    * 11.2.2 노드 레벨의 물리 상태 조회
* 11.3 클러스터에 대한 실시간 모니터링
    * 11.3.1 클러스터 레벨의 실시간 모니터링
    * 11.3.2 노드 레벨의 실시간 모니터링
    * 11.3.3 인덱스 레벨의 실시간 모니터링
* 11.4 Cat API로 콘솔에서 모니터링하기
    * 11.4.1 Cat API와 REST API 차이점
    * 11.4.2 Cat API 공통 파라미터
    *  11.4.3 콘솔에서 호출하는 Cat API

## 12장 안정적인 클러스터 운영 노하우
* 12.1 노드 부트스트랩 과정의 이해
    *  12.1.1 부트스트랩 과정이 필요한 이유
    *  12.1.2 부트스트랩 체크 과정 따라가기
* 12.2 마스터 노드와 데이터 노드 분리하기
    *  12.2.1 엘라스틱서치 노드의 종류
    *  12.2.2 마스터 노드와 데이터 노드를 분리해야 하는 이유
    *  12.2.3 클러스터 Split Brain 문제 방지하기
* 12.3 클러스터 관리 API
    *  12.3.1 런타임에 환경설정 변경(_cluster/settings API)
    *  12.3.2 대기 중인 클러스터 변경 명령 조회(_cluster/pending_tasks API)
    *  12.3.3 사용률이 높은 스레드 조회(_nodes/hot_threads API)
    *  12.3.4 노드 간 샤드 이동(_cluster/reroute API)
    *  12.3.5 실행 중인 태스크 조회(_tasks API)
    *  12.3.6 관리 API 호출 통계(_nodes/usage API)
* 12.4 안정적인 클러스터 운영을 위한 주요 체크포인트
    *  12.4.1 클러스터 상태 측정
    *  12.4.2 검색 성능 측정
    *  12.4.3 색인 성능 측정
    *  12.4.4 HTTP 성능 측정
    *  12.4.5 GC 성능 측정
    *  12.4.6 운영체제 성능 측정
    *  12.4.7 스레드풀 상태 측정
    *  12.4.8 캐시 상태 측정

## 13장 클러스터 성능 측정
* 13.1 엘라스틱서치를 위한 벤치마크 툴
    *  13.1.1 루씬 벤치마킹 유틸리티
    *  13.1.2 Elasticsearch Rally
* 13.2 랠리(Rally)를 이용한 클러스터 부하 테스트
    *  13.2.1 랠리 설치
    *  13.2.2 랠리 Tracks 옵션
    *  13.2.3 랠리 Cars 옵션
    *  13.2.4 레이스 시작하기
    *  13.2.5 토너먼트 결과 비교하기
* 13.3 키바나(Kibana)를 이용한 성능 모니터링
    *  13.3.1 Search Rate
    *  13.3.2 Search Latency
    *  13.3.3 Indexing Rate
    *  13.3.4 Indexing Latency