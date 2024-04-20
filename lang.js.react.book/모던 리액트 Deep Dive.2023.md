## 들어가며


## 01장: 리액트 개발을 위해 꼭 알아야 할 자바스크립트
* 1.1 자바스크립트의 동등 비교
* 1.2 함수
* 1.3 클래스
* 1.4 클로저
* 1.5 이벤트 루프와 비동기 통신의 이해
* 1.6 리액트에서 자주 사용하는 자바스크립트 문법
* 1.7 선택이 아닌 필수, 타입스크립트


## 02장: 리액트 핵심 요소 깊게 살펴보기
* 2.1 JSX란?
* 2.2 가상 DOM과 리액트 파이버
* 2.3 클래스형 컴포넌트와 함수형 컴포넌트
* 2.4 렌더링은 어떻게 일어나는가?
* 2.5 컴포넌트와 함수의 무거운 연산을 기억해 두는 메모이제이션


## 03장: 리액트 훅 깊게 살펴보기
* 3.1 리액트의 모든 훅 파헤치기
  * 3.1.1 useState
  * 3.1.2 useEffect
  * 3.1.3 useMemo
  * 3.1.4 useCallback
  * 3.1.5 useRef
  * 3.1.6 useContext
  * 3.1.7 useReducer
  * 3.1.8 useImperativeHandle
  * 3.1.9 useLayoutEffect
  * 3.1.10 useDebugValue
  * 3.1.11 훅의 규칙
* 3.2 사용자 정의 훅과 고차 컴포넌트 중 무엇을 써야 할까?
  * 3.2.1 사용자 정의 훅
  * 3.2.2 고차 컴포넌트


## 04장: 서버 사이드 렌더링
* 4.1 서버 사이드 렌더링이란?
* 4.2 서버 사이드 렌더링을 위한 리액트 API 살펴보기
  * 4.2.1 renderToString
  * 4.2.2 renderToStaticMarkup
  * 4.2.3 renderToNodeStream
  * 4.2.4 renderToStaticNodeStream
  * 4.2.5 hydrate
  * 4.2.6 서버 사이드 렌더링 예제 프로젝트
* 4.3 Next.js 톺아보기
  * 4.3.3 Data Fetching
  	* getStaticPaths, getStaticProps
  * 4.3.4 스타일 적용하기
  * 4.3.5 _app.tsx 응용하기
  * 4.3.6 next.config.js 살펴보기


## 05장: 리액트와 상태 관리 라이브러리
* 5.1 상태 관리는 왜 필요한가?
* 5.2 리액트 훅으로 시작하는 상태 관리
  * 5.2.1 가장 기본적인 방법: useState와 useReducer
  * 5.2.2 지역 상태의 한계를 벗어나보자: useState의 상태를 바깥으로 분리하기
  * 5.2.3 useState와 Context를 동시에 사용해 보기
  * 5.2.4 상태 관리 라이브러리 Recoil, Jotai, Zustand 살펴보기


## 06장: 리액트 개발 도구로 디버깅하기
* 6.1 리액트 개발 도구란?
* 6.2 리액트 개발 도구 설치
* 6.3 리액트 개발 도구 활용하기
  * 6.3.1 컴포넌트
  * 6.3.2 프로파일러


## 07장: 크롬 개발자 도구를 활용한 애플리케이션 분석
* 7.2 요소 탭
* 7.3 소스 탭
* 7.4 네트워크 탭
* 7.5 메모리 탭
  * 7.5.1 자바스크립트 인스턴스 VM 선택
  * 7.5.2 힙 스냅샷
  * 7.5.3 타임라인 할당 계측
  * 7.5.4 할당 샘플링
* 7.6 Next.js 환경 디버깅하기
  * 7.6.1 Next.js 프로젝트를 디버그 모드로 실행하기
  * 7.6.2 Next.js 서버에 트래픽 유입시키기
  * 7.6.3 Next.js의 메모리 누수 지점 확인하기


## 08장: 좋은 리액트 코드 작성을 위한 환경 구축하기
* 8.1 ESLint를 활용한 정적 코드 분석
  * 8.1.2 eslint-plugin과 eslint-config
* 8.2 리액트 팀이 권장하는 리액트 테스트 라이브러리
  * 8.2.1 React Testing Library란?
  * 8.2.3 리액트 컴포넌트 테스트 코드 작성하기
  * 8.2.4 사용자 정의 훅 테스트하기


## 09장: 모던 리액트 개발 도구로 개발 및 배포 환경 구축하기
* 9.1 Next.js로 리액트 개발 환경 구축하기
  * 9.1.1 create-next-app 없이 하나씩 구축하기
  * 9.1.2 tsconfig.json 작성하기
  * 9.1.3 next.config.js 작성하기
  * 9.1.4 ESLint와 Prettier 설정하기
  * 9.1.5 스타일 설정하기
  * 9.1.6 애플리케이션 코드 작성
* 9.2 깃허브 100% 활용하기
  * 9.2.1 깃허브 액션으로 CI 환경 구축하기
  * 9.2.2 직접 작성하지 않고 유용한 액션과 깃허브 앱 가져다 쓰기
  * 9.2.3 깃허브 Dependabot으로 보안 취약점 해결하기
* 9.3 리액트 애플리케이션 배포하기
  * 9.3.1 Netlify
  * 9.3.2 Vercel
  * 9.3.3 DigitalOcean
* 9.4 리액트 애플리케이션 도커라이즈하기
  * 9.4.1 리액트 앱을 도커라이즈하는 방법
  * 9.4.2 도커로 만든 이미지 배포하기


## 10장: 리액트 17과 18의 변경 사항 살펴보기
* 10.1 리액트 17 버전 살펴보기
  * 10.1.1 리액트의 점진적인 업그레이드
  * 10.1.2 이벤트 위임 방식의 변경
  * 10.1.3 import React from ‘reac’가 더 이상 필요 없다: 새로운 JSX transform
  * 10.1.4 그 밖의 주요 변경 사항
* 10.2 리액트 18 버전 살펴보기
  * 10.2.1 새로 추가된 훅 살펴보기
  * 10.2.2 react-dom/client
  * 10.2.3 react-dom/server
  * 10.2.4 자동 배치(Automatic Batching)
  * 10.2.5 더욱 엄격해진 엄격 모드
  * 10.2.6 Suspense 기능 강화


## 11장: Next.js 13과 리액트 18
* 11.1 app 디렉터리의 등장
  * 11.1.1 라우팅
* 11.2 리액트 서버 컴포넌트
  * 11.2.3 서버 사이드 렌더링과 서버 컴포넌트의 차이
* 11.3 Next.js에서의 리액트 서버 컴포넌트
  * 11.3.1 새로운 fetch 도입과 getServerSideProps, getStaticProps, getInitial Props의 삭제
  * 11.3.2 정적 렌더링과 동적 렌더링
  * 11.3.3 캐시와 mutating, 그리고 revalidating
  * 11.3.4 스트리밍을 활용한 점진적인 페이지 불러오기
* 11.4 웹팩의 대항마, 터보팩의 등장(beta)
* 11.5 서버 액션(alpha)
  * 11.5.1 form의 action
  * 11.5.2 input의 submit과 image의 formAction
  * 11.5.3 startTransition과의 연동
  * 11.5.4 server mutation이 없는 작업
  * 11.5.5 서버 액션 사용 시 주의할 점
* 11.6 그 밖의 변화
* 11.7 Next.js 13 코드 맛보기
  * 11.7.1 getServerSideProps와 비슷한 서버 사이드 렌더링 구현해 보기
  * 11.7.2 getStaticProps와 비슷한 정적인 페이지 렌더링 구현해 보기
  * 11.7.3 로딩, 스트리밍, 서스펜스


## 12장: 모든 웹 개발자가 관심을 가져야 할 핵심 웹 지표
* 12.1 웹사이트와 성능
* 12.2 핵심 웹 지표란?
* 12.3 최대 콘텐츠풀 페인트(LCP)
* 12.4 최초 입력 지연(FID)
* 12.5 누적 레이아웃 이동(CLS)


## 13장: 웹페이지의 성능을 측정하는 다양한 방법
* 13.1 애플리케이션에서 확인하기
  * 13.1.1 create-react-app
  * 13.1.2 create-next-app
* 13.2 구글 라이트하우스
  * 13.2.1 구글 라이트하우스 - 탐색 모드
  * 13.2.2 구글 라이트하우스 - 기간 모드
  * 13.2.3 구글 라이트하우스 - 스냅샷
* 13.3 WebPageTest
  * 13.3.1 Performance Summary
  * 13.3.2 Opportunities & Experiments
  * 13.3.3 Filmstrip
  * 13.3.4 Details
  * 13.3.5 Web Vitals
  * 13.3.6 Optimizations
  * 13.3.7 Content
  * 13.3.8 Domains
  * 13.3.9 Console Log
  * 13.3.10 Detected Technologies
  * 13.3.11 Main-thread Processing
  * 13.3.12 Lighthouse Report
  * 13.3.13 기타
* 13.4 크롬 개발자 도구
  * 13.4.1 성능 통계
  * 13.4.2 성능


## 14장: 웹사이트 보안을 위한 리액트와 웹페이지 보안 이슈
* 14.1 리액트에서 발생하는 크로스 사이트 스크립팅(XSS)
  * 14.1.1 dangerouslySetInnerHTML prop
  * 14.1.2 useRef를 활용한 직접 삽입
  * 14.1.3 리액트에서 XSS 문제를 피하는 방법
* 14.2 getServerSideProps와 서버 컴포넌트를 주의하자
* 14.3 〈a〉 태그의 값에 적절한 제한을 둬야 한다
* 14.4 HTTP 보안 헤더 설정하기
  * 14.4.1 Strict-Transport-Security
  * 14.4.2 X-XSS-Protection
  * 14.4.3 X-Frame-Options
  * 14.4.4 Permissions-Policy
  * 14.4.5 X-Content-Type-Options
  * 14.4.6 Referrer-Policy
  * 14.4.7 Content-Security-Policy
  * 14.4.8 보안 헤더 설정하기
  * 14.4.9 보안 헤더 확인하기
* 14.5 취약점이 있는 패키지의 사용을 피하자
* 14.6 OWASP Top 10


## 15장: 마치며
* 15.1 리액트 프로젝트를 시작할 때 고려해야 할 사항
  * 15.1.1 유지보수 중인 서비스라면 리액트 버전을 최소 16.8.6에서 최대 17.0.2로 올려두자
  * 15.1.3 서버 사이드 렌더링 애플리케이션을 우선적으로 고려한다
  * 15.1.4 상태 관리 라이브러리는 꼭 필요할 때만 사용한다
  * 15.1.5 리액트 의존성 라이브러리 설치를 조심한다
* 15.2 언젠가 사라질 수도 있는 리액트
