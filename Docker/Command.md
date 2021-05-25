# Command

save/scp on local

```shell script
docker image save -o /tmp/xxx.xxx image_name:tag
scp /tmp/xxx.xx user@host:/tmp/
```

load on remote

```sehll script
docker image load -i /tmp/xxx.xxx
```

Delete all local images

```bash
docker rmi $(docker images -a -q)
```

Delete all containers

```bash
docker rm -f $(docker ps -a -q)
```

Delete all volumes

```bash
docker volume rm $(docker volume ls -q)
```
