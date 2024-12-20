# Docker

## Install Docker
### Set up the repository
Update the apt package index and install packages to allow apt to use a repository over HTTPS
```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
```

Add Docker’s official GPG key
```
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

Use the following command to set up the repository
```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Update the apt package index
```
sudo apt-get update
```

Install Docker Engine, containerd, and Docker Compose
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
## Docker command
Docker CLI Command
```
docker --help
```

Managing container images
```
docker image ls
docker images
```

Managing container
```
docker container ls
docker ps
docker ps -a
```

Docker information
```
docker info
```

## Docker practices
Image download
```
docker pull ubuntu
```

Running Container
```
docker run -it ubuntu
```

Execution command inside container
```
cat /etc/os-release
free -m
hostname -i
exit
```

Rename container image
```
docker rename old-name-ct new-name-ct
```

Start container
```
docker start ct-name
```

Execution command into container
```
docker exec -it ct-name cat /etc/os-release
docker exec -it ct-name /bin/bash
```

Install nginx package inside container
```
apt update
apt install nginx
apt list --installed | grep nginx
nginx -g "daemon off;"
```

Backup container to container image
```
docker commit -p ct-ubuntu ubuntu-nginx
```

Running container nginx and start nginx service
```
docker run -dit -p 8001:80 --name ct-nginx ubuntu-nginx
docker exec -it ct-nginx nginx -g "daemon off;"
```

Export and import container image
```
docker save -o output-file ct-name
docker load -i file
```

Stop container
```
docker stop container-name
```

Terminate container
```
docker rm container-name
```

Force terminate container
```
docker rm -f container-name
```

## Dockerfile
Create Dockerfile
```
vim Dockerfile
```

Edit
```
FROM ubuntu:16.04
RUN apt update -y && apt install nginx -y
ADD index.html /var/www/html/
CMD nginx -g "daemon off;"
```

Build image from Dockerfile
```
docker build -t image-name path
```
## Docker Registry
First you can create Dockerhub account [here](https://hub.docker.com/)

Docker engine login with Dockerhub credentials
```
docker login
```

Tagging image name with repository
```
docker tag image-name repository/image-name
```

Push image to Dockerhub
```
docker push repository/image-name
```
## Docker Volume
Create Docker Volume
```
docker volume create volume-name
```

Create container to attach docker volume
```
docker run -d -p host:container -v volume-name:destination image-name
```
## Docker Network
Create Docker Network with range subnet
```
docker network create --subnet 192.168.100.1/24 net-A
```

Create container to attach custom network 
```
docker run -d -p host:container -v volume-name:destination --network net-A image-name
```
## Docker Logging and Troubleshooting
Show information about container
```
docker inspect ct-name
```

Show logging container
```
docker logs ct-name
```

Show process inside container
```
docker top ct-ubuntu
```

Show resource usage on docker
```
docker stats
```

Show history image build
```
docker image history image-name
```

Show storage usage on docker
```
docker system df
```
## Docker Dashboard
You can install management dashboard docker via web ui with Portainer

Create Portainer volume
```
docker volume create portainer_data
```

Running Container Portainer
```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

Access management dashboard
```
https://ip-address:9443
```
## Docker Compose
Create compose file
```
vim docker-compose.yml
```

Build compose file
```
docker compose build
```

Running container on compose file
```
docker compose up -d
```

Stop container on compose file
```
docker compose down
```