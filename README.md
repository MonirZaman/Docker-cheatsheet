# Docker-cheatsheet

## .dockerignore file
* Ignore file type: `**/*.csv`
* Ignore specific file: `.git`

## Docker registry setup
`cat <file-storing-password> | docker login --username <username> --password-stdin <server-name-without-https-and-port>`

## Remove dangling image
`docker rmi $(docker images -q -f dangling=true)`

## Volume mount in Windows
* Unshare the volume from its properties
* Prepare a Docker user
* Share volume with the Docker user from Docker settings
* Example command to create container
`docker run --rm -dit --name "<name_of_container>" -v d:/:/ds -p 5000:5000 <image_name>`

## Run-time argument in docker build
`docker build -t <image-name>` --build-arg SSH_KEY="$(cat ~/.ssh/id_rsa)" --build-arg SSH_KEY_PUB="$(cat ~/.ssh/id_rsa.pub)"  

Sample Dockerfile utilizing the run-time argument:  
```
FROM <base-image> as intermediate

RUN apt-get update && \
    apt-get install -y \
    git \
    openssh-server \
    libmysqlclient-dev

ARG SSH_KEY
ARG SSH_KEY_PUB

RUN echo "$SSH_KEY"
RUN whoami

RUN mkdir -p /root/.ssh && \
    chmod 0700 /root/.ssh && \
    mkdir /REPO_to_create && \
    chmod 0700 /REPO_to_create && \
    ssh-keyscan REMOTE-HOST > /root/.ssh/known_hosts && \
    echo "$SSH_KEY" > /root/.ssh/id_rsa && \
    echo "$SSH_KEY_PUB" > /root/.ssh/id_rsa.pub && \
    chmod 600 /root/.ssh/id_rsa && \
    chmod 600 /root/.ssh/id_rsa.pub && \
    git clone SSH_CLONE_URL /REPO_to_create && \
    cd /REPO_to_create && \
    git checkout V1 && \
    rm -rf /REPO_to_create/.git
```  


## Authenticate Docker client to an Azure container registry
`docker login myregistry.azurecr.io`
or  
`cat ~/file.txt| docker login myregistry.azurecr.io --username <username> --password-stdin`  
Enter additional authentication information such as username through interactive prompt.

## Additional resource:
* Windows and Docker: http://peterjohnlightfoot.com/tag/docker/
* Docker 101: https://towardsdatascience.com/how-docker-can-help-you-become-a-more-effective-data-scientist-7fc048ef91d5
