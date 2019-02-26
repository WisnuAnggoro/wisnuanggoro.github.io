---
layout: post
title: "Docker Commands for Beginner"
date: 2019-02-26
tags: [docker, devops]
---

After successfully [installing Docker in my Windows 10](https://docs.docker.com/docker-for-windows/install/), there are several commands I run to my new Docker system. Here are the commands that can be used to try Docker:

## docker version

This command is used to print the version of installed Docker. Use this command to verify that Docker has been successfully installed in our system:

```bash
docker version
```

## docker login

This command is used to login to [Docker Hub](https://hub.docker.com) in order to pull and push images.

Run the following command to login to Docker Hub:

```bash
docker login
```

We will be displayed the following prompt to fill `username` and `password`:

```console
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: wisnuanggoro
Password:
Login Succeeded
```

## docker run `<image-name>`

This command is used to run a new docker image. Run the following command to start a new Docker image named `hello-world`:

```bash
docker run hello-world
```

The preceding command will run an image named `hello-world`. Docker will look for the image on our local system. If the image cannot be found, Docker will download it from `Docker Hub`.

Another command to run a new image is follow:

```bash
docker run -it ubuntu bash
```

The preceding command will run a new `Ubuntu` container. The `-it` flag allows us to interact with the shell.

## docker ps -a

This command is used to list all containers in our system. Run the following command:

```bash
docker ps -a
```

It will print the following on console:

```console
CONTAINER ID  IMAGE        COMMAND   CREATED        STATUS                    PORTS  NAMES
d2d6e9d56429  hello-world  "/hello"  6 seconds ago  Exited (0) 4 seconds ago         angry_keldysh
```

## docker start --attach `<container-id/name>`

`docker run` command will run a new instance of image. To reuse an available container that we have run before, run `docker start` as  follow:

```bash
docker start --attach angry_keldysh
```

The preceding command will run `hello-world` container named `angry_keldysh`.

## docker stop `<container-id/name>`

This command is used to stop a running container. The following command will stop container named `angry_keldysh`.

```bash
docker stop angry_keldysh
```

## docker rm `<container-id/name>`

This command is used to remove a container. The following command will remove container named `angry_keldysh`.

```bash
docker rm angry_keldysh
```

---

Source links:<br />
[docker-curriculum](https://docker-curriculum.com/)<br />
[Docker Tutorial: Get Going From Scratch](https://stackify.com/docker-tutorial/)<br />
[Lifecycle of Docker Container](https://medium.com/@nagarwal/lifecycle-of-docker-container-d2da9f85959)