## 머릿말
* 기존 TF/IDF, BM25: 희소 벡터(sparse vector) 사용, 문장의 단어(키워드) 인코딩
	* 검색 증강 생성 RAG(Retrieval Augmented Generation) 는 임베딩 활용으로 벡터 DB로 지식 기반 구축, 질문에 대한 응답을 LLM 이 요약
		* RAG 의 의미(semantic) 검색은 고밀도 벡터(dense vector) 사용, 단어의 추상적 의미/관계를 인코딩


#	[1부] LLM의 기초 뼈대 세우기

## 1장 LLM 지도
* 1.1 딥러닝과 언어 모델링
		* LLM: Large Language Model
			* (딥러닝)과 (자연어처리의 부분집합인 (자연어생성))의 (교집합의 (부분집합))
			* 언어 모델: 다음에 올 단어가 무엇일지 예측
		* word2vec(2013), transformer architecture(2017), GTP-1(2018)
  * 1.1.1 데이터의 특징을 스스로 추출하는 딥러닝
  	* 머신러닝은 데이터의 feature 를 사람이 찾고 모델에 입력, 딥러닝은 모델이 데이터의 특징을 찾고 분류
  * 1.1.2 임베딩: 딥러닝 모델이 데이터를 표현하는 방식
  * 1.1.3 언어 모델링: 딥러닝 모델의 언어 학습법
  	* 전이 학습, 사전 학습, 미세 조정, 다운스트림
* 1.2 언어 모델이 챗GPT가 되기까지
  * 1.2.1 RNN에서 트랜스포머 아키텍처로
  	* attention: RNN 과 달리 맥락 데이터를 모두 활용
  * 1.2.2 GPT 시리즈로 보는 모델 크기와 성능의 관계
  * 1.2.3 챗GPT의 등장
  	* 지도 미세 조정(supervised fine-tuning), 사람의 피드백을 활용한 강화 학습(RLHF: Reinforcement Learning fro Human Feedback)
  	* 선호 데이터셋(preference dataset), 리워드 모델(reward model)
* 1.3 LLM 애플리케이션의 시대가 열리다
		* sLLM(small Large Language Model), 학습/추론, 검색 증강 생성(RAG: Retrieval Augmented Generation)
  * 1.3.1 지식 사용법을 획기적으로 바꾼 LLM
  * 1.3.2 sLLM: 더 작고 효율적인 모델 만들기
  * 1.3.3 더 효율적인 학습과 추론을 위한 기술
  * 1.3.4 LLM의 환각 현상을 대처하는 검색 증강 생성(RAG) 기술
* 1.4 LLM의 미래: 인식과 행동의 확장
	* 멀티 모달, 에이전트, 새 아키텍처
* 1.5 정리


## 2장 LLM의 중추, 트랜스포머 아키텍처 살펴보기
* 2.1 트랜스포머 아키텍처란
	* 기존 RNN: 토큰별로 이전 출력이 다음 입력, 병렬이 아닌 순차적
		* 지연, 성능 저하, 그레이디언트 소실(gradient vanishing), 그레이디언트 증폭(gradient exploding)
		* self-attension: 입력 문장 내 각 단어가 서로 어떤 관련 있는지 계산해서 각 단어의 표현(representation) 조정
		* embedding, 위치 인코딩(positional encoding), 층 정규화(layer normalization), 멀티 헤드 어텐션(multi-head attention), 피드 포워드(feed forward)
* 2.2 텍스트를 임베딩으로 변환하기
  * 2.2.1 토큰화
  	* 텍스트를 적절 단위로 나누고 숫자 아이디 부여
  	* 사전(vocabulary)
  * 2.2.2 토큰 임베딩으로 변환하기
  	* 임베딩: 데이터를 의미를 담아 숫자 집합(벡터)로 변환
  * 2.2.3 위치 인코딩
  	* 트랜스포머는 순차적(RNN)이 아닌 동시 입력(순서 정보 사라짐)이기 때문에 위치 인코딩(텍스트 순서)이 필요
  	* 절대적 위치 인코딩(absolute position encoding), 상대적 위치 인코딩(relative position encoding)
* 2.3 어텐션 이해하기
  * 2.3.1 사람이 글을 읽는 방법과 어텐션
  * 2.3.2 쿼리, 키, 값 이해하기
  	* 쿼리(검색어), 키(딕셔너리의 단어), 값(벡터)
  	* 가중치
  * 2.3.3 코드로 보는 어텐션
  * 2.3.4 멀티 헤드 어텐션
* 2.4 정규화와 피드 포워드 층
  * 2.4.1 층 정규화 이해하기
  * 2.4.2 피드 포워드 층
* 2.5 인코더
* 2.6 디코더
* 2.7 BERT, GPT, T5 등 트랜스포머를 활용한 아키텍처
  * 2.7.1 인코더를 활용한 BERT(Bidirectional Encoder Representations from Transformers): 구글: 양방향
  * 2.7.2 디코더를 활용한 GPT(Generative Pre-trained Transformers)
  * 2.7.3 인코더와 디코더를 모두 사용하는 BART(Bidirectional and Auto-Regressive Transformers), T5(Text-to-Text Transfer Transformers)
* 2.8 주요 사전 학습 메커니즘
  * 2.8.1 인과적 언어 모델링(Causal Language Modeling, CLM)
  * 2.8.2 마스크 언어 모델링
* 2.9 정리


## 3장 트랜스포머 모델을 다루기 위한 허깅페이스 트랜스포머 라이브러리
* 3.1 허깅페이스 트랜스포머란
* 3.2 허깅페이스 허브 탐색하기
  * 3.2.1 모델 허브
  * 3.2.2 데이터셋 허브
  * 3.2.3 모델 데모를 공개하고 사용할 수 있는 스페이스
* 3.3 허깅페이스 라이브러리 사용법 익히기
  * 3.3.1 모델 활용하기
  * 3.3.2 토크나이저 활용하기
  * 3.3.3 데이터셋 활용하기
* 3.4 모델 학습시키기
  * 3.4.1 데이터 준비
  * 3.4.2 트레이너 API를 사용해 학습하기
  * 3.4.3 트레이너 API를 사용하지 않고 학습하기
  * 3.4.4 학습한 모델 업로드하기
* 3.5 모델 추론하기
  * 3.5.1 파이프라인을 활용한 추론
  * 3.5.2 직접 추론하기
* 3.6 정리


## 4장 말 잘 듣는 모델 만들기
	* 지시 데이터 셋(instruction dataset), 사용자의 선호(preference) 학습
	* 지도 미세 조정(supervised fine-tuning), RLHF(Reinforcement Learning from Human Feedback), PPO
	* 기각 샘플링(rejective sampling)
* 4.1 코딩 테스트 통과하기: 사전 학습과 지도 미세 조정
  * 4.1.1 코딩 개념 익히기: LLM의 사전 학습
  * 4.1.2 연습문제 풀어보기: 지도 미세 조정
  	* 텍스트
	  	* 지시사항(instruction): 사용자의 요구사항을 표현한 문장
  		* 입력: 답변에 필요한 데이터
  		* 출력: 지시사항과 입력에 기반한 답변
  * 4.1.3 좋은 지시 데이터셋이 갖춰야 할 조건
* 4.2 채점 모델로 코드 가독성 높이기
  * 4.2.1 선호 데이터셋을 사용한 채점 모델 만들기
  * 4.2.2 강화 학습: 높은 코드 가독성 점수를 향해
  	* 사람의 피드백을 활용한 강화 학습(Reinforcement Learning from Human Feedback, RLHF)
  	* 강화 학습: 에이전트/환경/행동, 상태/보상, 에피소드
  * 4.2.3 PPO: 보상 해킹 피하기
  	* reward hacking: 보상을 높게 받는 데에만 집중
  	* 근접 정책 최적화(Proximal Preference Optimization)
  * 4.2.4 RLHF: 멋지지만 피할 수 있다면…
* 4.3 강화 학습이 꼭 필요할까?
  * 4.3.1 기각 샘플링: 단순히 가장 점수가 높은 데이터를 사용한다면?
  	* rejection sampling
  * 4.3.2 DPO: 선호 데이터셋을 직접 학습하기
  	* 직접 선호 최적화(Direct Preference Optimization)
  * 4.3.3 DPO를 사용해 학습한 모델들
* 4.4 정리



# [2부 LLM 길들이기]

## 5장 GPU 효율적인 학습
* 5.1 GPU에 올라가는 데이터 살펴보기
  * 5.1.1 딥러닝 모델의 데이터 타입
  	* 과거 32비트 부동소수점(fp32), 최근 16비트(bf16: brain float 16)
  	* 딥러닝 용량: 파라미터 수에 파라미터당 비트(혹은 바이트) 수 곱하기
  		* 파라미터 10억개 모델이 fp16으로 저장되면 20억 바이트: 2GB
  		* 파라미터 70억개 7B 모델이 16비트(2바이트)로 저장되면 모델은 14GB
  * 5.1.2 양자화로 모델 용량 줄이기
  * 5.1.3 GPU 메모리 분해하기
  	* 저장되는 데이터: 모델 파라미터, 그레이디언트(gradient), 옵티마이저 상태(optimizer state), 순전파 상태(forward activation)
  	* 딥러닝 학습 과정 간단 요약: 순전파 => 계산한 손실로부터 역전파 => 옵티마이저를 통해 모델 업데이트
  		* 순전파 상태 값: 순전파의 결과, 역전파 수행을 위해 저장
  		* 그레이디언트: 역전파 결과 생상
* 5.2 단일 GPU 효율적으로 활용하기
  * 5.2.1 그레이디언트 누적(gradient accumulation)
  * 5.2.2 그레이디언트 체크포인팅(gradient checkpointing):
* 5.3 분산 학습과 ZeRO
  * 5.3.1 분산 학습
  * 5.3.2 데이터 병렬화에서 중복 저장 줄이기(ZeRO: Deepspeed Zero)
* 5.4 효율적인 학습 방법(PEFT): LoRA
  * 5.4.1 모델 파라미터의 일부만 재구성해 학습하는 LoRA(Low Rank Adaption)
  * 5.4.2 LoRA 설정 살펴보기
  * 5.4.3 코드로 LoRA 학습 사용하기
* 5.5 효율적인 학습 방법(PEFT): QLoRA(Quantized LoRA)
  * 5.5.1 4비트 양자화와 2차 양자화
  * 5.5.2 페이지 옵티마이저
  * 5.5.3 코드로 QLoRA 모델 활용하기
* 5.6 정리


## 6장 sLLM 학습하기
	* 비용 효율적, 즉정 작업/도메인 특화
* 6.1 Text2SQL 데이터셋
  * 6.1.1 대표적인 Text2SQL 데이터셋
  * 6.1.2 한국어 데이터셋
  * 6.1.3 합성 데이터 활용
* 6.2 성능 평가 파이프라인 준비하기
  * 6.2.1 Text2SQL 평가 방식
  * 6.2.2 평가 데이터셋 구축
  * 6.2.3 SQL 생성 프롬프트
  * 6.2.4 GPT-4 평가 프롬프트와 코드 준비
* 6.3 실습: 미세 조정 수행하기
  * 6.3.1 기초 모델 평가하기
  * 6.3.2 미세 조정 수행
  * 6.3.3 학습 데이터 정제와 미세 조정
  * 6.3.4 기초 모델 변경
  * 6.3.5 모델 성능 비교
* 6.4 정리


## 7장 모델 가볍게 만들기
* 7.1 언어 모델 추론 이해하기
  * 7.1.1 언어 모델이 언어를 생성하는 방법
  * 7.1.2 중복 연산을 줄이는 KV 캐시: KV cache
  * 7.1.3 GPU 구조와 최적의 배치 크기
  * 7.1.4 KV 캐시 메모리 줄이기: multi-query attention, grouped-query attention
* 7.2 양자화로 모델 용량 줄이기
		* 학습 후 양자화(Post-Training Quantization, PTQ): BitsAndBytes, GPTO, AWQ
		* 학습 전 양자화(Quantization-Aware Training, QAT)
  * 7.2.1 비츠앤바이츠: BitsAndBytes
  * 7.2.2 GPTQ: GPT Quantization
  * 7.2.3 AWQ: Activation-aware Weight Quantization
* 7.3 지식 증류 활용하기: knowledge distillation: teacher model, student model
	* 더 크고 성능이 높은 선생 모델의 생성 결과를 활용해 더 작고 성능이 낮은 학생 모델을 만드는 방법
		* 학생 모델이 선생 모델의 생성 결과를 모방
		* 선생 모델에 쌓은 지식을 더 작은 모델로 압축해 전달
* 7.4 정리


## 8장 sLLM 서빙하기
* 8.1 효율적인 배치 전략
  * 8.1.1 일반 배치(정적 배치)
  * 8.1.2 동적 배치
  * 8.1.3 연속 배치
* 8.2 효율적인 트랜스포머 연산
  * 8.2.1 플래시어텐션: FlashAttention
  * 8.2.2 플래시어텐션 2
  * 8.2.3 상대적 위치 인코딩
* 8.3 효율적인 추론 전략
  * 8.3.1 커널 퓨전
  * 8.3.2 페이지어텐션: PagedAttention
  * 8.3.3 추측 디코딩
* 8.4 실습: LLM 서빙 프레임워크
  * 8.4.1 오프라인 서빙
  * 8.4.2 온라인 서빙
* 8.5 정리



# [3부] LLM을 활용한 실전 애플리케이션 개발
* 9장 LLM 애플리케이션 개발하기
* 9.1 검색 증강 생성(RAG): Retrieval Augmented Generation: 환각(hallucination) 감소
  * 9.1.1 데이터 저장
  * 9.1.2 프롬프트에 검색 결과 통합
  * 9.1.3 실습: 라마인덱스로 RAG 구현하기
* 9.2 LLM 캐시
  * 9.2.1 LLM 캐시 작동 원리
  * 9.2.2 실습: OpenAI API 캐시 구현
* 9.3 데이터 검증
  * 9.3.1 데이터 검증 방식
  * 9.3.2 데이터 검증 실습
* 9.4 데이터 로깅
  * 9.4.1 OpenAI API 로깅
  * 9.4.2 라마인덱스 로깅
* 9.5 정리


## 10장 임베딩 모델로 데이터 의미 압축하기
* 10.1 텍스트 임베딩 이해하기: 임베딩: 데이터의 의미를 압축한 숫자 배열(벡터)
  * 10.1.1 문장 임베딩 방식의 장점
  * 10.1.2 원핫 인코딩(one-hot encoding)
  * 10.1.3 백오브워즈(Bag of Words): 비슷한 단어가 많이 나오면 비슷한 문장/문서
  * 10.1.4 TF-IDF(Term Frequency-Inverse Document Frequency): 많은 문서에 등장하는 단어의 중요도를 작게
  	* 차원 증가, 대부분 0인 벡터, 희소(sparse)
  		* 워드투벡과 문장 임베딩은 압축된 형태: 밀집 임베딩(dense embedding)
  * 10.1.5 워드투벡(word2vec): 단어가 '함께 등장하는 빈도'
  	* 특정 단어 주변에 어떤 단어가 있는지 예측하는 모델
  		* CBOW(Continuous Bag of Words): 주변 단어로 가운데 단어를 예측
  		* 스킵그램(skip-gram): 중간 단어로 주변 단어를 예측
* 10.2 문장 임베딩 방식
  * 10.2.1 문장 사이의 관계를 계산하는 두 가지 방법
  	* BERT(Bidirectional Encoder Representations from Transformers): 바이 인코더(bi-encoder)
  	* 교차 인코더(cross-encoder)
  * 10.2.2 바이 인코더 모델 구조
  * 10.2.3 Sentence-Transformers로 텍스트와 이미지 임베딩 생성해 보기
  * 10.2.4 오픈소스와 상업용 임베딩 모델 비교하기
  	* 상업용: OpenAI: text-embedding-*, gpt-*: 적은 비용, 높은 성능: 사용자 데이터로 미세조정 지원이 없음
  	* 오픈소스: Sentence-Transformers 라이브러리로 사전 학습 모델을 로드
* 10.3 실습: 의미 검색 구현하기: semantic search
  * 10.3.1 의미 검색 구현하기
  	* Sentence-Transformers, faiss
  		* faiss: 페이스북이 개발한 벡터 연산 라이브러리: 코사인 유사도, 유클리드 거리 등 기본적 방법 지원, 벡터 검색 속도 향상을 위한 ANN(Approximate nearest Neighbor) 제공,
  * 10.3.2 라마인덱스에서 Sentence-Transformers 모델 사용하기
* 10.4 검색 방식을 조합해 성능 높이기
		* 단점 상쇄를 위해 의미 검색과 키워드 검색(동일 키워드 많이 포함될수록 유사도 높게 평가)을 조합
  * 10.4.1 키워드 검색 방식: BM25(Best Matching 25, TF-IDF 변형)
  	* TF-IDF에 문서 길이 가중치 추가
  * 10.4.2 상호 순위 조합 이해하기
* 10.5 실습: 하이브리드 검색 구현하기
  * 10.5.1 BM25 구현하기
  * 10.5.2 상호 순위 조합 구현하기
  * 10.5.3 하이브리드 검색 구현하기
* 10.6 정리


## 11장 자신의 데이터에 맞춘 임베딩 모델 만들기: RAG 개선하기
* 11.1 검색 성능을 높이기 위한 두 가지 방법
	* 교차 인코더: 두 문장 입력을 직접 비교: 정확하지만 느리고 확장성 낮음
	* 바이 인코더: 독립적 문장 임베딩, 임베딩끼리 코사인 유사도
	* 두 방식을 결합해서 RAG 성능 향상
		* 바이 인코더 => 선별된 소수의 문서를 교차 인코더로 재정렬
* 11.2 언어 모델을 임베딩 모델로 만들기
  * 11.2.1 대조 학습(contrastive learning): 관련/유사 데이터 더 가깝게 학습
  * 11.2.2 실습: 학습 준비하기
  * 11.2.3 실습: 유사한 문장 데이터로 임베딩 모델 학습하기
* 11.3 임베딩 모델 미세 조정하기
  * 11.3.1 실습: 학습 준비
  * 11.3.2 MNR 손실을 활용해 미세 조정하기
* 11.4 검색 품질을 높이는 순위 재정렬
* 11.5 바이 인코더와 교차 인코더로 개선된 RAG 구현하기
  * 11.5.1 기본 임베딩 모델로 검색하기
  * 11.5.2 미세 조정한 임베딩 모델로 검색하기
  * 11.5.3 미세 조정한 임베딩 모델과 교차 인코더 조합하기
* 11.6 정리


## 12장 벡터 데이터베이스로 확장하기: RAG 구현하기
* 12.1 벡터 데이터베이스란
		* 벡터 임베딩(데이터 의미를 담은 숫자 배열)을 키로 사용하는 DB
		* 데이터 => 임베딩 모델 => 임베딩 벡터
  * 12.1.1 딥러닝과 벡터 데이터베이스
  	* 모델이 존재, 표현 학습(representation learning)
  	* 벡터 DB 활용 단계
  		* 저장: 데이터를 임베딩 모델을 거쳐 벡터로 변환후 저장
  		* 검색: 검색할 데이터를 임베딩 모델을 거쳐 벡터로 변환하고 검색
  		* 결과 반환: 검색 쿼리의 임베딩과 거리가 가까운 벡터를 찾아 반환
  	* 유클리드 거리, 코사인 유사도, dot product
  	* 벡터 임베딩 활용 서비스 사례: 이미지 검색(핀터레스트), 유사상품 추천
  * 12.1.2 벡터 데이터베이스 지형 파악하기
  	* 벡터 라이브러리: Faiss(Meta), Annoy(Spotify), NMSLIB, ScaNN
  	* 벡터 DB(전용): Pinecone, Weaviate, Milvus, Chroma
  	* 벡터 DB(확장): Elasticsearch, PostgreSQL, MongoDB, Neo4j
* 12.2 벡터 데이터베이스 작동 원리
  * 12.2.1 KNN 검색과 그 한계: K-Nearest Neighbor
  	* 연산량이 데이터 수에 비례
  * 12.2.2 ANN 검색이란: Approximate Nearest Neighbor
  	* 정확도 약간 희생, 빠른 속도
  	* IVF(Inverted File Index), HNSW(Hierarchical Navigable Small World)
  * 12.2.3 탐색 가능한 작은 세계(NSW)
  * 12.2.4 계층 구조
* 12.3 실습: HNSW 인덱스의 핵심 파라미터 이해하기: Hierarchical Navigable Small World
  * 12.3.1 파라미터 m 이해하기
  * 12.3.2 파라미터 ef_construction 이해하기
  * 12.3.3 파라미터 ef_search 이해하기
* 12.4 실습: 파인콘으로 벡터 검색 구현하기: Pinecone
  * 12.4.1 파인콘 클라이언트 사용법
  * 12.4.2 라마인덱스에서 벡터 데이터베이스 변경하기
* 12.5 실습: 파인콘을 활용해 멀티 모달 검색 구현하기
  * 12.5.1 데이터셋
  * 12.5.2 실습 흐름
  * 12.5.3 GPT-4o로 이미지 설명 생성하기
  * 12.5.4 프롬프트 저장
  * 12.5.5 이미지 임베딩 검색
  * 12.5.6 DALL-E 3로 이미지 생성
* 12.6 정리


## 13장 LLM 운영하기
* 13.1 MLOps: Machine Learning Operations: 모델의 재현성(reproducibility)
  * 13.1.1 데이터 관리
  * 13.1.2 실험 관리
  * 13.1.3 모델 저장소
  * 13.1.4 모델 모니터링
* 13.2 LLMOps는 무엇이 다를까?
  * 13.2.1 상업용 모델과 오픈소스 모델 선택하기
  * 13.2.2 모델 최적화 방법의 변화
  * 13.2.3 LLM 평가의 어려움
* 13.3 LLM 평가하기
  * 13.3.1 정량적 지표
  	* BLEU(Bilingual Evaluation Understudy Score), n-gram, ROUGE(Recall-Oriented Understudy for Gisting Evaluation), PPL(perplexity)
  * 13.3.2 벤치마크 데이터셋을 활용한 평가
  	* ARC(AI2 Reasoning Challenge), HellaSwag, MMLU(Massive Multitask Language Understanding), TruthfulQA
  * 13.3.3 사람이 직접 평가하는 방식
  * 13.3.4 LLM을 통한 평가
  * 13.3.4 RAG 평가
  	* 신뢰성, 답변 관련성, 맥락 관련성, Ragas(RAG Assessment)
* 13.4 정리


# [4부] 멀티 모달, 에이전트 그리고 LLM의 미래

## 14장 멀티 모달
* LLM 14.1 멀티 모달 LLM이란
  * 14.1.1 멀티 모달 LLM의 구성요소
  * 14.1.2 멀티 모달 LLM 학습 과정
* 14.2 이미지와 텍스트를 연결하는 모델: CLIP
  * 14.2.1 CLIP 모델이란
  * 14.2.2 CLIP 모델의 학습 방법
  * 14.2.3 CLIP 모델의 활용과 뛰어난 성능
  * 14.2.4 CLIP 모델 직접 활용하기
* 14.3 텍스트로 이미지를 생성하는 모델: DALL-E
  * 14.3.1 디퓨전 모델 원리
  * 14.3.2 DALL-E 모델
* 14.4 LLaVA
  * 14.4.1 LLaVA의 학습 데이터
  * 14.4.2 LLaVA 모델 구조
  * 14.4.3 LLaVA 1.5
  * 14.4.4 LLaVA NeXT
* 14.5 정리


## 15장 LLM 에이전트
	* 예시: AutoGPT, MS AutoGen
	* 에이전트는 LLM과 RAG을 하나의 구성요소로 사용
* 15.1 에이전트란
  * 15.1.1 에이전트의 구성요소
  	* 환경, 감각(perception), 두뇌(brain), 행동(action)
  * 15.1.2 에이전트의 두뇌
  	* symbolic AI(규칙/지식 기반), 강화학습, meta learning, LLM
  * 15.1.3 에이전트의 감각
  * 15.1.4 에이전트의 행동
* 15.2 에이전트 시스템의 형태
  * 15.2.1 단일 에이전트
  	* AutoGPT
  * 15.2.2 사용자와 에이전트의 상호작용
  * 15.2.3 멀티 에이전트
  	* AutoGen, MetaGPT, CrewAI
* 15.3 에이전트 평가하기
* 15.4 실습: 에이전트 구현
  * 15.4.1 AutoGen 기본 사용법
  * 15.4.2 RAG 에이전트
  * 15.4.3 멀티 모달 에이전트
* 15.5 정리


## 16장 새로운 아키텍처
* 16.1 기존 아키텍처의 장단점
* 16.2 SSM: State Space Model
  * 16.2.1 S4
* 16.3 선택 메커니즘
* 16.4 맘바
  * 16.4.1 맘바의 성능
  * 16.4.2 기존 아키텍처와의 비교
* 16.5 코드로 보는 맘바


#3 부록 | 실습을 위한 준비사항
* A.1 구글 코랩 사용법
* A.2 허깅페이스 토큰
* A.3 OpenAI 토큰
