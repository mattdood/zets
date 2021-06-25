---
path: '/2021/6/formalizing-my-docker-notes-20210624212529'
title: 'formalizing my docker notes'
date: '20210624212529'
category: 'docker'
tags: ['docker']
---

# formalizing my docker notes
I'm finding that I would like a centralized place for my notes on using Docker.
My plan moving forward is to migrate most of my local development to docker
containers to help with dependency management on anything that doesn't support
a Python venv.

## Basics
Docker containers run on **container images**, the container's isolated filesystem
withe verything needed to run an application (dependencies, configs, scripts, etc.).
* Containers should do one thing and do it well.

### Flags
Below are some flags that I use. Typically I'll combine a few of them (ex: `up --build -d`).

* `--build` builds the container
* `-d` flag runs in detached mode (no output)
* `-t` a name tag for our image (human-readable)
* `-p` map to ports
* `-dp` detached running and map ports

### Commands
Below are some general and useful commands that I use. They usually have aliases
available in my `.bashrc`.

* `docker build -t <name> <some directory>` builds a container image with a name, implicitly calls the Dockerfile
* `docker ps` shows currently running containers
* `docker system prune -a` prunes all containers, stopped or not (alias is `docker-nuke`)
* `docker container prune --force --filter '\''until=$(date +"%Y-%m-%dT%H:%M:%S" --date="-7 days")'` removes any containers older than 15 days
* `docker ps -a --format "table {{.ID}}\t{{.Image}}\t{{.Command}}\t{{.CreatedAt}}\t{{.Status}}"` lists all containers in a table format
* `docker rm -f <container id>` this will remove and stop the container with a single command
    * this takes place of doing a `docker stop <container id> && docker rm <container id>`
* `docker tag <image> mattdood/<image>` retags an image with my username and the image
* `docker push mattdood/<image>` pushes my images to a remote docker repo
* `docker volume inspect <volume name>` inspects information about a volume

#### Example workflow
An oversimplified example of a local development environment.

1. Create a `Dockerfile`
1. Build the image
1. Run the container in detached mode and map to ports

```bash
# Dockerfile created

docker build -t <some container> <some dir (ex: '.')>

docker run -dp 3000:3000 <some container>

# push to a repo
docker push mattdood/<some-registry>

# pull from a repo
docker run -dp port:port mattdood/<some-registry>
```

### Container volumes
Volumes are persistent data storage. This allows us to have persistent access
to files and storage while we bring up and take down containers/change images.

This workflow is especially necessary when handling databases that are managed
by the Docker containers (like SQLite).

Volume workflow:
1. Create a volume using `docker volume create`
    * `docker volume create <some-volume>`
1. Stop the running container
1. Rerun the container and attach the volume
    * `docker run -dp port:port -v some-volume:/some/path <some-image>`

Inspecting a volume:
```bash
docker volume inspect todo-db

[
    {
        "CreatedAt": "2021-06-24T22:33:12-07:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/todo-db/_data",
        "Name": "todo-db",
        "Options": {},
        "Scope": "local"
    }
]
```

### Network connections
In general, if two containers are on the same network they can talk to each other.

Example creating a network and database container:
```bash

docker network create <some-network>

docker run -d \
    --network <some-network> --network-alias mysql \
    -v mysql-data:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=secret \
    -e MYSQL_DATABASE=<some-db> \
    mysql:5.7

```

Example inspecting the IP of the container:
```bash

docker run -it --network todo-app nicolaka/netshoot

dig mysql # inspects the IP

    ; <<>> DiG 9.14.1 <<>> mysql
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 32162
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

    ;; QUESTION SECTION:
    ;mysql.             IN  A

    ;; ANSWER SECTION:
    mysql.          600 IN  A   172.23.0.2

    ;; Query time: 0 msec
    ;; SERVER: 127.0.0.11#53(127.0.0.11)
    ;; WHEN: Tue Oct 01 23:47:24 UTC 2019
    ;; MSG SIZE  rcvd: 44
```

## Docker compose
Working with `docker-compose` removes a significant amount of the command overhead
that we have when creating these containers and building them.


### Structure of a `docker-compose` file


Example docker compose file from a tutorial application:
```
# docker-compose.yml
version: "3.7"

services:
  app:
    image: node:12-alpine
    command: sh-c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  mysql:
    image: mysql:5.7
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:
```

