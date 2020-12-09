# Shinobi

Reference: `https://shinobi.video/docs/start`

Install Docker

```shell script
sudo yum install -y yum-utils && sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo  && sudo yum install -y docker-ce docker-ce-cli containerd.io
```

Start Docker

```shell script
sudo systemctl start docker
```

Install Docker Compose

```shell script
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

Install Shinobi

```shell script
curl -o  shinobi-docker.sh https://gitlab.com/Shinobi-Systems/Shinobi-Installer/raw/master/shinobi-docker.sh

sudo sh -x shinobi-docker.sh
```

URL: `http://172.28.27.175:8080/super`

The generated `docker-compose.yml` is as below

```shell script
version: "3"
services:
    shinobi:
        image: shinobisystems/shinobi:dev
        container_name: Shinobi
        environment:
           - PLUGIN_KEYS={"Tensorflow":"a54f1551092a1386932fee8701832"}
           - SSL_ENABLED=false
        volumes:
           - /root/Shinobi/config:/config
           - /root/Shinobi/customAutoLoad:/home/Shinobi/libs/customAutoLoad
           - /root/Shinobi/database:/var/lib/mysql
           - /root/Shinobi/videos:/home/Shinobi/videos
           - /root/Shinobi/plugins:/home/Shinobi/plugins
           - /dev/shm/Shinobi/streams:/dev/shm/streams
           - /etc/localtime:/etc/localtime:ro
        ports:
           - 8080:8080
        restart: unless-stopped

    shinobiplugintensorflow:
        image: shinobisystems/shinobi-tensorflow:latest
        container_name: shinobi-tensorflow
        environment:
          - PLUGIN_KEY=a54f1551092a1386932fee8701832
          - PLUGIN_HOST=Shinobi
        volumes:
          - /root/Shinobi/docker-plugins/tensorflow:/config
        restart: unless-stopped
```
