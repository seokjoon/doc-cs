##
* curl -X GET 52.78.100.77:5000/v2/_catalog

* docker inspect CONTAINER_ID


##
* d run -it --name certbot -v '/d1/app/www/etc/letsencrypt:/etc/letsencrypt' -v '/d1/app/www/var/lib/letsencrypt:/var/lib/letsencrypt' certbot/certbot certonly -d '*.memorobot.com,memorobot.com,*.ecfirm.net,ecfirm.net,*.kilmeny.net,kilmeny.net' --manual --preferred-challenges dns --server https://acme-v02.api.letsencrypt.org/directory