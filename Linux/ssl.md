# ssl

<https://sslhow.com/how-to-check-ssl-certificate>

```shell
SERVER_NAME=baidu.com
openssl s_client -servername ${SERVER_NAME} -connect ${SERVER_NAME}:443 2>/dev/null | openssl x509 -noout -dates
```
