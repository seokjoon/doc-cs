## 1장. 리액트 기초 다지기


## 2장. 리액트 네이티브식 '헬로 월드!'
* 툴 설치: 엑스코드, 홈브류, 노드와 npm, 왓치맨과 플로, 리액트 네이티브 CLI
	* npm install -g react-native-cli
* 첫 번째 리액트 네이티브 앱
	* react-native init foo
	* 리액트 네이티브 패키저
* HelloWorld 앱의 이해
* 리액트 네이티브 앱 디버깅
	* 크롬 디버거
	* 중단점


## 3장. 스타일과 레이아웃 리액트 네이티브
* 스타일 구성과 적용
	* 인라인 스타일: <View style={{ foo: bar }}></View>
	* 스타일 객체: const style = { foo: bar };
		* 여러 스타일 조합: <View style={[ foo, bar ]}></View> 혹은 <View style={Object.assign(foo, bar)}></View>
* 스타일시트
	* const styles = StyleSheet.create({ foo: { ... }, bar: { ... } }); <View style={[ styles.foo, styles.bar ]}
		* StyleSheet.hairlineWidth
	* 컴포넌트에 특정적인 스타일 속성: ex) TouchableHighlight의 underlayColor, activityOpacity
* 상속 없는 스타일링: 범위가 해당 요소로 한정되므로 스타일을 캡슐화한 (함수형)컴포넌트를 재사용
	* const Button = ({ style, children, ...otherProps }) => ( ... ); Button.propType = { style: ..., children: ..., };
* 박스 모델과 플렉스박스
	* 박스 모델
	* 플렉스박스
	* 또 다른 축 다루기
	* 크기 조절
* 텍스트 스타일링
	* 텍스트 스타일 속성
	* 텍스트 스타일 캡슐화
* 이미지 스타일링
	* 배경 이미지
* 스타일 조사와 디버깅
	* 리액트 네이티브 인스펙터
* 유사 미디어 쿼리 기능 추가
	* Dimensions 객체
	* onLayout 핸들러
* 정리


## 4장. 리액트 네이티브 컴포넌트 리액트 네이티브
* 네이티브 컴포넌트
	* Text
	* View
	* Image
	* Touchable
	* ListView
	* Modal
	* WebView
	* TabBarIOS
	* TextInput
	* 그 외의 입력 컴포넌트
* 네이티브 API
	* ActionSheetIOS
	* AlertVibration
	* StatusBar
* 정리


## 5장. 플럭스와 리덕스
* 플럭스 아키텍처
	* Motivation
	* 플럭스 구현하기
* 리덕스 시작하기
	* 리덕스의 기본 원칙
	* 리덕스 설치
	* 리덕스 구현하기
	* 리액트-리덕스
	* 미들웨어
* 정리


## 6장. NYT API와 리덕스의 통합
* NYT API 데이터의 이해
* 리덕스 데이터의 흐름
	* 리덕스 상태 트리 만들기
	* 앱에 리덕스 데이터 연결하기
	* 리팩토링과 리셰이핑
	* 리셀렉트 도입
	* 검색 기능 추가
* 비동기식 요청으로 NYT API 연결하기
	* iOS ATS에 대한 조치
	*  ‘당겨서 새로고침'과 ‘로딩 스피너'
* 정리


## 7장. 내비게이션과 고급 API
* 내비게이션
	* NavigatorIOS
	* Navigator
	* NavigationExperimental
	* 내비게이션 API의 선택
* Navigator의 사용
	* Navigator 컴포넌트
	* 내비게이션바
* NavigationExperimental의 사용
	* 내비게이션 상태 표현하기
	* 내비게이션 상태 관리
	* CardStack 컴포넌트
	* 내비게이션 헤더
	* 탭내비게이션
	* 모달 추가
* 그 밖의 고급 API
	* NetInfo를 이용한 오프라인 메시지
	* Linking을 이용한 브라우저 열기
	* AsyncStorage를 이용한 북마크 저장
* 정리


## 8장. 애니메이션과 제스처
* LayoutAnimation과 Animated 소개
* 기본형 온보딩 구축
	* 시작하기
* LayoutAnimation
	* 하나 더!
* Animated
	* 온보딩의 리팩토링
	* 온보딩 경험에 Animated 추가
	* 애니메이션 값 보정
* PanResponder 적용
	* PanResponder 보완
* 정리


## 9장. 안드로이드를 위한 리팩토링
* 툴 설치
	* JDK 설치
	* 안드로이드 스튜디오 설치
	* ANDROID_HOME과 PATH 설정
	* 안드로이드 에뮬레이터 실행
* RNNYT에 안드로이드 지원 추가
	* 플랫폼 로직의 분기
	* 안드로이드를 위한 RNNYT 리팩토링
* 정리


## 10장. 네이티브 모듈의 작성과 사용
* 네이티브 모듈 사용하기
	* 네이티브 모듈 설치
	* 아이콘 라이브러리 사용하기
* 네이티브 모듈 제작
	* iOS 네이티브 모듈
	* 안드로이드 네이티브 모듈
* 정리


## 11장. 앱 출시 준비
* 테스트
	* 단위 테스트
	* 컴포넌트 테스트
* 성능
	* 말썽쟁이 ListView
	* 낮은 반응의 터치와 느린 내비게이션
	* 성능 관련 요약
* 실제 기기에서의 실행
	* iOS 디바이스에서의 디버깅
	* 안드로이드 디바이스에서의 디버깅
* 앱 배포
	* 디버깅 코드 제거
	* iOS
	* 안드로이드
* 정리


## 12장. 리액트 네이티브 툴과 참고자료
* 리액트 네이티브 에디터, 플러그인, IDE
	* 아톰과 뉴클라이드
* iOS와 안드로이드를 넘어
	* 리액트 네이티브 웹 소개
	* 리액트 네이티브 UWP 플러그인
	* 리액트 네이티브 맥 OS
* 정리 