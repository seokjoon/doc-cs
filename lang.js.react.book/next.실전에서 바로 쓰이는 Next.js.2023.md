## PART 1 Next.js의 세계로

### CHAPTER 1 Next.js 알아보기
* 1.6 Next.js 시작하기
  * npx create-next-app foo
  * npm run dev


### CHAPTER 2 렌더링 전략
* 2.1 서버 사이드 렌더링 (SSR)
  * export async function getServerSideProps() {}
    * 빌드시 이 함수를 export 하는 모든 페이지에서 이 함수를 호출
    * 이 함수는 서버에서만 실행: console.log 도 브라우저에 표시되지 않음
* 2.2 클라이언트 사이드 렌더링 (CSR)
  * React.useEffect 훅
  * process.browser 변수
    * (typeof window === 'undefined')
  * 동적 컴포넌트 로딩
    * const Foo = dynamic(() => import('./Foo'), { ssr: false })
* 2.3 정적 사이트 생성 (SSG)
  * 증분 정적 재생성(ISR)
  * export async function getStaticProps() {
      return { props: {}, revalidate: 600 } //요청이 있을 경우 10분 단위로 갱신
    }


### CHAPTER 3 Next.js 기초와 내장 컴포넌트
* 3.1 라우팅 시스템
  * pages/index.js, pages/[id].js
* 페이지에서 경로 매개변수 사용하기
  * export async function getServerSideProps(context)
    * const { query, params } = context
* 컴포넌트에서 경로 매개변수 사용하기
  * const { query } = useRouter()
    * query.foo
* 클라이언트에서의 내비게이션
  * <Link href='/foo'>foo</Link>
    * preload, prefetch
  * <Link ref={{ pathname: '/foo/[bar]', query: { fee: bee }, }}>foo</Link>
  * const r = useRouter(); r.push('/foo')
    * Link 와 달리 페이지를 미리 불러오지 못함, 사용자 피드백 등에 사용하고 redirect 용도는 next.config.js 에서 redirects 사용 
* 3.2 정적 자원 제공
  * 자동 이미지 최적화
    * <Image />, next.config.js 파일의 images 속성(domains, loader)
  * 외부 서비스를 통한 자동 이미지 최적화
* 3.3 메타데이터
  * <Head {...{title:foo}} />, <title key='' />
  * 공통 메타 태그 그룹
* 3.4 _app.js와 _document.js 페이지 커스터마이징
  * _app.js: 네비게이션
  * _document.js: 메타, 컴포넌트 렌더링, 클라이언트 커스텀 스크립트



## PART 2 Next.js 실전 감각 익히기

### CHAPTER 4 코드 구성과 데이터 불러오기
* 4.1 디렉터리 구조 구성
  * 컴포넌트 구성
    * atoms, molecules, organisms, templates
  * 유틸리티 구성
  * 정적 자원 구성
    * public/manifest.json: PWA
  * 스타일 파일 구성
  * lib 파일 구성
* 4.2 데이터 불러오기
  * 서버가 데이터 불러오기
    * getStaticProps: 정적
    * getServerSideProps: 동적
  * 서버에서 REST API 사용하기
  * 클라이언트가 데이터 불러오기
  * 클라이언트에서 REST API 사용하기
  * GraphQL API 사용하기


### CHAPTER 5 지역 및 전역 상태 관리
* 5.1 지역 상태 관리
* 5.2 전역 상태 관리
  * 콘텍스트 API
  * Redux


### CHAPTER 6 CSS와 내장 스타일링 메서드
* 6.1 Styled JSX
* 6.2 CSS Module
* 6.3 SASS


### CHAPTER 7 UI 프레임워크
* 7.1 UI 라이브러리
* 7.2 Chakra UI
* 7.3 Tailwind CSS
* 7.4 Headless UI


### CHAPTER 8 커스텀 서버
* 8.1 커스텀 서버가 필요한 경우
* 8.2 Express.js 서버
* 8.3 Fastify 서버


### CHAPTER 9 테스트
* 9.1 테스트란?
* 9.2 Jest를 사용한 단위 테스트와 통합 테스트
* 9.3 Cypress를 사용한 엔드 투 엔드 테스트


### CHAPTER 10 SEO와 성능 관리
* 10.1 SEO와 성능
* 10.2 SEO와 성능 관점에서의 렌더링 전략
  * 실제 웹 사이트를 통해 살펴본 렌더링 전략의 선택 이유
  * 사진 세부 정보 페이지
  * 프라이빗 라우트
  * 선택한 렌더링 전략 정리
* 10.3 SEO 다루기
* 10.4 성능 다루기


### CHAPTER 11 배포 플랫폼
* 11.1 다양한 배포 플랫폼
* 11.2 Vercel에 배포하기
* 11.3 CDN에 정적 사이트 배포하기
* 11.4 적절한 CDN 고르기
* 11.5 아무 서버에나 Next.js 배포하기
* 11.6 도커 컨테이너에서 Next.js 애플리케이션 실행하기



## PART 3 Next.js로 상용 애플리케이션 만들기

### CHAPTER 12 인증과 사용자 세션 관리
* 12.1 인증과 사용자 세션
* 12.2 JSON web token
* 12.3 커스텀 인증
* 12.4 Auth0
* 12.5 Auth0 커스터마이징


### CHAPTER 13 GraphCMS로 온라인 상거래 웹 사이트 만들기
* 13.1 온라인 상거래 웹 사이트 만들기
* 13.2 GraphCMS 설정하기
* 13.3 상점 홈 페이지, 장바구니 및 제품 상세 페이지 만들기
* 13.4 Stripe로 결제 구현하기


### CHAPTER 14 예제 프로젝트로 살펴보는 Next.js의 다음 단계
* 14.1 무궁무진한 가능성을 가진 프레임워크
* 14.2 Next.js 연습을 위한 프로젝트
  * 스트리밍 웹 사이트
  * 블로깅 플랫폼
  * 실시간 채팅 웹 사이트
* 14.3 다음 단계
