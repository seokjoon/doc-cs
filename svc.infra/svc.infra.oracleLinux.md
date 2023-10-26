
## 
* sudoer 등록 (주석제거)
sudo vi /etc/sudoers
%wheel  ALL=(ALL)   ALL
* sudo vi /etc/pam.d/su (주석제거)
auth        sufficient  pam_wheel.so trust use_uid
* 그룹추가
usermod -aG wheel targetuser


##
* cat /etc/oracle-release
* oracle linux 8.8 arm pakage
	* https://yum.oracle.com/repo/OracleLinux/OL8/developer/EPEL/aarch64/index.html
