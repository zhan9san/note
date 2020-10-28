# Generic LDFLAGS variable set

Just export LDFLAGS before installing it, here is generic command which shall work for OS X (and I believe any LINUX system which has same error):

```Bash
LDFLAGS=`echo $(pg_config --ldflags)` pip install psycopg2
```
