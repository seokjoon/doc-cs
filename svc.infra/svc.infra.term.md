# 터미널 사용법


## alias
* vi .bashrc
  ```
  alias a='apt install'
  alias audg='apt update & apt install'
  alias ca='composer dump-autoload'
  alias d='docker'
  alias dit='docker exec -it'
  alias ds='docker ps -a'
  alias l='ls -al'
  alias p='ps -ae'
  alias pa='php artisan'
  alias pt='php artisan tinker'
  ```
* source .bashrc


## 퍼블리셔 레벨
* 로그아웃: ctrl + d
* 서버에 접속: ssh 사용자이름@주소(도메인 혹은 아이피): ``` ssh root@foo.bar ```
* 자동 끊김 방지: 로컬에서 ~/.ssh/config 편집
```
Host *
Protocol 2
ServerAliveInterval 240
```

## ssh key
```
$ ssh-keygen -t rsa
명령으로 key 생성한 뒤에
~/.ssh/id_rsa.pub 파일의 내용을
접속하려는 server의
~/.ssh/authorized_keys
파일에 넣으면 접속 가능
```

## ssh key: GCP 사례
* ssh-keygen -t rsa -C "root"
	* 결과를 .ssh/root-gcp-key 등으로 저장
* gcp => compute engine => 메타데이터 => ssh키
	* '수정' 후 root-gcp-key.pub 내용 붙여넣기
* ssh -i .ssh/root-gcp-key root@ec15.ecfirm.net
