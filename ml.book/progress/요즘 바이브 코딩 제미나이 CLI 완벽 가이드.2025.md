# [파트 01] 제미나이 CLI 첫 만남
## 챕터 01 제미나이와 CLI의 만남
## 챕터 02 제미나이 CLI 알아보기
## 챕터 03 터미널 사용하기


## 챕터 04 설치와 인증하기
* 30초 만에 제미나이 CLI 실행하기
  * npm install -g @google/gemini-cli
  * npm update -g @google/gemini-cli
  * npm uninstall -g @google/gemini-cli
## 챕터 05 첫 대화 시작하기


[파트 02] 제미나이 CLI 제대로 써먹는 핵심 비법
## 챕터 06 효과적인 프롬프트 작성하기
## 챕터 07 프로젝트 컨텍스트 작성하기
* 컨텍스트 파일은 어떻게 동작하나요?
* 컨텍스트 작성을 위한 꿀팁
  * /init: GEMINI.md 생성


## 챕터 08 내장 명령어 알아보기
* 슬래시 명령어가 뭔가요?
  * /about: model
  * /auth
  * /chat: 저장 또는 재개
    * /chat save foo
      * 세션 단위 저장. 로컬에 저장됨. 세션이 끝나도 유지됨
    * /chat resume foo
  * /compress: 컨텍스트 요약(세션 단위)
  * /copy: 마지막 결과를 클립보드에 복사
  * /clear
  * /directory, /dir: 디렉토리를 컨텍스트에 추가
  * /docs
  * /editor
  * /extensions: 사용 가능한 확장 기능
  * /help
  * /ide
  * /init: GEMINI.md 자동 생성
  * /mcp: mcp 서버, 도구 나열
  * /memory
    * /memory add foo: 컨텍스트 파일에 추가
    * /memory show
    * /memory refresh: 컨텍스트 파일 다시 읽음
  * /model
  * /privacy
  * /quit, /exit
  * /restore
  * /settings: .gemini/settings.json 내용 수정
  * /stats
  * /theme
  * /tools
* 셸 명령어를 바로 실행하는 셸 모드: !
* 외부 자료 참조를 위한 @ 명령어: @


## 챕터 09 내장 도구 알아보기
* 내장 도구 작동 단계: 사용자에게 보이지 않음
* 정확한 정보가 필요할 땐 검색 도구: web_fetch, google_web_search
* 파일 관리를 위한 파일시스템 도구: list_directory, read_file, read_many_files, write_file, write_todos, glob, search_file_content, replace, 
* 다양한 내장 도구: run_shell_command, save_memory
* 제미나이 CLI 커맨드라인
  * 모델 지정: gemini -m "foo"
  * 명령 지정(일회성): gemini -p "google_web_search('do foo')" 
  * 자동 승인: -y, --yolo
  * 이어서 작업: -r
  * 디버그 모드: -d
## 챕터 10 깃 & 깃허브 함께 사용하기


[파트 03] 나만의 제미나이 CLI를 만드는 AI 개인화

## 챕터 11 설정 파일 알아보기
* 제미나이 CLI 설정
  * 커맨드라인, 환경변수, 프로젝트 설정파일(foo/.gemini/settings.json), OS 유저 설정파일(~/.gemini/settings.json), 기본값
* 나를 위한 도구를 만드는 settings.json
* .env에 환경 변수 설정하기


## 챕터 12 안전하게 작업하기
* 체크포인트가 뭔가요?
* 보안 강화를 위한 격리 환경, 샌드박싱


## 챕터 13 커스텀 도구 만들기
* 커스텀 도구 알아보기
  * 스크립트 2, 설정 2
  * discovery script: 도구 이름, 설명, 파라미터
  * execution script: 실행
  * settings.json: 스크립트 위치
  * GEMINI.md
* 간단한 커스텀 도구 생성하기


## 챕터 14 MCP로 제미나이 CLI 확장하기
* MCP 이해하기: Model Context Protocol
  * settings.json
  * https://geminicli.com/extensions
  * https://github.com/modelcontextprotocol/servers
  * https://smithery.ai
* 옵시디언 MCP 사용하기
* 다양한 MCP 기능 확인하기
  * /mcp list

## 챕터 15 확장 기능 정의하기
* 확장 기능의 구조와 동작 원리
* gemini-extension.json
* 확장 기능과 settings.json의 차이


[파트 04] 일상과 업무를 혁신하는 생산성 레시피
## 챕터 16 마크다운 업무 보고서 만들기
## 챕터 17 발표 자료 만들기
## 챕터 18 프로젝트 공유하기
## 챕터 19 파일 관리 자동화하기
## 챕터 20 체계적으로 문서 작업하기
[파트 05] 실전 블로그 자동화 프로젝트
## 챕터 21 프로젝트 준비하기
## 챕터 22 커스텀 도구로 워크플로 구축하기
## 챕터 23 자료 수집과 글 작성하기
## 챕터 24 깃허브에 블로그 게시하기
[파트 06] 실전 코인 모니터링 프로젝트
## 챕터 25 애플리케이션 기획하기
## 챕터 26 비즈니스 로직 구현하기
## 챕터 27 웹 서비스를 애플리케이션으로 만들기