# general

* version
* info

Since v11 commands are organized by Managment Commands.

```bash
 docker run
 ...
 docker container run
```

## terms

| docker    |     os      |
| --------- | :---------: |
| image     | application |
| Container |   process   |

## container execution

```bash
docker container run --publish 80:80 nginx
```

* *...wait*

* <http://localhost>

what'd happend:

* looked in cache -- no image
* nginx image (nginx:latest by default) dowload from docker hub (by default)
* image -> container
* open host:80 (private network inside docker)
* route to container:80 from host:80

*...ctrl+c* .

```bash
docker container run --publish 80:80 --detach nginx
```

```powershell
docker stop nginx
docker container run --publish 80:80 --detach nginx
```

<http://localhost> still answers.

```bash
docker container ls
docker container stop <container-id>
docker container ls
```

Just unique container-id substring from start is enough.

```bash
docker container ls -a
```

Each run == new container.

```bash
docker container run --publish 80:80 --detach --name webhost nginx
docker container ls -a
```

* goto <http://localhost>
* back to terminal

```bash
docker container logs webhost
docker container top webhost
```

```bash
docker container ls -a
docker container rm [<container-id>, ...]
docker container rm -f [<container-id>, ...]
```

* goto <http://localhost>
* *process* was *killed*

More customized command to run:

```bash
docker container run --publish 8080:80 --name webhost -d nginx:1.11 nginx -T
```

Container is a linux process ([sheduled task](https://stackoverflow.com/questions/807506/threads-vs-processes-in-linux))

```bash
docker container run --publish 8080:80 --name webhost -d nginx:1.11 nginx -T

docker ps
docker top mongo
ps aux | grep mongo

docker stop mongo

docker ps
docker top mongo
ps aux | grep mongo
```

Each start == start container which had been run once.

```bash
docker container start webhost
```

## inspect container from outside

```bash
docker container top webhost

docker container inspect webhost

docker container stats
```

## inspect container from inside

```bash
# if not started yet
docker container run -it --name proxy nginx bash
docker container run -it --name cent7 centos:7 bash


# if is started already
docker container exec -it mysql bash
root@<id>$> apt-get update && apt-get install -y procps
root@<id>$> ps
```

Depends on entrypoint and container configuration, "exit" in shell session may shotdown the container (e.g. the 1st container citizen is a daemon).

## images

Term desribes contents of a container. There is a need to have a docker image to run a docker container.

```bash

docker pull alpine

docker image ls
```
