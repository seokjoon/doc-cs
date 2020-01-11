# 터미널 사용법

## 퍼블리셔 레벨
* 로그아웃: ctrl + d
* 서버에 접속: ssh 사용자이름@주소(도메인 혹은 아이피): ``` ssh root@foo.bar ```
* 자동 끊김 방지: 로컬에서 ~/.ssh/config 편집
```
Host *
Protocol 2
ServerAliveInterval 240
```

## ssh key: GCP 사례
* ssh-keygen -t rsa -C "root"
	* 결과를 .ssh/root-gcp-key 등으로 저장
* gcp => compute engine => 메타데이터 => ssh키
	* '수정' 후 root-gcp-key.pub 내용 붙여넣기
* ssh -i .ssh/root-gcp-key root@ec15.ecfirm.net