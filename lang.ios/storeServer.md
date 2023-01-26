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
* 구매목록(구매내역): Get Transaction History(거래 내역 가져오기)
	* /inApps/v1/history/{originalTransactionId}
	* https://developer.apple.com/documentation/appstoreserverapi/get_transaction_history
	* 응답: https://developer.apple.com/documentation/appstoreserverapi/historyresponse
		* signedTransactions: 고객의 인앱 구매 거래 배열
* 구독상태
	* /inApps/v1/subscriptions/{originalTransactionId}
	* https://developer.apple.com/documentation/appstoreserverapi/get_all_subscription_statuses
	* 응답: https://developer.apple.com/documentation/appstoreserverapi/statusresponse
		* data: 거래 정보, 갱신 정보를 포함한 자동 갱신 구독에 대한 일련의 정보
* 소비정보(환불근거)
	* /inApps/v1/transactions/consumption/{originalTransactionId}
	* https://developer.apple.com/documentation/appstoreserverapi/send_consumption_information
	* 요청(PUT): 앱스토어가 환불을 판단하기 위해 서버에 알림을 보내면 서버는 12시간 이내에 응답
* 구매항목(주문 ID 조회, 영수증)
	* https://developer.apple.com/documentation/appstoreserverapi/look_up_order_id
	* /inApps/v1/lookup/{orderId}
	* 응답: https://developer.apple.com/documentation/appstoreserverapi/orderlookupresponse
		* signedTransactions: 고객의 인앱 구매 거래 배열	
* 환불조회
	* /inApps/v2/refund/lookup/{originalTransactionId}
	* https://developer.apple.com/documentation/appstoreserverapi/get_refund_history
	* 응답: https://developer.apple.com/documentation/appstoreserverapi/refundhistoryresponse
		* signedTransactions: 최대 20개의 트랜잭션 목록 또는 (환불 받지 못한 경우)빈 배열, 오름차순
* 구독연장(보상)
	* /inApps/v1/subscriptions/extend/{originalTransactionId}
	* https://developer.apple.com/documentation/appstoreserverapi/extend_a_subscription_renewal_date
	* 요청(PUT): https://developer.apple.com/documentation/appstoreserverapi/extendrenewaldaterequest
		* 년당 2회, 회당 최대 90일
	* 응답: https://developer.apple.com/documentation/appstoreserverapi/extendrenewaldateresponse
* 알림목록: 앱스토어 서버가 서버로 보내려고 시도한 알림 목록
	* /inApps/v1/notifications/history
	* https://developer.apple.com/documentation/appstoreserverapi/get_notification_history
	* 요청(POST): https://developer.apple.com/documentation/appstoreserverapi/notificationhistoryrequest
	* 응답: 알림 기록 배열
* 알림생성(테스트)
	* /inApps/v1/notifications/test
	* https://developer.apple.com/documentation/appstoreserverapi/request_a_test_notification
	* 요청(POST)
	* 응답: 테스트 알림 식별 토큰
* 알림항목
	* /inApps/v1/notifications/test/{testNotificationToken}
	* https://developer.apple.com/documentation/appstoreserverapi/get_test_notification_status
	* 응답: https://developer.apple.com/documentation/appstoreserverapi/checktestnotificationresponse
		* signedPayload: 알림 내용


## JWS(json 웹 서명)

## 오류