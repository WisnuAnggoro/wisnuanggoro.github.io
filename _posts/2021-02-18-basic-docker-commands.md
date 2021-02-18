---
layout: post
title: "Basic Docker Commands"
date: 2020-02-18
tags: [docker, devops]
---

These're the basic Docker commands we should really know:

## 1. run

The Docker **run** command is used to run a container from an image. Let's run the following command:

```bash
docker run nginx
```

Running the preceding command will run an instance of the `nginx` application on the docker host if the image already exists. If the image is not present on the host, Docker will go out to **docker-hub** and pull that image down. This process is only done the first time for the subsequent executions. The same image will be reused if we run the preceding command again.

## 2. pull

When we ran the Docker `run` command earlier, it downloaded the `nginx` image as it couldn't find one locally. What if we simply want to download the image and keep it on our host so the next time we run the Docker `run` command we don't need to wait for it to download?

For the answer, we can use the Docker `pull` command. It will only pull the image and not run the container. Let's run the following command:

```bash
docker pull ubuntu
```

By running the preceding command, Docker will only pulls the Ubuntu image from **docker-hub** and will not create any container using that image.

## 3. images

As we have discussed earlier, Docker will download image from **docker-hub** when we create a container for the first time or when we run `pull` command.

If we want to list all images that available in our host, we can run `images` command as follow:

```bash
docker images
```

The output of the preceding should be a list of available images on our host. For instance:

```bash
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
nginx                      latest              35c43ace9216        20 hours ago        133MB
ubuntu                     latest              f63181f19b2f        4 weeks ago         72.9MB
```

## 4. ps

The Docker `ps` command will list all running containers and some basic information about them such as the container ID, the name of the image we used to run the containers, the current status and the name of the container. Each container automatically gets a random ID and name created for it by Docker.

Now, let's run the following command:

```bash
docker ps
```

When I run the preceding command, the response in my machine is as follow: 

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
de9a6c766f31        nginx               "/docker-entrypoint.…"   11 seconds ago      Up 10 seconds       80/tcp              funny_hermann
```

As we can see, the Docker create a random name for container `nginx`, which is `funny_hermann`

To see all containers that is running or not, use the `-a` option. The command should be as follow:

```bash
docker ps -a
```

The preceding command will output all running containers as well as previously stopped or exited containers.


## 5. stop

The Docker `stop` command will stop a running container. When we use the `stop` command, we have to provide either the container ID or the container name. If we're not sure of the name, run the `docker ps` command to get it.

Here the example command to stop `nginx` container we have created when running `docker run nginx`:

```bash
docker stop de9a6
```

**NOTE:** `de9a6` is the container ID that we get by running `docker ps` command. We don't need to provide completed container ID, instead several different first character only.

After we stop the container and we run `docker ps -a` command, the container we've just stopped is appear as `Exited` state.

## 6. rm

After we stop a container and will not use it anymore, we can delete it so it's not consume space. To do that, we can use `rm` command to remove the stopped or exited container permanently. The command is as follow:

```bash
docker rm de9a6
```

Note that the preceding command need either the container ID or the container name (as we also use in **stop** command). Use `docker ps -a` to get the container name or ID.

If `rm` command run successfully, it will response the container ID we have provided in the command.

## 7. rmi

The Docker **rmi** command is used to remove image we are not using anymore. We can see the list of available images on our host by running `docker images` command.

To remove an image that we're no longer plan to use, run the `rmi` command as follow:

```bash
docker rmi f6318
```

The preceding command will permanently remove `ubuntu` image from our host since its ID begins with `f6318`.

**REMEMBER:** We must ensure that no containers are running off of that image before attempting to remove the image. We have to stop and delete all dependent containers to be able to delete an image.

## 8. exec

Now, let's talk about `exec` command. But, before that, we need to understand more about the flow of the docker.

Suppose we run a docker container from an Ubuntu image by running the following command:

```bash
docker run ubuntu
```

By running the preceding command, Docker runs an instance of ubuntu image and exits immediately. If we list the running containers by running `docker ps` command, we won't see the container running.

However, if we list all containers including those that are stopped by running `docker ps -a` command, we will see that the new container we ran is in an exited stage.

Why can it happen?

Containers are not meant to host an operating system. Containers are meant to run a specific task or process such as to host an instance of a web server or application server or a database or simply to carry some kind of computation or analysis task. Once the task is complete the container exits. A container only lives as long as the process inside it is alive.

If the web service inside the container is stopped or crash then the container exits. This is why when we run a container from an Ubuntu image it stops immediately because Ubuntu is just an image of an operating system that is used as the base image for other applications. There is no process or application running in it by default.

If the image isn't running any service as is the case with Ubuntu, we can instruct Docker to run a process with the docker run command for example a sleep command with a duration of five seconds as follow:

```bash
docker run ubuntu sleep 5000
```

By running the preceding command, when the container starts it runs `sleep` command and goes into sleep for five seconds. After that, the `sleep` command exits and the container stops.

But what if we would like to execute a command on a running container? (For instance, when we run `docker run ubuntu sleep 100000` command which is a running Ubuntu container that sleeps for 100 second).

For that purpose, we can use `exec` command. Suppose we would like to see the contents of a file inside this particular container, we can use the docker `exec` command to execute a command on our docker container. For instance, running the following command:

```bash
docker exec trusting_chatelet cat /etc/hosts
```

**NOTE:** We can find the container name (`trusting_chatelet`) by using `docker ps -a` command.

By running the preceding command, Docker will print the contents of the `/etc/hosts` file on the console.