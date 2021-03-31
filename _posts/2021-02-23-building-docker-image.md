---
layout: post
title: "Building Docker Image"
date: 2021-02-23
tags: [docker, python, github, devops, dockerfile]
---

We can find so many Docker images in [Docker Hub](https://hub.docker.com/) site. However, sometimes we cannot find a service that we want to use as part of our application or our team decided that the application will be dockerizing for ease of shipping and deployment.

## Preparing

Now, let's containerize a simple Web application that I have built using the Python Flask framework. The repository can be found in this link: [https://github.com/WisnuAnggoro/simple-flask-web](https://github.com/WisnuAnggoro/simple-flask-web).

To create a Docker image, simply start by thinking what we might do if we want to deploy the application manually. First thing first, we setup an operating system, like `Ubuntu`, then update the source repositories using the `apt-get update` command, then install `python` and the dependencies, then copy over the source code of our application to a location like `/opt` and then finally run the Web server using the `Flask` command.

## Creating `Dockerfile`

To build Docker image, we have to write a text file named `Dockerfile`. The file contains a set of `instruction` and `argument` format.

In `Dockerfile`, everything on the left in capital leters is an instruction, for instance: `FROM`, `RUN`, and `COPY`. Each of these instruction performs a specific action when creating the image. Everything on the right is an `argument` to those instructions.

Based on the previous discussion about setting up things when we deploy application manually, we can transfer it to `Dockerfile` as follow:

```
# Setup Ubuntu
FROM ubuntu

# Update Ubuntu Source Repositories
RUN apt-get update

# Install Python3 and Python3-Pip
RUN apt-get install -y python3 python3-pip

# Install Python Dependencies that is used in the code
COPY requirements.txt /tmp/requirements.txt
RUN python3 -m pip install -r /tmp/requirements.txt

# Run the web server
COPY app.py /opt/app.py
ENTRYPOINT FLASK_APP=/opt/app.py flask run --host=0.0.0.0
```

Here's the explanation of the content of `Dockerfile` we have written previously:

* The first line is `FROM ubuntu` which defines what the base OS should be used for this container. All Docker images must be based of another image, either an OS or another image that was created before. We can find official releases of all operating systems on Docker Hub. (**Note that all Docker files must start with a from instruction**).
* The `RUN` instruction instructs Docker to run a particular command on those base images, which `bash` command in Ubuntu.
* The `COPY` instruction copies files from the local system onto the Docker image. In this case, we copy `requirements.txt` file from local system to the image base OS so that it can install all dependencies stated in the `requirements.txt` file from the image.
* Finally, `ENTRYPOINT` instruction allows us to specify a command that will be run when the image is run as a container.

## Building An Image

After completing the `Dockerfile`, we can build an image by running the following command:

```bash
docker build . -f Dockerfile -t simple-flask-web
```

**NOTE:** `-f` option is optional in case we create `Dockerfile` with different name and `-t` option is `tag` which gives a name and tag to built image.

When Docker builds an image, it create this in a layered architecture. Each line of instruction creates a new layer in the Docker image with just the changes from the previous layer. It is also reflected in the size. To find out the size of each layer, we can `docker history` followed by the image name as follow:

```bash
docker history simple-flask-web:latest 
```

The output will be similar like follows:

```bash
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
cea1c9b31a0c        7 seconds ago       /bin/sh -c #(nop)  ENTRYPOINT ["/bin/sh" "-c…   0B                  
63aebe23c639        9 seconds ago       /bin/sh -c #(nop) COPY file:d9405d0b92ad5bd0…   325B                
da157dc5d2bb        10 seconds ago      /bin/sh -c python3 -m pip install -r /tmp/re…   4.38MB              
3b4201da9273        14 seconds ago      /bin/sh -c #(nop) COPY file:2f57c6de4d15d496…   5B                  
d5d4f906fdd3        16 seconds ago      /bin/sh -c apt-get install -y python3 python…   314MB               
a582710508ab        59 seconds ago      /bin/sh -c apt-get update                       27.1MB              
d70eaf7277ea        4 months ago        /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B                  
<missing>           4 months ago        /bin/sh -c mkdir -p /run/systemd && echo 'do…   7B                  
<missing>           4 months ago        /bin/sh -c [ -z "$(apt-get indextargets)" ]     0B                  
<missing>           4 months ago        /bin/sh -c set -xe   && echo '#!/bin/sh' > /…   811B                
<missing>           4 months ago        /bin/sh -c #(nop) ADD file:435d9776fdd3a1834…   72.9MB
```

As we can see in the last line, that is the Ubuntu layer which size is `72.9MB` and with reposities update size is `27.1MB`. Also, for `python` and dependencies installation, the size is `314MB`. In total, the image size is `419MB` which can be found using `docker images` command.

## Pushing The Image To DockerHub 

When we have our image ready, we can push it to DockerHub so it can be used by others. To do that, we can run `docker push` command followed by the image name.

However, we have to rebuild the docker image and tag the docker name with the DockerHub account. My DockerHub account is `wisnuanggoro` so I will tag the image with my account as follows:

```bash
docker build . -f Dockerfile -t wisnuanggoro/simple-flask-web
```

After that, we can run `docker push` command followed by image name. I will push the previous built image to my DockerHub repository with the following command:

```bash
docker push wisnuanggoro/simple-flask-web
```

NOTE: If you get the error like this `denied: requested access to the resource is denied`, you must login first using `docker login` command.

---

Source links:<br />
[Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)<br />
[Docker Credentials Store](https://docs.docker.com/engine/reference/commandline/login/#credentials-store)