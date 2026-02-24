## start: https://geminicli.com/docs/cli/cli-reference/
* 명령어: cat(파이프라인), -r(세션 재개)
* 옵션: --approval-mode=yolo(자동승인), --model, --list-sessions, --output-format
  * 모델 선택: auto, pro, flash, flash-lite
* extensions: disable, enable, install, list, uninstall, update --all
* mcp: add, list, remove
* skill: disable, enable, install, list, uninstall


## use: https://geminicli.com/docs/cli/tutorials/file-management/
* @: 파일/디렉토리 참조/수정/생성: 폴더가 클수록 토큰 사용량 증가
* 스킬: .gemini/skills/
* 컨텍스트: GEMINI.md: ~/.gemini/GEMINI.md, ./GEMINI.md, ./src/GEMINI.md
  * /memory: refresh, show
* !: 쉘, 엔터로 쉘모드 진입 가능
* 세션
  * gemini -r, --list-sessions, --delete-session 1
  * /resume, /rewind
* plan, todo: 명시적으로 프롬프트 요청
* 웹 검색 시키기
* mcp: list, 
  * ~/gemini/settings.json, ./gemini/settings.json
* 자동화: headless


## feature: https://geminicli.com/docs/cli/skills/
* agent skill: .gemini/skills/, ~/.gemini/skills/, 확장 프로그램의 스킬
  * /skills disable, enable, link, list
  * 스킬 생성: 프롬프트에 요청: https://geminicli.com/docs/cli/creating-skills/
* 체크포인트: 기본 비활성: /restore
* 확장 기능: /extensions list, install
* headless
  * 입력
    * gemini --prompt "What is machine learning?"
    * echo "Explain this code" | gemini
    * cat README.md | gemini --prompt "Summarize this documentation"
  * 출력
    * gemini -p "What is the capital of France?" --output-format json
    * 스트리밍: --output-format stream-json
    * 리디렉션: >, >> 
* help
  * command: /auth, /chat, /compress, /copy, /dir, /editor, /extensions, /ide, /init, /mcp, /memory, /model, /policies, /privacy, /restore, /rewind, /resume, /settings, /shells, /skills, /stats, /tools
  * 실행취소 Alt+z 또는 Cmd+z, 재개 Shift+Alt+Z 또는 Shift+Cmd+Z
  * 메모리 import: GEMINI.md 에서: @./foo/fee.md, @../bar.md
* hook: 이벤트
* mcp: settings.json, mcpServers, args, 인증
  * mcp add, disable, enable, remove
* plan 모드
* sendbox
* 설정: /settings
* OpenTelemetry
* 토큰 캐싱


## configuration: https://geminicli.com/docs/cli/custom-commands/
* 사용자 정의 command: 프롬프트들 실행: ~/.gemini/commands/, ./.gemini/commands


## extensions: https://geminicli.com/docs/extensions/
* 빌드: gemini extensions new ...
* 사례: 구조, link
* Gemini CLI extension gallery 배포
