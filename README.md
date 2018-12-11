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

## Additional resource:
* Windows and Docker: http://peterjohnlightfoot.com/tag/docker/
* Docker 101: https://towardsdatascience.com/how-docker-can-help-you-become-a-more-effective-data-scientist-7fc048ef91d5
