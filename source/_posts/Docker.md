---

title: Docker
date: 2025-01-24 16:24:20
comment: true
category: Docker
tag: Linux Commands
---

## Definition

Docker is an open-source platfom used to build, test and deploy the work accorss the teams. It used to create the image with necessary libraries and run them on the containers.

- Docker Hub

- Docker Image

- Docker Container

- Docker Registry

- Docker Compose

<div style="display: flex; justify-content: center;">
    <img src="/images/Docker.assets/Docker1.png" style="zoom: 30%;" />
</div>

## 1. Installing Docker

```bash
sudo apt update && sudo apt upgrade
sudo apt install docker.io
docker --version
```



## 2. Basic Docker Commands

### Pull an image from docker hub

Docker images are templates for containers. Pull an image from Docker Hub (a public registry):

```bash
docker pull
```

```bash
docker pull <image-name>
# ex: docker pull ubuntu:20.04
```

### Run a container

Start a container from an image:

```bash
docker run <image-name>
```

To run in detached mode (in the background), use the -d flag:


```bash
docker run -d <image-name>
```

### List running containers

View all running containers:

```bash
docker ps
```

To see all containers (including stopped ones):

```bash
docker ps -a
```

### Stop a container

Stop a running container:

```bash
docker stop <container-id>
```

### Remove a Container

Delete a stopped container:

```bash
docker rm <container-id>
```

### Remove an Image

Delete an image:

```bash
docker rmi <image-name>
```

