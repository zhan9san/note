# Register a service

`https://www.consul.io/commands/services/register`

Run the following commands on Consul server

```bash script
$ cat web.json 
{
  "Service": {
    "Name": "web",
    "Address": "172.28.24.101",
    "Port": 80
  }
}

$ consul services register web.json
```
