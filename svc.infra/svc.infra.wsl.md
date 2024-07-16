
## wsl, docker: 20240716
* win 11
  * https://learn.microsoft.com/ko-kr/windows/wsl/install
    * 파워쉘(관리자모드)에서
      * wsl --list --online
      * wsl --install Ubuntu-24.04
      * wsl --set-default Ubuntu-24.04
      * wsl -l -v
        * Ubuntu-24.04 Running 2
      * ubuntu-24.04.exe config --default-user root
* docker
  * https://docs.docker.com/desktop/install/windows-install/
  * setup: resources > WSL integration > enable Ubuntu-24.04
* 수시로 재부팅

----


## requirement WSL 2
* win10 20h1, docker stable
* 필요시 재부팅

## install
* https://docs.microsoft.com/ko-kr/windows/wsl/install-win10
    * powershell(관리자)
        * dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
        * dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    * store 에서 Ubuntu 20.04 설치
* https://docs.microsoft.com/ko-kr/windows/wsl/wsl2-kernel
    * https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
    * 재부팅 후 시작버튼 앱 목록에서 Ubuntu 20.04 LTS 실행: 사용자 아이디 비번 설정
    * powershell(관리자)
        * wsl -l -v
        * wsl --set-default-version 2
        * wsl --set-version Ubuntu-20.04 2
        * wsl -l -v

## config
* ubuntu shell
    * sudo passwd
* powershell(관리자)
    * ubuntu2004.exe config --default-user root
    * 재부팅: Restart-Service LxssManager

## docker
* https://docs.docker.com/docker-for-windows/
    * https://hub.docker.com/editions/community/docker-ce-desktop-windows/
        * https://desktop.docker.com/win/stable/Docker%20Desktop%20Installer.exe
* 설치 후 로그아웃
* docker desktop 실행(환경설정): 활성화
    * use the WSL 2 based engine,
    * Resources > WSL integration: Ubuntu-20.04

## 주의사항
* i/o 성능, hot reload: 작업 대상(코드)가 wsl filesystem 내부에 있어야 함

## 웹개발환경 예시
* apt update && apt install
* apt install php-cli php-mbstring php-xml php-mysql php-bcmath php-gd php-zip php-redis mysql-client
* apt install composer
* apt install npm
* 2022/01/15: windows 10이 아닌 windows 11의 경우, wsl2에서 phpstorm의 indexing/scanning이 완료되지 않는 오류 있음
    * https://youtrack.jetbrains.com/issue/IDEA-286059
* Increasing the amount of inotify watchers
    * echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
    * echo 999999 | sudo tee -a /proc/sys/fs/inotify/max_user_watches && echo 999999 | sudo tee -a /proc/sys/fs/inotify/max_queued_events && echo 999999 | sudo tee -a /proc/sys/fs/inotify/max_user_instances && sudo sysctl -p

## phpstorm
* encoding: utf-8

## win terminal
```
"defaultProfile": "{2c4de342-38b7-51cf-b940-2309a097f518}",
"initialCols" : 162,
"initialRows" : 40,
 ...
 {
     "guid": "{2c4de342-38b7-51cf-b940-2309a097f518}",
     "hidden": false,
     "name": "Ubuntu",
     "source": "Windows.Terminal.Wsl",
     "fontFace": "D2Coding",
     "fontSize": 10,
     "commandline" : "wsl.exe ~"
},
```
