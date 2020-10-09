## ssh allow
* vi /etc/ssh/sshd_config
```
PermitRootLogin yes
PasswordAuthentication yes
```


## sftp test: https://linuxconfig.org/how-to-setup-sftp-server-on-ubuntu-20-04-focal-fossa-linux
* apt install ssh
* vi /etc/ssh/sshd_config
```
Match group sftp
ChrootDirectory /home
X11Forwarding no
AllowTcpForwarding no
ForceCommand internal-sftp
```
* systemctl restart ssh