## requirement WSL 2
* win10 20h1, docker stable

## install
* https://docs.microsoft.com/ko-kr/windows/wsl/wsl2-install
    * dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    * dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    * store 에서 Ubuntu 설치
    * wsl -l -v
    * wsl --set-default-version 2
    * wsl --set-version Ubuntu-20.04 2
* https://docs.microsoft.com/ko-kr/windows/wsl/wsl2-kernel
    * https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

## config
* sudo passwd
* ubuntu2004.exe config --default-user root
* 재부팅: 파워쉘 관리자모드에서 Restart-Service LxssManager

## 주의사항
* i/o 성능, hot reload: 작업 대상(코드)가 wsl filesystem 내부에 있어야 함

## 웹개발환경 예시
* www, db, etc: docker 
* composer, git, npm, php, svn: wsl
    * Increasing the amount of inotify watchers
        * echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
        * echo 999999 | sudo tee -a /proc/sys/fs/inotify/max_user_watches && echo 999999 | sudo tee -a /proc/sys/fs/inotify/max_queued_events && echo 999999 | sudo tee -a /proc/sys/fs/inotify/max_user_instances && sudo sysctl -p

## win terminal
```
	"defaultProfile": "{2c4de342-38b7-51cf-b940-2309a097f518}",
	"initialCols" : 162,
    	"initialRows" : 40,
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
