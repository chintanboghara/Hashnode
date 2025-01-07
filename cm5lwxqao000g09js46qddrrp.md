---
title: "Docker Command Line Cheat Sheet: Essential Commands Guide"
seoTitle: "Docker CLI Cheat Sheet: Key Commands"
seoDescription: "Essential Docker commands for managing images and containers in a comprehensive cheat sheet for beginners and pros"
datePublished: Tue Jan 07 2025 03:30:32 GMT+0000 (Coordinated Universal Time)
cuid: cm5lwxqao000g09js46qddrrp
slug: docker-command-line-cheat-sheet-essential-commands-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736100143351/223f2971-e0ed-4eae-b94c-de60691eaac3.png
tags: cloud, docker, devops, sre, devsecops, dockerfile, docker-compose, docker-images

---

**Docker** allows you to package and run an application in a loosely isolated environment called a container. This isolation and security enable you to run many containers simultaneously on a single host. Containers are lightweight and include everything needed to run the application, so you don't have to rely on what's installed on the host. You can easily share containers while you work, ensuring that everyone you share with receives the same container that works the same way.

## INSTALLATION

**Docker Desktop is available for Mac, Linux, and Windows** [https://docs.docker.com/desktop](https://docs.docker.com/desktop)

**View example projects that use Docker** [https://github.com/docker/awesome-compose](https://github.com/docker/awesome-compose)

**Check out the documentation for information on using Docker** [https://docs.docker.com](https://docs.docker.com)

## IMAGES

**Docker images are lightweight, standalone packages that include everything needed to run an application: code, runtime, system tools, system libraries, and settings.**

* Build an Image from a Dockerfile: `docker build -t <image_name> .`
    
* Build an Image from a Dockerfile without using the cache: `docker build -t <image_name> . --no-cache`
    
* List local images: `docker images`
    
* Delete an Image: `docker rmi <image_name>`
    
* Remove all unused images: `docker image prune`
    

## DOCKER HUB

Docker Hub is a service offered by Docker for finding and sharing container images with your team. Learn more and discover images at [https://hub.docker.com](https://hub.docker.com).

* Log in to Docker: `docker login -u`
    
* Publish an image to Docker Hub: `docker push <image_name>`
    
* Search Docker Hub for an image: `docker search <image_name>`
    
* Pull an image from Docker Hub: `docker pull <image_name>`
    

## GENERAL COMMANDS

* Start the Docker daemon: `docker -d`
    
* Get help with Docker. You can also use `--help` with all subcommands: `docker --help`
    
* Display system-wide information: `docker info`
    

## CONTAINERS

A container is a runtime instance of a Docker image. It will always run the same way, no matter the infrastructure. Containers separate software from its environment, ensuring it works consistently, even with differences between development and staging.

* Create and run a container from an image with a custom name: `docker run --name <container_name> <image_name>`
    
* Run a container and publish its port(s) to the host: `docker run -p <host_port>:<container_port> <image_name>`
    
* Run a container in the background: `docker run -d <image_name>`
    
* Start or stop an existing container: `docker start|stop <container_name>`
    
* Remove a stopped container: `docker rm <container_name>`
    
* Open a shell inside a running container: `docker exec -it <container_name> sh`
    
* Fetch and follow the logs of a container: `docker logs -f <container_name>`
    
* Inspect a running container: `docker inspect <container_name>` (or `<container_id>`)
    
* List currently running containers: `docker ps`
    
* List all Docker containers (running and stopped): `docker ps --all`
    
* View resource usage stats: `docker container stats`
    

## References

1. **Docker Desktop**  
    [https://docs.docker.com/desktop](https://docs.docker.com/desktop)
    
2. **Example Projects Using Docker**  
    [https://github.com/docker/awesome-compose](https://github.com/docker/awesome-compose)
    
3. **Docker Documentation**  
    [https://docs.docker.com](https://docs.docker.com/)
    
4. **Docker Hub**  
    [https://hub.docker.com](https://hub.docker.com/)