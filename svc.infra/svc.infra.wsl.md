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
* 재부팅: Restart-Service LxssManager

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

## network
* PowerShell.exe -ExecutionPolicy Bypass -File .\wsl-net.ps1
```
$remoteport = bash.exe -c "ifconfig eth0 | grep 'inet '"
$found = $remoteport -match '\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}';

if( $found ){
  $remoteport = $matches[0];
} else{
  echo "The Script Exited, the ip address of WSL 2 cannot be found";
  exit;
}

#[Ports]

#All the ports you want to forward separated by coma
$ports=@(80,443,10000,3000,5000);


#[Static ip]
#You can change the addr to your ip config to listen to a specific address
$addr='0.0.0.0';
$ports_a = $ports -join ",";


#Remove Firewall Exception Rules
iex "Remove-NetFireWallRule -DisplayName 'WSL 2 Firewall Unlock' ";

#adding Exception Rules for inbound and outbound Rules
iex "New-NetFireWallRule -DisplayName 'WSL 2 Firewall Unlock' -Direction Outbound -LocalPort $ports_a -Action Allow -Protocol TCP";
iex "New-NetFireWallRule -DisplayName 'WSL 2 Firewall Unlock' -Direction Inbound -LocalPort $ports_a -Action Allow -Protocol TCP";

for( $i = 0; $i -lt $ports.length; $i++ ){
  $port = $ports[$i];
  iex "netsh interface portproxy delete v4tov4 listenport=$port listenaddress=$addr";
  iex "netsh interface portproxy add v4tov4 listenport=$port listenaddress=$addr connectport=$port connectaddress=$remoteport";
}
```

## sshd
* dpkg --purge ssh openssh-server
* apt-get update && apt-get install openssh-server
* 주석 해제 /etc/ssh/sshd_config
```
Port 22
Protocol 2
PermitRootLogin yes
AuthorizedKeysFile  .ssh/authorized_keys
PasswordAuthentication yes
PubkeyAuthentication yes
ChallengeResponseAuthentication no
X11Forwarding yes
UseDNS no
```
* ~~service ssh --full-restart~~
* ~~service ssh restart~~
* STARTUP_DIR=$(ls -d /mnt/c/Users/*/AppData/Roaming/Microsoft/Windows/Start\ Menu/Programs/Startup)
* echo 'wsl sudo /etc/init.d/ssh start' > "$STARTUP_DIR"/startup_ssh.bat