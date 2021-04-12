# Docker Network

默认的桥接网络无法通过容器名访问，但是自定义网络可以通过名称访问

network connect是给容器分配处于待连接的网络子网一个额外的网卡

```shell script
docker network connect --help

Usage:	docker network connect [OPTIONS] NETWORK CONTAINER

Connect a container to a network

Options:
      --alias strings           Add network-scoped alias for the container
      --driver-opt strings      driver options for the network
      --ip string               IPv4 address (e.g., 172.30.100.104)
      --ip6 string              IPv6 address (e.g., 2001:db8::33)
      --link list               Add link to another container
      --link-local-ip strings   Add a link-local address for the container
```
