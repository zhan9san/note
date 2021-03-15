# Control Docker with systemd

`https://docs.docker.com/config/daemon/systemd/`

1. Create a systemd drop-in directory for the docker service:

    ```bash
    sudo mkdir -p /etc/systemd/system/docker.service.d
    ```

2. Create a file named `/etc/systemd/system/docker.service.d/http-proxy.conf` that adds the `HTTP_PROXY` environment variable:

    ```bash
    [Service]
    Environment="HTTP_PROXY=http://proxy.example.com:80"
    Environment="HTTPS_PROXY=https://proxy.example.com:443"
    Environment="NO_PROXY=localhost,127.0.0.1,docker-registry.example.com,.corp"
    ```

3. Flush changes and restart Docker

    ```bash
    sudo systemctl daemon-reload
    sudo systemctl restart docker
    ```

4. Verify that the configuration has been loaded and matches the changes you made, for example:

    ```bash
    $ sudo systemctl show --property=Environment docker
    Environment=HTTP_PROXY=http://proxy.example.com:80 HTTPS_PROXY=https://proxy.example.com:443 NO_PROXY=localhost,127.0.0.1,docker-registry.example.com,.corp
    ```
