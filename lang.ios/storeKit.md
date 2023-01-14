## 인앱 구매
* https://developer.apple.com/documentation/storekit/in-app_purchase
* 다운로드, 샘플 구성
* Product: 제품: app store에 구성된
	* 이름, 설명, 가격
	* 구매, 구매설정, 구매결과, 구매오류
	* 사용자에게 제품 권한 부여 트랜잭션, 최근 트랜잭션
	* 구독정보, 제품식별자/유형, json
* Product.SubscriptionInfo: 제품 구독: 상태, 기간 등
	* 구독상태, 구독그룹식별, 구독기간, 구독제안자격
* Transaction: 구매
	* 환경, 속성, 변경관찰
	* 트랜잭션내역, 현재권한, 자격부여, 트랜잭션완료
	* 트랜잭션확인, json, 환불요청
* Product.SubscriptionInfo.Status: 제품 구독 상태
	* 구독상태, 변경관찰
* VerificationResult: 검증결과
	* 확인결과, 트랜잭션 속성, 구독갱신 속성, 앱 트랜잭션 속성
* VerificationError: 검증오류
	* 오류설명, 오류코드
* AppStore: 앱스토어
	* 구독관리, 장치확인, 결제설정(가능여부), 구매복원(동기화), 평가요청, 쿠폰
* AppTransaction: 앱 구매
	* 트랜잭션, 앱 정보, 구매날짜, json
* Storefront: 상점
	* 식별, 지역
* 테스트
	* StoreKit(Xcode) 테스트(앱내구입 설정 불필요), 샌드박스 테스터, TestFlight
* 테스트(샌드박스)
	* 제품 식별자 요청, 결제 트랜잭션, 구독, 서버 알림
* 스토어 키트 오류
* original api: deprecated??


## 앱 트랜잭션
* AppTransaction: 앱 구매 정보
	* 앱 트랜잭션, 앱 정보, 구매날짜
* Environment: 환경
	* 프로덕션/샌드박스/StoreKit테스트(Xcode)


## 메시지
* Message: 메시지
	* 메시지 수신, 이유, 표시요청
* DisplayMessageAction: 메시지 표시