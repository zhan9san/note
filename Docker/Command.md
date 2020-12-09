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
