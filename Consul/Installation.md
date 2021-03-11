# Consul

## Installation

```bash script
sudo yum install wget unzip -y
wget https://releases.hashicorp.com/consul/1.9.4/consul_1.9.4_linux_amd64.zip
unzip consul_1.9.4_linux_amd64.zip
```

```bash script

./consul agent -server -bootstrap-expect 3 -bind=172.28.24.98 -client=0.0.0.0 -data-dir=./data -node=consul1 -ui
./consul agent -server -bootstrap-expect 3 -bind=172.28.24.97 -client=0.0.0.0 -data-dir=./data -node=consul2 -ui -join 172.28.24.98
./consul agent -server -bootstrap-expect 3 -bind=172.28.24.100 -client=0.0.0.0 -data-dir=./data -node=consul3 -ui -join 172.28.24.98

./consul agent -bind 172.28.24.101 -client 172.28.24.101 -data-dir=./data -node=consul-client-1 -join 172.28.24.98
./consul agent -bind 172.28.24.103 -client 172.28.24.103 -data-dir=./data -node=consul-client-2 -join 172.28.24.98
```

## Commands

```bash script
./consul members

./consul operator raft list-peers
```

## Outage

If one server is down, there is no need to add `join x.x.x.x` explictly at the end of command.
