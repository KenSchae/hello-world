# DOCKER BASICS

## Table of Contents
1. [Introduction](#introduction)
2. [Building Images](#building-images)
    - [Basic build command](#basic-build-command)
3. [Managing Images](#managing-images)

## Introduction

If you are running these commands on a Linux server (because why not?), then
you need to run them as sudo. Or you can enter as the root user by using `sudo -i`

## Installation

[Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)


## BUILDING IMAGES

### Basic build command

`docker build .`

### Assign a Name:Tag to the build

Assign a name and tag to the image because you are a responsible dev. 

`docker build -t name:tag .`

## MANAGING IMAGES

### List out the images installed on this server
`docker images`

### Remove an image from this server
`docker rmi {imagename}`

### Remove all dangling (untagged) images
`docker image prune`

## MANAGING CONTAINERS

Parameters for running a container
|Switch | Description |
|-------|-------|
|-p     |(port) map a port|
|-d     |(detached mode) run in the background|
|-it    |(interactive mode) not -d|
|--rm   |(remove) the container when the service is stopped|
|--name |(name) give the container a name|
|-v     |(volume) assigns a named volume to the container| 

`docker run -p 3000:80 -d --rm --name goalsapp goals:latest`

### List all running containers
`docker ps`

### List all containers (running and not running)
`docker ps -a`

### Stop a container
`docker stop {containername}`

### Remove a stopped container
`docker rm {containername}`

### Remove ALL stopped containers
`docker container prune`

## Volumes

Volumes store persistent data that survives after a container shuts down. These are folders on the host machine that are mounted in the container. 

Volumes are managed by Docker. This means that we do not know where the volume is located and have no ability to manage them. Bind mounts solve that problem.

### Add a volume to the container

This command creates an anonymous volume. Anonymous volumes are not persisted when the container is removed.

`VOLUME ["{path}"]`
`VOLUME ["app/feedback"]`

Named volumes persist data when the container is removed. Named volumes are NOT defined in the Dockerfile, rather it is done at the command line when running the container.

`-v {volume name}:{mount location in container}`

`docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback feedback-node:volumes`

### List volumes

`docker volume ls`

### Troubleshooting

`docker logs {appname}`

## Bind Mounts

Like named volumes but we have management control over the file system. Bind mounts are not created in the Dockerfile. Bind mounts are created from terminal.

A bind mount is created by adding a second -v command. Should use quotes to protect the absolute path. 

`-v "{absolute path on host file system}:{mount location in container}"`

`docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v "/home/kschaefer/repos/webdev/docker/data-volumes-01-starting-setup:/app" feedback-node:volumes`

If you mount a volume to the app folder in the way that this command above does, then the mount will overwrite everything that the COPY and RUN commands do in the Dockerfile. This command is overwriting the container folder with the contents of the local host folder. Since the local host does not have the same npm dependencies as the container then we get an issue.

The solution is to use an anonymous volume. In the following command the folder that is defined in the anon volume is protected.

`docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v "/home/kschaefer/repos/webdev/docker/data-volumes-01-starting-setup:/app" -v /app/node_modules feedback-node:volumes`

🛸 Why do  this? Now we can make changes to the HTML files and we do NOT have to rebuild the container.

### Read Only Volume
When using a Bind Mount, the local drive that is mapped to the container is writable by the container. Since we probably don't want the container writing back to our source-code marking the volume as read-only is a good idea. Do this by adding :ro to the end of the volume declaration.

`docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v "/home/kschaefer/repos/webdev/docker/data-volumes-01-starting-setup:/app:ro" -v /app/node_modules feedback-node:volumes`

You can add volume declarations after the bind-mount to make subfolders writable if they need it. Use anonymous folders to do this. In the above example, all of app is read only but node_modules can be written by the container.

## References

[Docker & Kubernetes: The Practical Guide](https://www.udemy.com/course/docker-kubernetes-the-practical-guide/)