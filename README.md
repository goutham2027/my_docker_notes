## Section-1: Setup
### Step-1: Installing Docker on ubuntu
```
apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" > /etc/apt/sources.list.d/docker.list
apt-get update
apt-get purge lxc-docker*
apt-get install -y docker-engine
service docker start
docker run hello-world
```

### Step-2: Allowing normal user to run Docker
```
usermod -aG docker <username>
```


## Section - 2: Docker CLI commands
```
docker pull ubuntu:latest
docker images
docker run -i -t ubuntu:latest /bin/bash
```


## Section - X: Running Docker on AWS/Digital Ocean from scratch

## Section - X: Running 2 Apache/nginx webserver containers and load balance them

## Section - X: Deploying Rails App using docker.


## References

