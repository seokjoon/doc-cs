##
- 154p: server sent events: 서버의 푸시
- 244p: 인증 캐시 프로바이더
- 265p: jwt
- 299p: 이벤트, 큐, 수퍼바이저
- 325p: CQRS(커맨드 쿼리 책임 분리)
- 349p: 커맨드
- 375p: 배치처리
- 399p: 테스트



# I | 라라벨 기초 1
## 2 | 라라벨 아키텍처 57
* 2-1 라이프 사이클 59
* 2-1-1 라라벨 애플리케이션 실행 흐름 59
* 2-1-2 엔트리 포인트 60
* 2-1-3 HTTP 커널 62
* 2-1-4 라우터 63
* 2-1-5 미들웨어 64
* 2-1-6 컨트롤러 65
* 2-2 서비스 컨테이너 67
* 2-2-1 서비스 컨테이너란? 67
* 2-2-2 바인드와 리졸브 68
* 2-2-3 바인드 69
* 2-2-4 리졸브 75
* 2-2-5 DI와 서비스 컨테이너 77
* 2-2-6 퍼사드 82
* 2-3 서비스 프로바이더 86
* 2-3-1 서비스 프로바이더 동작 기본 87
* 2-3-2 DeferrableProvider 인터페이스 지연 실행 89
* 2-4 컨트랙트 91
* 2-4-1 컨트랙트 기본 91
* 2-4-2 컨트랙트를 이용한 기능 대체 93

## 3 | 애플리케이션 아키텍처 99
* 3-1 MVC와 ADR 101
* 3-1-1 MVC 101
* 3-1-2 ADR 108
* 3-2 아키텍처 다루기 116
* 3-2-1 프레임워크와 아키텍처 설계 116
* 3-2-2 아키텍처 설계의 포인트 117
* 3-2-3 레이어드 아키텍처 118
* 3-2-4 레이어드 아키텍처 이후의 세계 123

# II | 실천패턴 125
## 4 | HTTP 요청과 응답 125
* 4-1 요청 핸들링 127
* 4-1-1 요청 취득 127
* 4-1-2 Request 퍼사드 128
* 4-1-3 Request 객체 130
* 4-1-4 폼 요청 131
* 4-2 밸리데이션 135
* 4-2-1 밸리데이션 규칙 지정 방법 136
* 4-2-2 밸리데이션 규칙 137
* 4-2-3 밸리데이션 이용 140
* 4-2-4 밸리데이션 실패 처리 143
* 4-2-5 규칙 커스터마이즈 146
* 4-3 응답 149
* 4-3-1 다양한 응답 149
* 4-3-2 리소스 클래스를 조합한 REST API 응답 패턴 155
* 4-4 미들웨어 165
* 4-4-1 미들웨어 기본 165
* 4-4-2 기본 제공 미들웨어 166
* 4-4-3 커스텀 미들웨어 구현 169

## 5 | 데이터베이스 173
* 5-1 마이그레이션 175
* 5-1-1 마이그레이션 처리 흐름 175
* 5-1-2 마이그레이션 파일 작성 176
* 5-1-3 정의 기술 178
* 5-1-4 마이그레이션 실행과 롤백 183
* 5-2 시더 186
* 5-2-1 시더 작성 186
* 5-2-2 시더 클래스 이용 설정 187
* 5-2-3 시딩 실행 188
* 5-2-4 Faker 이용 188
* 5-2-5 Factory 이용 예 190
* 5-3 Eloquent 193
* 5-3-1 클래스 작성 193
* 5-3-2 규약과 속성 194
* 5-3-3 데이터 검색 및 업데이트 기본 197
* 5-3-4 데이터 조작 응용 200
* 5-3-5 연관성이 있는 테이블 그룹의 값을 일괄 조작한다(릴레이션) 205
* 5-3-6 실행된 SQL 확인 207
* 5-4 쿼리 빌더 210
* 5-4-1 쿼리 빌더 형식 211
* 5-4-2 쿼리 빌더 얻기 211
* 5-4-3 처리 대상 및 내용의 특징 213
* 5-4-4 쿼리 실행 215
* 5-4-5 트랜잭션과 테이블 락 217
* 5-4-6 데이터 조작 기본 218
* 5-5 리포지터리 패턴 220
* 5-5-1 리포지터리 패턴 개요 220
* 5-5-2 리포지터리 패턴 구현 221
* 5-5-3 리팩터링 224

## 6 | 인증과 인가 231
* 6-1 세션 기반 인증 233
* 6-1-1 인증 지원 클래스 및 그 기능 233
* 6-1-2 인증 처리 이해 234
* 6-1-3 데이터베이스/세션을 이용한 인증 처리 237
* 6-1-4 폼 인증 적용 242
* 6-1-5 인증 처리 커스터마이즈 244
* 6-1-6 비밀번호 초기화 249
* 6-2 토큰 인증 252
* 6-2-1 api_token 저장용 테이블 작성 253
* 6-2-2 시더를 이용한 레코드 작성 255
* 6-2-3 커스텀 인증 프로바이더 작성 257
* 6-2-4 토큰 인증 이용 방법 263
* 6-3 JWT 인증 265
* 6-3-1 tymon/jwt-auth 설치 265
* 6-3-2 tymon/jwt-auth 이용 준비 266
* 6-3-3 tymon/jwt-auth 이용 267
* 6-3-4 토큰 발행 268
* 6-4 OAuth 클라이언트를 이용한 인증 및 인가 272
* 6-4-1 Socialite 272
* 6-4-2 깃허브 OAuth 인증 273
* 6-4-3 동작 확장 276
* 6-4-4 OAuth 드라이버 추가 278
* 6-5 인가 처리 283
* 6-5-1 인가 처리 이해 283
* 6-5-2 인가 처리 283
* 6-5-3 Blade 템플릿을 이용한 인가 처리 293

## 7 | 이벤트와 큐를 이용한 처리 분산 297
* 7-1 이벤트 299
* 7-1-1 이벤트 기본 299
* 7-1-2 이벤트 작성 300
* 7-1-3 이벤트를 이용한 견고한 옵저버 패턴 303
* 7-1-4 이벤트 취소 306
* 7-1-5 비동기 이벤트를 이용한 분리 패턴 307
* 7-2 큐 310
* 7-2-1 큐 기본 310
* 7-2-2 비동기 실행 드라이버 준비(Queue 드라이버) 311
* 7-2-3 큐 사양 312
* 7-2-4 큐를 이용한 PDF 파일 출력 패턴 312
* 7-2-5 Supervisor를 이용한 상주 프로그램 패턴 317
* 7-2-6 손쉬운 분산 처리 패턴 321
* 7-3 이벤트와 큐를 이용한 CQRS 325
* 7-3-1 CQRS(커맨드 쿼리 책임 분리) 325
* 7-3-2 애플리케이션 사양 326
* 7-3-3 애플리케이션 구현 준비 329
* 7-3-4 리뷰 등록 기능 구현 334
* 7-3-5 리뷰 작성 컨트롤러 구현 337
* 7-3-6 리스너 클래스를 이용한 엘라스틱서치 조작 339
* 7-3-7 Command 실행과 Query 구현 343

## 8 | 콘솔 애플리케이션 347
* 8-1 Command 기초 349
* 8-1-1 클로저를 이용한 Command 작성 349
* 8-1-2 클래스를 이용한 Command 작성 350
* 8-1-3 Command로의 입력 353
* 8-1-4 Command에서의 출력 356
* 8-1-5 Command 실행 358
* 8-2 Command 구현 361
* 8-2-1 샘플 구현 사양 361
* 8-2-2 Command 생성 363
* 8-2-3 유스케이스 클래스와 서비스 클래스 분리 364
* 8-2-4 유스케이스 클래스 모형 작성 366
* 8-2-5 서비스 클래스 구현 367
* 8-2-6 유스케이스 클래스 구현 369
* 8-2-7 Command 클래스 마무리 371
* 8-3 배치 처리 구현 375
* 8-3-1 배치 처리 사양 375
* 8-3-2 Command 클래스 구현 377
* 8-3-3 유스케이스 클래스 구현 378
* 8-3-4 Command 클래스 사양 381
* 8-3-5 배치 처리 로그 출력 385
* 8-3-6 스케줄 태스크를 이용한 배치 처리 실행 390

## 9 | 테스트 397
* 9-1 단위 테스트 399
* 9-1-1 테스트 대상 클래스 399
* 9-1-2 테스트 클래스 생성 401
* 9-1-3 테스트 메서드 구현 404
* 9-1-4 데이터 프로바이더 활용 407
* 9-1-5 예외 테스트 410
* 9-1-6 테스트 전처리 및 후처리 412
* 9-1-7 테스트 설정 414
* 9-2 데이터베이스 테스트 417
* 9-2-1 테스트 대상 테이블과 클래스 417
* 9-2-2 데이터베이스 테스트 기초 424
* 9-2-3 Eloquent 클래스 테스트 430
* 9-2-4 서비스 클래스 테스트 433
* 9-2-5 목을 이용한 테스트(서비스 클래스) 435
* 9-3 WebAPI 테스트 438
* 9-3-1 WebAPI 테스트 기능 438
* 9-3-2 테스트 대상 API 443
* 9-3-3 API 테스트 구현 450
* 9-3-4 WebAPI 테스트의 편리한 기능 456

## 10 | 에러 핸들링과 로그 활용 463
* 10-1 에러 핸들링 465
* 10-1-1 에러 표시 465
* 10-1-2 에러 종류 465
* 10-1-3 에러 핸들링 기초 466
* 10-1-4 Fluentd 활용 467
* 10-1-5 예외 메시지 표시 템플릿 변경 469
* 10-1-6 에러 핸들링 패턴 471
* 10-2 로그 활용 패턴 475
* 10-2-1 로그 기본 475
* 10-2-2 로그 출력 설정 476
* 10-2-3 엘라스틱서치를 이용한 커스텀 로그 드라이버 구현 479

# III | 애플리케이션 개발 485
## 11 | 테스트 주도 개발 실천 485
* 11-1 테스트 주도 개발이란? 487
* 11-1-1 가능한 작게 구현 487
* 11-1-2 샘플 애플리케이션 사양 488
* 11-1-3 데이터베이스 사양 489
* 11-1-4 API 엔드포인트 491
* 11-2 API 엔드포인트 작성 493
* 11-2-1 애플리케이션 작성 및 사전 준비 493
* 11-2-2 첫 번째 테스트 493
* 11-2-3 테스트 메서드 작성 내용 495
* 11-2-4 최소한의 구현 498
* 11-2-5 두 번째 이후의 테스트 498
* 11-2-6 하나의 테스트 메서드에서는 한 가지만 검증 500
* 11-2-7 테스트 코드 확인 501
* 11-3 테스트용 데이터베이스 설정 505
* 11-3-1 데이터베이스 설정 505
* 11-3-2 마이그레이션/모델/팩토리 508
* 11-3-3 초기 데이터 입력용 시더 준비 515
* 11-4 데이터베이스 테스트 517
* 11-4-1 테스트용 트레이트 이용 및 초기 데이터 입력 517
* 11-4-2 데이터베이스 관련 테스트 518
* 11-4-3 임시 구현을 통한 빠른 테스트 520
* 11-4-4 첫 번째 리팩터링 521
* 11-4-5 반환값 내용 검증 521
* 11-4-6 성공하는 테스트 추가 524
* 11-4-7 데이터 추가 검증 525
* 11-4-8 의존 테스트 수정 527
* 11-4-9 밸리데이션 테스트 528
* 11-5 리팩터링 유스케이스 531
* 11-5-1 컨트롤러 사용 531
* 11-5-2 프레임워크 표준에 맞는 리팩터링 ① 534
* 11-5-3 정확한 테스트를 쓸 수 없을 때의 대처 방법 535
* 11-5-4 프레임워크 표준에 맞는 리팩터링 ② 538
* 11-5-5 서비스 클래스 분리 540
