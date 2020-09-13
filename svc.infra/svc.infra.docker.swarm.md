## docker image
* cd /d1/app/server/seokjoon/docker/web/foo
	* docker build --tag 192.168.1.253:5000/foo .
	* docker push 192.168.1.253:5000/foo
* curl -X GET 192.168.1.253:5000/v2/_catalog


## docker swarm
### foo-pweb01
* docker swarm init --advertise-addr 192.168.1.253
    * docker node ls
    * docker swarm leave --force
* docker network create --driver=overlay --attachable foo-net
* docker stack deploy -c ./swarm/foo/foo-manager/foo.yml foo
* docker stack deploy -c ./swarm/foo/foo-manager/foo-daemon.yml daemon
* docker stack deploy -c ./swarm/foo/foo-manager/vs.yml vs
    * docker stack services foo
* docker stack ps foo
    * docker stack remove foo
* docker logs 컨테이너이름
### foo-pdb01
* docker swarm join --token SWMTKN-1-2xumxhmst4wmq45voo0ua73gi88x361duh64rtlxb0wcltf7r2-bed8g0fvzm6re4ea4kbpej78a foo-manager
    * docker swarm leave