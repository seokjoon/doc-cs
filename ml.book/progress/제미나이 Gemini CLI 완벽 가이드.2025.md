## ch 3. 컨텍스트와 GEMINI.md
* 컨텍스트
  * @dir/filename
* GEMINI.md


## ch 4. tools
* /file
* /shell 또는 /run
* /http url
* /search query


## ch 5. 멀티모달리티
* @foo.js: 텍스트 코드 참조
* @foo.png: 이미지 픽셀 참조


## ch 6. 대화와 컨텍스트 관리
* @ 기호는 대상 파일에 집중시킴
  * 복수 지시 가능
* 대화 저장/로드/편집
  * chat --write foo.json
  * chat --resume foo.json
  * chat --resume foo.json --edit
* gemini info


## ch 7. 페어 프로그래밍
## ch 8. SRE(Site Reliability Engineer: 사이트 신뢰성 엔지니어)
## ch 9. DevOps
## ch 10. 쉘 스크립트 통합
## ch 11. tool schemas
## ch 12. 커스텀 도구 연결


## ch 13. 커스텀 명령어와 프롬프트
* ~/.gemini/.prompts.yaml
  * name, prompt, {{.Input}}


## A. 명령어
* @
  * 파일 경로
  * 디렉토리 경로
  * url
  * 이미지 파일
* /


## B. GEMINI.md


## C. 보안
* .geminiignore
* --auto-execute