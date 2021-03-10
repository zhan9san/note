# rsync

Transfer single big file partially

```bash script
rsync --append 1GB user@host:/tmp/
```

With timeout

```bash script
timeout 20 rsync --append 1GB user@host:/tmp/
```
