

## headless
* 입력
  * gemini --prompt "What is machine learning?"
  * echo "Explain this code" | gemini
  * cat README.md | gemini --prompt "Summarize this documentation"
* 출력
  * gemini -p "What is the capital of France?" --output-format json
  * 스트리밍: --output-format stream-json
  * 리디렉션: >, >>


## mcp server: https://geminicli.com/docs/tools/mcp-server/



## extension: https://geminicli.com/docs/extensions/getting-started-extensions/