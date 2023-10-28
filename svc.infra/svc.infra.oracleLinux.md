##
* docker-compose
	* yum install python3-pip
	* pip3 install setuptools-rust
	* pip3 install docker-compose


##
* https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm
* VM.Standard.A1.Flex
* cat /etc/oracle-release
* oracle linux 8.8 arm pakage
	* https://yum.oracle.com/repo/OracleLinux/OL8/developer/EPEL/aarch64/index.html


## 
* sudoer 등록 (주석제거)
sudo vi /etc/sudoers
%wheel  ALL=(ALL)   ALL
* sudo vi /etc/pam.d/su (주석제거)
auth        sufficient  pam_wheel.so trust use_uid
* 그룹추가
usermod -aG wheel targetuser
