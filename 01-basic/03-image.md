# docker images

## layers
- Image consits of layers
- Each layer represents changes to the execution environment for processes
- they are storaged with COW-optimization (commits)
- real data (e.g. file changes) may absent in commit (just metadata)
- container uses the top layer

```bash
docker image ls

docker image history mysql

docker image inspect nginx
```

## tags

Layers have id-s, images have id-s. Identification for humans:

```text
<user>/<repo>:<tag>
```

Official (at Docker Hub) repositories are named with repo name simply.
Ther is a normal situation to have several images with one id and different tags.
If it is needed to create a new repo with name *new_repo*:

```bash
docker image tag -- help

docker image ls

docker image tag nginx new_repo/nginx

docker image push new_repo/nginx

docker image push new_repo/nginx new_repo/nginx:testing
```

Do *docker login* before, of cause.

## clean space

```bash
diocker system --help

docker system df

docker image prune

docker system prune
```