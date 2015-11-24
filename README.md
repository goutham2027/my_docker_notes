## Section-1: Setup
##### Step-1: Installing Docker on ubuntu
```
apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" > /etc/apt/sources.list.d/docker.list
apt-get update
apt-get purge lxc-docker*
apt-get install -y docker-engine
service docker start
docker run hello-world
```

##### Step-2: Allowing normal user to run Docker
```
usermod -aG docker <username>
```


## Section - 2: Docker CLI commands
```
docker pull ubuntu:latest # To pull latest ubuntu image

docker images # Displays all images

docker run -i -t ubuntu:latest /bin/bash # Runs ubuntu container with
bash prompt

docker search centos

docker info

```



## Section - X: Running 2 nginx webserver containers and load balance them
```
docker pull ubuntu:latest

docker run -it ubuntu:latest /bin/bash

# apt-get update
# apt-get install curl
```

Installing nginx, php on ubuntu.
Refer: https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-12-04

After installing nginx, php and create an index.php exit from container and
commit.

Configuration for: <br/>
container nginx conf: <br/>
  path: /etc/nginx/sites-available/default <br/>
  config file: templates/nginx_with__php/default_container <br/>

VM nginx conf (for loadbalancing) <br/>:
  path: /etc/nginx/sites-available/default <br/>
  config file: templates/nginx_with__php/default_vm <br/>

index.php <br/>
  path: /var/www/html/index.php <br/>
  file: templates/nginx_with__php/index.php <br/>

Starting nginx and php5-fpm run when container boots up.
Append the following lines to ~/.bashrc.
```
service nginx start
service php5-fpm start
```

Committing and pushing to Dockerhub.
```
docker commit <id> <dockerhub_username>/<image_name>:<tag>
eg: docker commit 43cb7dc12ecf goutham2027/ubuntu:with_nginx_php

docker push goutham2027/ubuntu:with_nginx_php
```

Lets remove the image and pull from Dockerhub.
```
docker rmi <image id>

docker pull goutham2027/ubuntu:with_nginx_php

docker images
```

Starting two containers.
```
docker run -dit -p 8081:80 goutham2027/ubuntu:with_nginx_php /bin/bash
docker run -dit -p 8082:80 goutham2027/ubuntu:with_nginx_php /bin/bash
```

Lets curl from VM. It displays the image id of the container serving the
request.
```
curl localhost:8081
curl localhost:8082
```

As reverse proxy has been setup, we can directly access VMs IP
```
curl <localhost>/<IP of VM>
```

## Section - X: Deploying Rails App using docker.


## Section - X: Running Docker on AWS/Digital Ocean from scratch


## References

