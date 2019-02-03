# 이 책에서 다루는 도구와 데이터

## 3. 시스템
* PostgreSQL, Apache Hive, Amazon Redshift, Google BigQuery, SparkSQL

## 4. 데이터
* 업무 데이터: 갱신형 데이터
	* 트랜잭션 데이터
	* 마스터 데이터
* 로그 데이터: 누적형 데이터
* 데이터 사용 가치: 목표 관리, 서비스 개선, 미래 예측


# 데이터 가공을 위한 SQL

## 5. 하나의 값 조작: 53p

## 6. 여러 개의 값에 대한 조작
* 두 값의 거리 계산하기: 78p: abs, power, sqrt, point 자료형, - 연산자
	* 유클리드 거리 계산하기: psql point 자료형 사용: ``` select sqrt(power(x1 - x2, 2) + power(y1 - y2, 2)) as dist from loc; ```

## 7. 하나의 테이블에 대한 조작

## 8. 여러 개의 테이블 조작: 119p
* 여러 개의 테이블을 세로로 결합: union all
* 여러 개의 테이블을 가로로 정렬: left join, 서브쿼리


# 매출을 파악하기 위한 데이터 추출

## 9. 시계열 기반으로 데이터 집계: 139p
* 날짜별 매출 집계: group by
* 이동평균 날짜별 추이: over(order by)
* 당월 매출 누계: over(partition by)
* 작대비, Z 차트

## 10. 다면적인 축을 사용해 데이터 집약: 162p
* 카테고리별 매출과 소계: union all, rollup
* abc 분석으로 잘 팔리는 상품 판별: sum, over: 구성비누계
* 팬 차트로 상품의 매출 증가율 확인: first_value
* 히스토그램으로 구매 가격대 집계: width_bucket: 도수분포표


# 사용자를 파악하기 위한 데이터 추출

## 11. 사용자 전체의 특징과 경향 찾기: 188p
* 사용자의 액션 수 집계: count, count(distinct), rollup: UU(Unique Users)
* 연령별 구분 집계: case, cast
* 연령별 구분의 특징 추출: join, group by
* 사용자의 방문 빈도 집계: sum
* 벤 다이어그램으로 사용자 액션 집계: sign, sum, case, cube
* Decile 분석을 사용해 사용자를 10단계 그룹으로 나누기: ntile
* RFM 분석으로 사용자를 3가지 관점의 그룹으로 나누기: case, generate_series

## 12. 시계열에 따른 사용자 전체의 상태 변화 찾기: 235p
* 등록 수의 추이와 경향: count(distinct)
* 지속률과 정착률 산출: count(distinct)
* 지속과 정착에 영향을 주는 액션 집계: cross join, case, avg
* 액션 수에 따른 정착률 집계: cross join, case, avg
* 사용 일수에 따른 정착률 집계: count, sum, avg
* 사용자의 잔존율 집계: cross join, sum(case), avg(case)
* 방문 빈도를 기반으로 사용자 속성을 정의하고 집계: case, nullif, lag: MAU, 리피트, 컴백
* 방문 종류를 기반으로 성장지수 집계하기: cast, lag, sum(case)

## 13. 시계열에 따른 사용자의 개별적인 행동 분석: 304p
* 사용자의 액션 간격 집계: 날짜, lag: 리드 타임
* 카트 추가 후에 구매 파악: case, sum, avg: 카트 탈락률
* 등록으로부터의 매출을 날짜별 집계: cross join, case, avg: ARPU, ARPPU, LTV


# 웹사이트에서의 행동을 파악하는 데이터 추출

## 14. 사이트 전체의 특징/경향 찾기: 326p
* 날짜별 방문자 수/방문 횟수/페이지뷰 집계: count, count(distinct)
* 유입원별로 방문 횟수 또는 CVR 집계: 정규표현식, url
* 접근 요일, 시간대 파악하기

## 15. 사이트 내의 사용자 행동 파악: 345p
* 입구 페이지와 출구 페이지 파악하기: first_value, last_value
* 이탈률과 직귀율 계산: row_number, count, avg(case end)
* 성과로 이어지는 페이지 파악: sign, sum: CVR
* 페이지 가치 산출: row_number
* 검색 조건들의 사용자 행동 가시화: sign, sum(case end), avg(case end), lag: CTR, CVR
* 폴아웃 리포트를 사용해 사용자 회유를 가시화: lag, first_value
* 사이트 내부에서 사용자 흐름 파악: lag, lead, sum
* 페이지 완독률 집계: sum(case end)

## 16. 입력 양식 최적화: 395p
* 오류율 집계: sum(case), avg(case)
* 입력-확인-완료까지의 이동률 집계: lag, min, count, first_value: 확정률, 이탈률
* 입력 양식 직귀율 집계: sum(case), sign


# 데이터 활용의 정밀도를 높이는 분석 기술

## 17. 데이터를 조합해서 새로운 데이터 만들기
* ip 주소로 국가/지역 보완, 주말/공휴일 판단, 하루 집계 범위 변경

## 18. 이상값 검출하기: 421p
* 데이터 분산 계산: percent_rank
* 크롤러 제외: like
* 데이터 타당성 확인, 특정 ip 제외

## 19. 데이터 중복 검출하기: 440p
* 마스터 데이터 중복 검출, 로그 중복 검출

## 20. 여러 개의 데이터셋 비교: 453p
* 데이터의 차이 추출: left outer join, right outer join, full outer join, is distinct from
* 두 순위의 유사도 계산: rank, sum, count: 스피어만 상관 계수


# 데이터를 무기로 삼기 위한 분석 기술

## 21. 검색 기능 평가: 467p
* NoMatch 비율과 키워드 집계: sum(case), avg(case)
* 재검색 비율과 키워드 집계: lead, sum(case), avg(case)
* 재검색 키워드 분류해서 집계: like
* 검색 이탈 비율과 키워드 집계: sum(case), avg(case)
* 검색 결과의 포괄성 지표화: full outer join, sum: 재현율
* 검색 결과의 타당성 지표화: full outer join, sum: 정확률
* 검색 결과 순위와 관련된 지표 계산: avg: MAP
	* 검색 평가에 사용되는 대표적인 순위 지표: 표 21-1

## 22. 데이터 마이닝: 505p
* 어소시에이션 분석: count: 지지도, 확신도, 리프트

## 23. 추천: 514p
* 추천 시스템의 종류, 모듈의 종류, 추천의 효과, 정밀도와 효과의 차이
* 특정 아이템에 흥미가 있는 사람이 함께 찾아보는 아이템 검색: sum(case), row_number: 벡터 내적, L2 정규화, 코사인 유사도
* 당신을 위한 추천 상품: sum(case), row_number: 벡터 내적, L2 정규화, 코사인 유사도
	* 추천 시스템의 대표적인 평가 지표 목록: 표 23-6

## 24. 점수 계산하기: 538p
* 여러 값을 균형있게 조합해서 점수 계산: sum(case), row_number: 산술 평균, 기하 평균, 조화 평균, 가중 평균
* 값의 범위가 다른 지표를 정규화해서 비교 가능한 상태 만들기: min, max: min-max 정규화, 시그모이드
* 각 데이터의 편차값 계산: stddev_pop: 표준편차, 정규값, 편차값
* 거대 숫자 지표를 직감적으로 이해하기 쉽게 가공: log
* 독자적인 점수 계산 방법을 정의해서 순위 작성: 가중 평균


# 지식을 행동으로

## 25. 데이터 활용의 현장: 570p
* 빅데이터 활용 단계: 그림 25-2
* 빅데이터 팀의 역할, 등장 인물, 제공중인 내용: 그림 25-3
* 로그 형식: 표 25-1
* 데이터 활용 쉽게 상태 조정: 3계층: 로그, 집약, 집계
* 데이터 분석 과정: 4가지: 서비스 이해, 그래프 작성, 여러 수치 비교, 가설 및 검증
* 분석: KG(Goal)I, KPI: 둘 다 계측 가능한 지표 설정