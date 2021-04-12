# Dockerfile

```shell script
FROM busybox
CMD ["-l"]
ENTRYPOINT ["ls", "-a"]
```

ENTRYPOINT -> append
CMD -> Replace

`docker run --rm test` -> `ls -a -l`

`docker run --rm test -h` -> `ls -a -h`
