# Command

`https://benohead.com/blog/2013/07/31/mac-netstat-list-ports-programs/#:~:text=Actually%20on%20Mac%20OS%20X,can%20be%20done%20using%20%2Dptcp.&text=This%20shows%20you%20the%20listening,ll%20have%20to%20use%20sudo.`

Somehow I’ve only noticed now that netstat on Mac OS X cannot show the program name. Actually on Mac OS X, the -p parameter of netstat doesn’t mean program or process but protocol. Also there is no -t parameter but it can be done using -ptcp.

```Bash script
$ netstat -an -ptcp | grep LISTEN
tcp4       0      0  127.0.0.1.10000        *.*                    LISTEN
tcp6       0      0  *.43611                *.*                    LISTEN
tcp4       0      0  *.43611                *.*                    LISTEN
tcp46      0      0  *.80                   *.*                    LISTEN
tcp4       0      0  127.0.0.1.3306         *.*                    LISTEN
tcp4       0      0  127.0.0.1.631          *.*                    LISTEN
tcp6       0      0  ::1.631                *.*                    LISTEN
```

When checking the listening ports on my Linux machine I put netstat some pants on:

```Bash script
netstat -pant | grep LISTEN
```

I want to see the ports and the programs listening on these ports. The netstat options used mean:

```Bash script
-p: show the program name / PID owning the socket
-a: show all connections
-n: show numerical addresses
-t: show only TCP connections
```

There seems to be no way to get the same kind of info using netstat on Mac OS X. But everything is not lost. A tcp socket is just another type of file descriptor in Unix derivatives so we can use lsof to get the same info on Mac OS X:

```Bash script
$ lsof -i -P | grep -i "listen"
mysqld    31797 henribenoit   10u  IPv4 0xe1e3f49df503def7      0t0  TCP localhost:3306 (LISTEN)

This shows you the listening ports for programs running under your user name. If you want to see it for all users, you’ll have to use sudo.

```Bash script
$ sudo lsof -i -P | grep -i "listen"
```
