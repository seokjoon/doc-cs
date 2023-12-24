##
* curl -X GET 52.78.100.77:5000/v2/_catalog

* docker inspect CONTAINER_ID


##
* d run -it --rm --name certbot -v "/data/app/mr/ivt/etc/letsencrypt:/etc/letsencrypt" -v "/data/app/mr/ivt/var/lib/letsencrypt:/var/lib/letsencrypt" certbot/certbot certonly -d '*.memorobot.com,memorobot.com' --manual --preferred-challenges dns --server https://acme-v02.api.letsencrypt.org/directory


##
docker run -td <image>

Here is what the flags do (according to docker run --help):

-d, --detach=false         Run container in background and print container ID
-t, --tty=false            Allocate a pseudo-TTY
