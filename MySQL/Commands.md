# Commands

Get server_id

```bash script
SELECT @@server_id
```

As `@@` points to global-defined variables (not like single `@` which is for session-defined variables)

```bash script
SHOW VARIABLES LIKE 'server_id';
```

## log-bin

`https://www.cnblogs.com/chuanzhang053/p/9335924.html`

If `log-bin` is set, `server-id` has to be set as well in MySQL 5.7

```bash script
server-id=11 
log-bin = mysql-bin
```

Get log-bin related configuration

```bash script
show variables where variable_name in ('log_bin','log_bin_basename','log_bin_index');
```

Location of log-bin

```bash script
ls -ltr mysql-bin.*
```
