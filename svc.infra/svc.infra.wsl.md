## requirement WSL 2
* win10 20h1, docker stable, ~~hyper-v~~, ~~docker edge~~

## install
* https://docs.microsoft.com/ko-kr/windows/wsl/wsl2-install
    * dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    * dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    * ~~store 에서 Ubuntu 설치~~
    * ~~wsl --set-version Ubuntu 2~~
    * wsl --set-default-version 2
    * store 에서 Ubuntu 설치
    * wsl -l -v
* ~~https://docs.microsoft.com/ko-kr/windows/wsl/wsl2-kernel~~
    * ~~https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi~~
* ~~https://docs.docker.com/docker-for-windows/wsl-tech-preview/~~
    * ~~https://download.docker.com/win/edge/Docker%20Desktop%20Installer.exe~~

## config
* apt-get update, apt-get upgrad
* sudo passwd
* ubuntu config —default-user root

## 주의사항
* i/o 성능, hot reload: 작업 대상(코드)가 wsl filesystem 내부에 있어야 함

## 웹개발환경 예시
* www, db, etc: docker 
* composer, git, npm, php, svn: wsl