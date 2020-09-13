## docker image
* cd /d1/app/server/seokjoon/docker/web/ami.wcms.v3.3
	* docker build --tag 192.168.1.253:5000/ami.wcms.v3.3 .
	* docker push 192.168.1.253:5000/ami.wcms.v3.3
* curl -X GET 192.168.1.253:5000/v2/_catalog


## docker swarm
* wcms-pweb01
* docker swarm init --advertise-addr 192.168.1.253
    * docker node ls
    * docker swarm leave --force
* docker network create --driver=overlay --attachable wcms-net
* docker stack deploy -c ./swarm/ami.wcms.v3.3/wcms-manager/wcms.yml wcms
* docker stack deploy -c ./swarm/ami.wcms.v3.3/wcms-manager/daemon.yml daemon
* docker stack deploy -c ./swarm/ami.wcms.v3.3/wcms-manager/vs.yml vs
    * docker stack services wcms
* docker stack ps wcms
    * docker stack remove wcms
* docker logs 컨테이너이름
* wcms-pdb01
* docker swarm join --token SWMTKN-1-2xumxhmst4wmq45voo0ua73gi88x361duh64rtlxb0wcltf7r2-bed8g0fvzm6re4ea4kbpej78a wcms-manager
    * docker swarm leave