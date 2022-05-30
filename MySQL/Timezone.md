# Timezone

<https://stackoverflow.com/questions/19903610/how-to-set-permanent-default-timezone-in-mysql-server>

```shell
[mysqld]
default-time-zone=+08:00
```

<https://dev.mysql.com/doc/refman/5.7/en/time-zone-support.html>

```sql
SELECT @@GLOBAL.time_zone, @@SESSION.time_zone;
```

```sql
SELECT NOW();
```

Changing the Time Zone in MySQL

```sql
SET GLOBAL time_zone = ‘-6:00’;
```
