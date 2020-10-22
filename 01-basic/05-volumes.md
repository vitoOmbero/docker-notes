# container liftime and volumes

## Persistent Data: Data Volumes

```bash
docker pull mysql

docker image inspect mysql
# Mount and volume

docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql

docker container ls

docker container inspect mysql

docker volume ls

docker volume inspect

docker container run -d --name2 mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql

docker volume ls

docker container stop mysql

docker container stop mysql2

docker container ls

docker container ls -a

docker volume ls
# anonymous volumes auto deleted if run with --rm
# see also docker volumes prune

docker container rm mysql mysql2

docker volume ls

# named volume
docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql

docker volume ls

docker volume inspect mysql-db

docker container rm -f mysql

# reuse named volume
docker container run -d --name mysql3 -e MYSQL_ALLOW_EMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql

docker volume ls

docker container inspect mysql3

# see https://docs.docker.com/engine/reference/commandline/volume_create/
docker volume create --help

```

## Persistent Data: Bind Mounting

For runtime operations and development purposes (nowadays).

```bash
# prepare new index file first
docker container run -d --name nginx -p 80:80 -v $(pwd):/usr/share/nginx/html nginx

# the default
docker container run -d --name nginx2 -p 8080:80 nginx

# touch file and see there
docker container exec -it nginx bash
```
