## 01 리액트 네이티브 개발 환경 갖추기


## 02 리액트 네이티브 기본 다지기
* 02-1 리액트 네이티브 프레임워크의 작동 원리
	* 브리지 방식 렌더링
	* npm run android
	* npm run ios
	* npx pod-install
	* 초기화
		* ./gradlew clean
		* rm -rf .gradle
		* xcodebuild clean
		* pod deintegrate
* 02-2 JSX 구문 탐구하기
* 02-3 컴포넌트와 속성 이해하기
	* faker
	* type
* 02-4 컴포넌트의 이벤트 속성 이해하기
	* Alert
	* TextInput
	* onBlur, onChangeText, onEndEditing, onFocus, onPress,


## 03 컴포넌트 스타일링
* 03-1 style 속성과 StyleSheet API 이해하기
	* StyleSheet API
		* 캐시됨, 인라인 스타일은 속도 지연
	* react-native-paper
	* ~~react-native-vector-icons~~
	* color
* 03-2 View 컴포넌트와 CSS 박스 모델
	* Platform.OS
	* Dimensions.get('window')
	* flex: 1: 부모와 동일한 크기
	* margin, padding
	* border
	* SafeArea
	* Platform.select({})
* 03-3 자원과 아이콘 사용하기
	* Image, ImageBackground
	* textAlign
	* flexDirection, justiryContent, alignItems, flexWrap, overflow
* 03-4 컴포넌트 배치 관련 스타일 속성 탐구하기
* 03-5 재사용할 수 있는 컴포넌트 만들기
	* moment, moment-with-locales-es6
	* FlatList
	* 재사용을 위한 컴포넌트
		* props, children, FC, ReactNode
		* 타입스크립트 교집합 타입 구문
		* ComponentProps
	* <Text>
		* numberOfLines, ellipsizeMode: head, middle, tail, clip
		* textDecorationLine: underline, textDecorationColor

## 04 함수 컴포넌트와 리액트 훅
* 04-1 리액트 훅 맛보기
	* 동일 리액트 혹을 여러번 호출 가능
	* 함수 컴포넌트 몸통을 제외한 블럭 {} 에서 혹 설정 불가
	* 비동기(async) 함수는 콜백 함수로 사용 불가
	* useEffect(콜백, 의존성목록)
		* 의존성 목록 중 하나라도 충족되면 콜백 실행
		* 의존성 목록이 빈 배열일 때 콜백 한번만 실행
		* 함수 반환 가능: useEffect() => { ... return () => {} }
	* useState
		* const [valCurrent, setFunc] = useState(valInit)
		* setFunc = (valNew): void
* 04-2 useMemo와 useCallback 훅 이해하기
	* useMemo: 생성한 데이터를 캐시에 저장
		* const outs = useMemo(() => ([1,2].map(v => v)), [])
	* useCallback: 생성한 콜백을 캐시에 저장
		* const cb = useCallback(() => {}, [])
* 04-3 useState 훅 이해하기
	* const [val, setVal] = useState(valInit)
* 04-4 useEffect와 useLayoutEffect 훅 이해하기
	* useLayoutEffect: 동기
	* useEffect: 비동기, 가급적 useEffect 권고
	* ActivityIndicator: 화면 기다림 UI
* 04-5 커스텀 훅 이해하기
	* BottomNavigation


## 05 콘텍스트와 ref 속성
* 05-1 콘텍스트 이해하기
* 05-2 useRef 훅 이해하기
* 05-3 useImperativeHandle 훅 이해하기


## 06 리액트 네이티브 애니메이션
* 06-1 처음 만나는 리액트 네이티브 애니메이션
* 06-2 transform 스타일 속성에 적용하는 애니메이션
* 06-3 여러 개의 애니메이션 한꺼번에 실행하기
* 06-4 PanResponder API 이해하기


## 07 리액트 내비게이션
* 07-1 리액트 내비게이션 패키지 이해하기
	* npm install @react-navigation/native 
	* npm install react-native-screens react-native-safe-area-context
	* npm install @react-navigation/stack @react-navigation/bottom-tabs @react-navigation/drawer
	* npm install react-native-reanimated react-native-gesture-handler
	* cd ios && pod-install
	* <NavigationContainer>
* 07-2 스택 내비게이션 이해하기
	* <Stack.Nvigator>, <Stack.Screen>
	* useRoute, useNavigation
	* useIsFocused, useFocusEffect
* 07-3 탭 내비게이션 이해하기
	* <Tab.Navigator>, <Tab.Screen>
* 07-4 드로어 내비게이션 이해하기


## 08 리덕스 이해하기
* 08-1 리덕스의 기본 개념
* 08-2 combineReducers 함수 이해하기
* 08-3 리덕스 미들웨어 이해하기


## 09 엑스포 앱 이해하기
* 09-1 엑스포 앱 만들기
* 09-2 베어 워크플로 프로젝트 퍼블리싱
* 09-3 JSON 웹 토큰 기반 인증 서버 만들기
* 09-4 카메라 앱 만들기