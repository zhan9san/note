# Command

save/scp on local

```shell script
docker image save -o /tmp/xxx.xxx image_name:tag
scp /tmp/xxx.xx user@host:/tmp/
```

load on remote

```shell script
docker image load -i /tmp/xxx.xxx
```

Remove unused images

```shell
docker image prune
```

Delete all local images

```bash
docker rmi $(docker images -a -q)
```

Delete all containers

```bash
docker rm -f $(docker ps -a -q)
```

Remove all stopped containers

```shell
docker container prune
```

Delete all volumes

```bash
docker volume rm $(docker volume ls -q)
```

Deleted 15 oldest images

```bash
docker images | tail -n 15 | docker rmi $( awk '{printf "%s:%s ", $1, $2}')
```
