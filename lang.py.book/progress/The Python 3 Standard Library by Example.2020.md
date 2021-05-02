## 1장 텍스트
* 1.1 string: 텍스트 상수와 템플릿
    * deprecated
* 1.2 textwrap: 텍스트 문단 포매팅
    * .shorten(src, length, placeholder)
* 1.3 re: 정규 표현식
    * .search(pattern, src)
        * .start(), .stop()
    * .compile()
    * .findall(pattern, src), .finditer(pattern, src)
    * 패턴: 반복, 문자집합, 이스케이프, 앵커링, 제한, 그룹 매칭 분리, 옵션, 전/후방, ... 
* 1.4 difflib: 시퀀스 비교
    * .splitlines()
    * print('\n'.join(difflib.Differ().compare('foo', 'bar')))
    * print('\n'.join(difflib.unified_diff('foo', 'bar', lineterm='')))
    * .get_opcodes()


## 2장 자료 구조
* 2.1 enum: 열거 타입
    * class Foo(enum.Enum)
* 2.2 컬렉션: 컨테이너 데이터 타입
    * .ChainMap(dicA, dicB): 여러 딕셔너리 검색
    * .Counter(): 동일 값이 몇번 추가됐는지 기록
    * .defaultdict(0): 없는 키 기본값 반환
    * .deque(): 양방향 큐, 스레드 세이프, 큐 크기 제한
    * .nametuple(): tuples 에 이름 할당
    * .OrderedDict: 키가 딕셔너리에 추가된 순서 저장, 재정렬, 
* 2.3 array: 연속된 고정 타입 자료
    * fixed-size primitive type
    * 사용할 타입과 초기 데이터 시퀀스를 인자로 생성
        * foo = array.array('i', range(3))
        * int(b, B, i, I), short(h, H), long(l, L, q, Q), float(f, d)
        * .extend(), foo[2:5], list(enumerate(foo))
    * 파일
        * tempfile.NamedTemporaryFile(), .flush()
        * .tofile(), fromfile(), .read(), .seek()
    * 바이트 순서 변경
* 2.4 heapq: 힙 정렬 알고리즘
    * 생성: .heappush(), .heapify()
    * 가장 작은 값부터 제거: .heappop()
    * 변경: .heapreplace()
    * 최대/최소값: .nlargest(), nsmallest()
* 2.5 bisect: 리스트를 정렬된 상태로 유지
    * 정렬 유지하며 삽입: .bisect(), .insort(), insort_right(), insort_left()
* 2.6 queue: 스레드 안전한 FIFO 구현
    * FIFO: .Queue(), .put(), .get()
    * LIFO: .LifoQueue()
    * 우선순위 선택: .PriorityQueue()
    * 멀티스레드 활용 예제
* 2.7 struct: 바이너리 문자열을 파이썬 primitive 로 변환
    * 패킹, 언패킹: .Struct() .pack(), .unpack()
    * 인코딩: .encode(), 엔디언
    * 버퍼: ctypes.*, pack_into(), .unpack_from()
* 2.8 weakref: 객체에 대한 임시 참조(가비지 컬렉션 가능)
    * 참조, (삭제시)콜백
        * weakref.ref(foo, callback)
    * 파이널라이즈
        * weakref.finalize(foo, on_finalize, param)
            * 추적할 객체, 가비비 컬렉션시 호출될 callable 객체, callable에 전달할 인자
        * 콜백 비활성: .atexit()
        * 참조가 유지되어 가비지 컬렉션 방지


* 2.9 copy: 객체 복사
* 2.10 pprint: 자료 구조를 보기 좋게 출력


## 3장 알고리즘
* 3.1 functools: 함수를 다루기 위한 도구
* 3.2 itertools: 반복자 함수
* 3.3 operator: 내장 연산자에 대한 함수형 인터페이스
* 3.4 contextlib: 콘텍스트 매니저 유틸리티


## 4장 날짜와 시간
* 4.1 time: 시간
* 4.2 datetime: 날짜와 시간 값 다루기
* 4.3 calendar: 날짜 관련 작업


## 5장 수학 계산
* 5.1 decimal: 고정, 부동소수점 계산
* 5.2 fractions: 유리수
* 5.3 random: 의사 난수 생성기
* 5.4 math: 수학 함수
* 5.5 statistics: 통계 연산


## 6장 파일 시스템
* 6.1 os.path: 플랫폼 독립적 파일명 관리
* 6.2 pathlib: 객체로서의 파일 시스템 경로
* 6.3 glob: 파일명 패턴 매칭
* 6.4 fnmatch: 유닉스 스타일 Glob 패턴 매칭
* 6.5 linecache: 텍스트 파일 효율적으로 읽기
* 6.6 tempfile: 임시 파일 시스템 객체
* 6.7 shutil: 고수준 파일 작업
* 6.8 filecmp: 파일 비교
* 6.9 mmap: 메모리 맵 파일
* 6.10 codecs: 문자열 인코딩과 디코딩
* 6.11 io: 텍스트와 바이너리, Raw 스트림 입출력 도구


## 7장 데이터 보존과 교환
* 7.1 pickle: 객체 직렬화
* 7.2 shelve: 객체 보존
* 7.3 dbm: 유닉스 키-값 데이터베이스
* 7.4 sqlite3: 임베디드 관계형 데이터베이스
* 7.5 xml.etree.ElementTree: XML 조작 API
* 7.6 csv: 쉼표로 구분한 값 파일


## 8장 데이터 압축과 보관
* 8.1 zlib: GNU zlib 압축
* 8.2 gzip: GNU zip 파일 읽고 쓰기
* 8.3 bz2: bzip2 압축
* 8.4 tarfile: Tar 아카이브 접근
* 8.5 zipfile: ZIP 아카이브 접근


## 9장 암호 기법
* 9.1 hashlib: 암호화 해싱
* 9.2 hmac: 암호 메시지 서명과 검증


## 10장 프로세스, 스레드, 코루틴을 통한 병렬 작업
* 10.1 subprocess: 추가 프로세스 생성
* 10.2 signal: 비동기 시스템 이벤트
* 10.3 threading: 프로세스 내에서 병렬 작업 관리
* 10.4 multiprocessing: 프로세스를 스레드처럼 관리
* 10.5 asyncio: 비동기적 I/O, 이벤트 루프, 병렬 작업 도구
* 10.6 concurrent.futures: 병렬 작업 풀 관리


## 11장 네트워킹
* 11.1 ipaddress: 인터넷 주소
* 11.2 socket: 네트워크 통신
* 11.3 selectors: I/O 멀티플랙싱 추상화
* 11.4 select: 효율적인 I/O 대기
* 11.5 socketserver: 네트워크 서버 생성


## 12장 인터넷
* 12.1 urllib.parse: URL을 컴포넌트로 나눔
* 12.2 urllib.request: 네트워크 리소스 액세스
* 12.3 urllib.robotparser: 인터넷 스파이더 접근 컨트롤
* 12.4 base64: 바이너리 데이터를 아스키로 인코드
* 12.5 http.server: 웹 서비스 구현을 위한 베이스 클래스
* 12.6 http.cookies: HTTP 쿠키
* 12.7 webbrowser: 웹 페이지 보여주기
* 12.8 uuid: 보편적인 고유 식별자
* 12.9 json: 자바스크립트 객체 표기법
* 12.10 xmlrpc.client: XML-RPC용 클라이언트 라이브러리
* 12.11 xmlrpc.server: XML-RPC 서버


## 13장 이메일
* 13.1 smtplib: 단순 메일 전송 프로토콜 클라이언트
* 13.2 smtpd: 메일 서버 구현
* 13.3 mailbox: 이메일 아카이브 관리
* 13.4 imaplib: IMAP4 클라이언트 라이브러리


## 14장 애플리케이션 빌딩 블록
* 14.1 argparse: 커맨드라인 옵션과 인자 파싱
* 14.2 getopt: 커맨드라인 옵션 파싱
* 14.3 readline: GNU readline 라이브러리
* 14.4 getpass: 보안 패스워드 프롬프트
* 14.5 cmd: 줄 단위 명령 프로세서
* 14.6 shlex: 셸 스타일 구문 파싱
* 14.7 configparser: 구성 파일 작업
* 14.8 logging: 상태, 에러, 정보 메시지 보고
* 14.9 fileinput: 커맨드라인 필터 프레임워크
* 14.10 atexit: 프로그램 종료 콜백
* 14.11 sched: 이벤트 스케줄러


## 15장 국제화와 지역화
* 15.1 gettext: 메시지 카탈로그
* 15.2 locale: 문화 지역화 API


## 16장 개발자 도구
* 16.1 pydoc: 모듈의 온라인 도움말
* 16.2 doctest: 문서를 통한 테스트
* 16.3 unittest: 자동화된 테스팅 프레임워크
* 16.4 trace: 프로그램의 흐름 추적
* 16.5 traceback: 예외와 스택 추적
* 16.6 cgitb: 상세한 트레이스백 보고서
* 16.7 pdb: 대화형 디버거
* 16.8 profile과 pstats: 성능 분석
* 16.9 timeit: 파이썬 코드의 실행 시간 측정
* 16.10 tabnanny: 들여쓰기 검증
* 16.11 compileall: 소스 파일 바이트 컴파일
* 16.12 pyclbr: 클래스 브라우저
* 16.13 venv: 가상 환경
* 16.14 ensurepip: 파이썬 패키지 인스톨러 설치


## 17장 런타임 기능
* 17.1 site: 사이트 구성
* 17.2 sys: 시스템 종속적인 구성
* 17.3 os: 운영체제 종속적인 기능의 액세스
* 17.4 platform: 시스템 버전 정보
* 17.5 resource: 시스템 리소스 관리
* 17.6 gc: 가비지 컬렉터
* 17.7 sysconfig: 인터프리터 컴파일 타임 구성


## 18장 언어 도구
* 18.1 warnings: 치명적이지 않은 경고
* 18.2 abc: 추상 베이스 클래스
* 18.3 dis: 파이썬 바이트코드 역어셈블러
* 18.4 inspect: 라이브 객체 검사


## 19장 모듈과 패키지
* 19.1 importlib: 파이썬의 임포트 메커니즘
* 19.2 pkgutil: 패키지 유틸리티
* 19.3 zipimport: ZIP 아카이브에서 파이썬 코드 로드


## 부록 A 포팅 노트
* A.1 참조
* A.2 새 모듈
* A.3 이름이 바뀐 모듈
* A.4 제거된 모듈
* A.5 더 이상 사용하지 않게 된 모듈
* A.6 모듈 변경 사항 요약


## 부록 B 표준 라이브러리 확장
* B.1 텍스트
* B.2 알고리즘
* B.3 날짜와 시간
* B.4 수학 함수
* B.5 데이터 영속성과 교환
* B.6 암호화
* B.7 프로세스와 스레드, 코루틴과 함께 하는 동시성
* B.8 인터넷
* B.9 이메일
* B.10 애플리케이션 빌딩 블록
* B.11 개발 도구 