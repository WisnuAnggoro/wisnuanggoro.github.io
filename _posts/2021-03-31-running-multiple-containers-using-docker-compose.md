---
layout: post
title: "Running Multiple Containers Using Docker Compose"
date: 2021-03-31
tags: [docker, compose, docker-compose, container, devops]
---

`Docker Compose` is used for running multiple containers and each of the containers run in isolation but can interact with each other when required. `Docker Compose` file are written in a scripting language called `YAML`.

We will use `example-voting-app` that we can find in `dockersamples` Github repository: [https://github.com/dockersamples/example-voting-app](https://github.com/dockersamples/example-voting-app)

After cloning the repository, we have to build three applications since they are not available in Docker Hub: `vote`, `worker`, and `result`. To build them, run these three commands one by one:

```bash
docker build ./vote -t voting-app
docker build ./worker -t worker-app
docker build ./result -t result-app
```

After building those three applications, we can create a new `docker-compose.yml` file that containing the following script:

```yaml
version: "3"
services:
    redis:
        image: redis
    
    db:
        image: postgres:9.4
        environment:
            POSTGRES_USER: postgres
            POSTGRES_PASSWORD: postgres

    vote:
        image: voting-app
        ports:
            - 5000:80
    
    worker:
        image: worker-app
    
    result:
        image: result-app
        ports:
            - 5001:80
```

We can then run `docker-compose up` command to run multiple containers.

To run `voting-app` we can go to `localhost:5000` and to run `result-app` we can go to `localhost:5001".

---

Source links:<br />
[Overview of Docker Compose](https://docs.docker.com/compose/)