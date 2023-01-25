* https://developer.apple.com/documentation/appstoreserverapi

## 앱스토어 서버 api
* app store connect
	* 앱: 구매, 구독 등록
	* 사용자 및 액세스: sendbox 사용자 등록, 키 등록
* host
	* sandbox: https://api.storekit-sandbox.itunes.apple.com
	* production: https://api.storekit.itunes.apple.com
* jwt
	*  composer require lcobucci/jwt
		* https://github.com/lcobucci/jwt
			* https://lcobucci-jwt.readthedocs.io/en/latest/quick-start/

##
* {originalTransactionId}: 구매에 사용된 트랜잭션 아이디, 앱스토어가 서버에 보내는 알림에 포함됨
* {orderId}: (영수증의)주문 아이디
* {testNotificationToken}: 테스트 알림 토큰
* 구매 내역: Get Transaction History(거래 내역 가져오기)
	* /inApps/v1/history/{originalTransactionId}
	* https://developer.apple.com/documentation/appstoreserverapi/get_transaction_history
	* 응답: https://developer.apple.com/documentation/appstoreserverapi/historyresponse
		* signedTransactions: JSON 웹 서명 형식으로 Apple 에서 서명한 고객의 인앱 구매 거래 배열
* 구독 상태
	* /inApps/v1/subscriptions/{originalTransactionId}
	* https://developer.apple.com/documentation/appstoreserverapi/get_all_subscription_statuses
* 소비 정보
	* /inApps/v1/transactions/consumption/{originalTransactionId}
* 주문 ID 조회, 영수증
	* /inApps/v1/lookup/{orderId}
* 환불 조회
	* /inApps/v2/refund/lookup/{originalTransactionId}
* 구독 갱신 날짜 연장
	* /inApps/v1/subscriptions/extend/{originalTransactionId}
* 알림 기록: 앱스토어 서버가 서버로 보내려고 시도한 알림 목록
	* /inApps/v1/notifications/history
* 알림 생성(테스트)
	* /inApps/v1/notifications/test
* 알림 내용
	* /inApps/v1/notifications/test/{testNotificationToken}

## JWS(json 웹 서명)

## 오류