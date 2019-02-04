# 호스트 명령어

## 퍼블리셔 레벨
* cd: 위치 이동
	* 폴더 foo 로 이동 ``` cd foo ```
	* 상위 폴더로 이동 ``` cd .. ```
* chmod: 폴더/파일 권한 변경
	* foo 및 하부 폴더/파일을 일반적으로 사용 가능하게 변경 ``` chmod -R 644 foo ```
* chown: 폴더/파일 소유자 변경
	* foo 및 하부 폴더/파일을 웹서비스 사용자(www-data)가 읽기 가능하게 변경 ``` chown -R www-data:www-data foo ```
* cp: 폴더/파일 복사
	* foo 및 하부 폴더/파일을 bar 로 복사 ``` cp -R foo bar ```
* find: 파일 검색
	* 현재 및 하부 폴더에서 문자열 foo 가 포함된 모든 파일 위치 출력 ``` find ./ -name *foo* ```
* grep: 문자열 검색
	* foo 및 하부 폴더/파일에서 문자열 bar 가 포함된 모든 파일 위치 출력 ``` grep -R bar ./foo  ```
* ln: 폴더/파일 링크
	* foo 폴더를 bar 이름으로 심볼릭 링크 ``` ln -s foo bar ```
* ls
	* 현 위치 폴더/파일 목록 출력 ``` ls -al ```
	* foo 폴더 하부의 폴더/파일 출력 ``` ls -al foo ```
* mkdir: 폴더 생성 ``` mkdir foo ```
* mv: 폴더/파일 이동
	* foo 를 bar 로 이동(이름 변경) ``` mv foo bar ```
* rm: 폴더/파일 삭제
	* foo 및 하부 폴더/파일을 무조건 삭제 ``` rm -rf foo ```
* touch: 빈 파일 생성 ``` touch foo ```
