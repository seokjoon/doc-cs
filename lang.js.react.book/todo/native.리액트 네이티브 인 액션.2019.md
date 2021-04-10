# Part 01 리액트 네이티브로 시작하기

## Chapter 01 리액트 네이티브로 시작하기
### 1.1 리액트와 리액트 네이티브 소개
* 1.1.1 리액트의기본클래스
* 1.1.2 리액트생명주기
### 1.2 앞으로 배울 내용
### 1.3 알아야 할 내용
### 1.4 리액트 네이티브의 작동 방식 이해하기
* 1.4.1 JSX
* 1.4.2 스레드처리
* 1.4.3 리액트
* 1.4.4 단방향데이터흐름
* 1.4.5 디핑(코드비교)
* 1.4.6 컴포넌트로생각하기
### 1.5 리액트 네이티브의 강점
* 1.5.1 개발자가용성
* 1.5.2 개발자생산성
* 1.5.3 성능
* 1.5.4 단방향 데이터 흐름
* 1.5.5 개발자 경험
* 1.5.6 트랜스파일링
* 1.5.7 생산성과 효율성
* 1.5.8 커뮤니티
* 1.5.9 오픈 소스
* 1.5.10 빈번한 업데이트
* 1.5.11 크로스 플랫폼 모바일 앱을 만드는 대안
### 1.6 리액트 네이티브의 약점
### 1.7 기본 컴포넌트 만들어 사용하기
* 1.7.1 컴포넌트 개요
* 1.7.2 네이티브 컴포넌트
* 1.7.3 컴포넌트 구성
* 1.7.4 외부로export 가능한 컴포넌트
* 1.7.5 컴포넌트 조립하기
### 1.8 시작 프로젝트 만들기
* 1.8.1 Create React Native App CLI
* 1.8.2 React Native CLI


## Chapter 02 리액트 이해하기
### 2.1 state를 사용해 컴포넌트 데이터 다루기
* 2.1.1 컴포넌트의 상태 제대로 조작하기
### 2.2 props를 사용해 컴포넌트 데이터 다루기
### 2.3 리액트 컴포넌트 스펙
* 2.3.1 render 메서드로UI 만들기
* 2.3.2 속성 초기화와 생성자 사용하기
### 2.4 리액트 생명주기 메서드
* 2.4.1 static getDerivedStateFromProps 메서드
* 2.4.2 componentDidMount 생명주기 메서드
* 2.4.3 shouldComponentUpdate 생명주기 메서드
* 2.4.4 componentDidUpdate 생명주기 메서드
* 2.4.5 componentWillUnmount 생명주기 메서드


## Chapter 03 처음 만드는 리액트 네이티브 앱
### 3.1 todo 앱 레이아웃 작성하기
### 3.2 todo 앱 코드 작성하기
### 3.3 개발자 메뉴 열기
* 3.3.1 iOS 시뮬레이터에서 개발자 메뉴 열기
* 3.3.2 안드로이드 에뮬레이터에서 개발자 메뉴 열기
* 3.3.3 개발자 메뉴 사용하기
### 3.4 계속해서 todo 앱 만들기


# Part 02 리액트 네이티브로 앱 개발하기

## Chapter 04 스타일링 소개
### 4.1 리액트 네이티브에서 스타일 적용하고 관리하기
* 4.1.1 앱에서 스타일 적용하기
* 4.1.2 스타일 구성하기
* 4.1.3 스타일과 코드
### 4.2 View 컴포넌트에 스타일 적용하기
* 4.2.1 배경색 설정하기
* 4.2.2 border 속성 지정하기
* 4.2.3 마진(margin)과 패딩(padding) 지정하기
* 4.2.4 position을 이용해서 컴포넌트 배치하기
* 4.2.5 프로필 카드의 위치 지정하기
### 4.3 Text 컴포넌트에 스타일 적용하기
* 4.3.1 Text 컴포넌트vs View 컴포넌트
* 4.3.2 폰트 스타일
* 4.3.3 텍스트 장식하기


## Chapter 05 고급 스타일링 기법
### 5.1 플랫폼별 크기와 스타일
* 5.1.1 픽셀, 포인트,DP(DPs)
* 5.1.2 shadowPropTypesIOS와elevation 속성으로 음영 넣기
* 5.1.3 프로필 카드 예제에 음영 넣기
### 5.2 컴포넌트를 이동, 회전, 크기 변경, 기울이기
* 5.2.1 3D 효과를 내기 위한perspective 속성
* 5.2.2 translateX와translateY 속성으로 이동하기
* 5.2.3 rotateX,rotateY,rotateZ 속성으로 엘리먼트 회전하기
* 5.2.4 90도 이상 회전할 때visibility 속성 지정하기
* 5.2.5 scale,scaleX,scaleY 속성으로 화면에서 크기 변경하기
* 5.2.6 scale을 이용해 프로필 카드 섬네일 만들기
* 5.2.7 skewX와skewY 속성을 이용해X 축과Y축을 따라 기울이기
* 5.2.8 변형 효과의 핵심 포인트
### 5.3 flexbox를 이용해서 컴포넌트 배치하기
* 5.2.1 flex 속성으로 컴포넌트의 면적 변경하기
* 5.2.2 flexDirection 속성으로flex 진행 방향 지정하기
* 5.3.3 justifyContent 속성으로 컴포넌트 주위 여백 정하기
* 5.3.4 alignItems 속성으로 하위 요소들 정렬하기
* 5.3.5 alignSelf 속성으로 부모에 지정된 정렬 기준 재정의하기
* 5.3.6 flexWrap 속성으로 잘려나가지 않도록 하기


## Chapter 06 내비게이션
### 6.1 리액트 네이티브 내비게이션과 웹 내비게이션의 비교
### 6.2 내비게이션이 구현된 앱 만들기
### 6.3 데이터 유지하기
### 6.4 DrawerNavigator를 이용해서 드로어 내비게이션 만들기


## Chapter 07 애니메이션
### 7.1 Animated API 소개
### 7.2 입력창에 포커스 애니메이션 적용하기
### 7.3 애니메이션을 연결해 사용자 정의 애니메이션 만들기
### 7.4 병렬처리되는 애니메이션 만들기
### 7.5 순차적으로 처리되는 애니메이션 만들기
### 7.6 Animated.stagger 함수를 이용해서 간격 주기
### 7.7 Animated API 라이브러리 이용 시 유용한 팁
* 7.7.1 애니메이션 효과 재지정하기
* 7.7.2 애니메이션 끝난 뒤 실행되는 콜백 함수
* 7.7.3 네이티브UI 스레드에서 애니메이션 실행하기
* 7.7.4 createAnimatedComponent로 애니메이션 적용 가능 컴포넌트 만들기


## Chapter 08 리덕스 데이터 아키텍처 라이브러리 이용하기
### 8.1 리덕스란?
### 8.2 context를 이용해서 앱의 전역 state 관리하기
### 8.3 리액트 네이티브 앱에 리덕스 구현하기
### 8.4 리덕스 리듀서로 리덕스 상태 관리하기
### 8.5 provider를 추가하고 스토어 만들기
### 8.6 connect 함수를 이용해서 데이터 참조하기
### 8.7 액션 추가하기
### 8.8 리듀서에서 리덕스 스토어에 저장된 내용 지우기


# Part 03 API 레퍼런스

## Chapter 09 크로스 플랫폼 API 구현하기
### 9.1 Alert API를 이용해서 크로스 플랫폼용 알림 만들기
* 9.1.1 alert API(alerts) 활용 예
* 9.1.2 alert API를 사용하는 예제
### 9.2 AppState API를 이용해서 현재 앱 상태 확인하기
* 9.2.1 AppState API 활용 예
* 9.2.2 AppState API를 사용하는 예제
### 9.3 AsyncStorage API를 이용해서 데이터 유지하기
* 9.3.1 AsyncStorage API 활용 예
* 9.3.2 AsyncStorage API를 사용하는 예제
### 9.4 Clipboard API를 이용해서 텍스트를 사용자 클립보드에 복사하기
* 9.4.1 Clipboard API 활용 예
* 9.4.2 Clipboard API를 사용하는 예제
### 9.5 Dimensions API를 이용해서 디바이스의 화면 정보 확인하기
* 9.5.1 Dimensions API 활용 예
* 9.5.2 Dimensions API를 사용하는 예제
### 9.6 Geolocation API를 이용해서 사용자의 현재 위치 확인하기
* 9.6.1 Geolocation API 활용 예
* 9.6.2 Geolocation API를 사용하는 예제
### 9.7 Keyboard API를 이용해서 네이티브 키보드의 위치와 기능 조정하기
* 9.7.1 Keyboard API 활용 예
* 9.7.2 Keyboard API를 사용하는 예제
### 9.8 NetInfo API를 이용해서 사용자의 온라인 연결 상태 확인하기
* 9.8.1 NetInfo API 활용 예
* 9.8.2 NetInfo API를 사용하는 예제
### 9.9 PanResponder API를 이용해서 touch와 gesture 이벤트의 정보 알아 내기
* 9.9.1 PanResponder API 활용 예
* 9.9.2 PanResponder API를 사용하는 예제


## Chapter 10 iOS용 컴포넌트와 API 구현하기
### 10.1 플랫폼별 코드 지정하기
* 10.1.1 iOS와 안드로이드 파일 확장자
* 10.1.2 Platform API를 이용해서 플랫폼 확인하기
### 10.2 DatePickerIOS
* 10.2.1 DatePickerIOS를 사용하는 예제
### 10.3 PickerIOS로 데이터 목록 처리하기
* 10.3.1 PickerIOS를 사용하는 예제
### 10.4 ProgressViewIOS로 로딩 인디케이터 표시하기
* 10.4.1 ProgressViewIOS 활용 예
* 10.4.2 ProgressViewIOS를 사용하는 예제
### 10.5 SegmentedControlIOS로 수평 탭 바 만들기
* 10.5.1 SegmentedControlIOS 활용 예
* 10.5.2 SegmentedControlIOS를 사용하는 예제
### 10.6 TabBarIOS로 UI 아래에 탭 보여주기
* 10.6.1 TabBarIOS 활용 예
* 10.6.2 TabBarIOS를 사용하는 예제
### 10.7 ActionSheetIOS로 액션 시트나 공유 시트 만들기
* 10.7.1 ActionSheetIOS 활용 예+M148
* 10.7.2 ActionSheetIOS를 사용하는 예제


## Chapter 11 안드로이드 용 컴포넌트와 API 구현하기
### 11.1 DrawerLayoutAndroid로 메뉴 만들기
### 11.2 ToolbarAndroid로 툴바 만들기
### 11.3 ViewPagerAndroid로 스크롤 가능한 페이지 구현하기
### 11.4 DatePickerAndroid API로 네이티브 날짜 선택하기
### 11.5 TimePickerAndroid로 타임 피커 만들기
### 11.6 ToastAndroid로 안드로이드 토스트 메시지 구현하기

# Part 04 모든 기능을 모아 앱 개발하기

## Chapter 12 크로스 플랫폼 컴포넌트를 이용해서 StarWars 앱 만들기
### 12.1 앱 만들고 의존성 라이브러리 설치하기
* 12.1.1 People 컴포넌트를 가져오고Container 컴포넌트 만들기
* 12.1.2 내비게이션 컴포넌트를 만들고 라우트 등록하기
* 12.1.3 첫 번째 뷰의 메인 클래스 만들기
### 12.2 FlatList, Modal, Picker로 People 컴포넌트 만들기
* 12.2.1 state를 만들고 데이터를 가져오는fetch() 설정하기
* 12.2.2 기타 클래스 메서드 추가하기
* 12.2.3 render 메서드 구현하기
### 12.3 HomeWorld 컴포넌트 만들기
* 12.3.1 HomeWorld 클래스를 만들고state 초기화하기
* 12.3.2 url prop을 이용해서API로부터 데이터 가져오기
* 12.3.3 HomeWorld 컴포넌트 감싸기 