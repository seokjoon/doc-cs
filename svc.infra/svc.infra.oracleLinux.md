
## oci
* 뭔가 변화 후 컨테이너 연결 안될때: https://svrforum.com/svr/1276559
	* firewalld 업뎃등의 이유로 iptables에 Docker chain이 등록되지 않아 발생한 상황
	* iptables -t filter -F
  * iptables -t filter -X
  * systemctl restart docker



## oracle linux

### cron
* systemctl restart crond.service

###
* docker-compose
	* yum install python3-pip
	* pip3 install setuptools-rust
	* pip3 install docker-compose

###
* https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm
* VM.Standard.A1.Flex
* cat /etc/oracle-release
* oracle linux 8.8 arm pakage
	* https://yum.oracle.com/repo/OracleLinux/OL8/developer/EPEL/aarch64/index.html

###
* sudoer 등록 (주석제거)
sudo vi /etc/sudoers
%wheel  ALL=(ALL)   ALL
* sudo vi /etc/pam.d/su (주석제거)
auth        sufficient  pam_wheel.so trust use_uid
* 그룹추가
usermod -aG wheel targetuser
