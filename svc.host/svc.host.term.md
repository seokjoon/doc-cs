# 터미널 사용법

## 퍼블리셔 레벨
* 로그아웃: ctrl + d
* 서버에 접속: ssh 사용자이름@주소(도메인 혹은 아이피)
``` ssh root@foo.bar ```
* 자동 끊김 방지: 로컬에서 ~/.ssh/config 편집
```
Host *
Protocol 2
ServerAliveInterval 240
```
