# create database

<https://www.jfrog.com/confluence/display/JFROG/MySQL#MySQL-CreatingtheArtifactoryMySQLDatabase>

```shell
CREATE DATABASE artdb CHARACTER SET utf8 COLLATE utf8_bin;
CREATE USER 'artifactory'@'%' IDENTIFIED BY 'password';
GRANT ALL on artdb.* TO 'artifactory'@'%';
FLUSH PRIVILEGES;
```
