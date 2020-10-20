# docker networks

## option -p for Container Run command

... -p HOST:CONTAINER ...

May be used for dev/testing only.

## because

- each container connects to provate virtual network bridge
- each network routs throught NAT firewall on host
- containers talk w/o -p
- you create a new virtual network for each logic "bundle" of contaners serving one app.

## port?

```bash
docker container port webhost

docker container inspect --format '{{ .NetworkSettings.IPAddress }}' webhost

# compare with e.g. ifconfig en0
```

## network?

```bash

# 3 defaults: bridge (when use pure -p), host, none
docker netwok ls

docker network inspect bridge

docker network create my_app_net

# --help everywhere
docker network create --help
docker network --help

docker network connect <id-1> <id-2>

# install command completion scripts for host docker
docker container inspect [TAB COMPLETION]

docker container disconnect [TAB COMPLETION]
```

## dns?

No by default. Just use names.

```bash
docker container run -d --name named1 --network my_app_net nginx:alpine

docker container run -d --name named2 --network my_app_net nginx:alpine

docker container exec -it named1 ping named2

docker container exec -it named2 ping named1

docker network ls
```

BTW, *container run* has --link option.

Either, define network alias

```bash
docker network connect --alias search my-app-net app1
docker network connect --alias search my-app-net app2

docker network inspect my-app-net

docker container run -it --network my-app-net  alpine nslookup search
```
