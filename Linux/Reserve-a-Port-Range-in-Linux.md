# How to Reserve a Port Range for a Third Party Application in CentOS/RHEL

This post provides guidance on how to reserve a specific port range on CentOS/RHEL systems when these ports are needed for a third party application. For example, one need a port range between “10000 to 15000” to be used by Application A and one need a port range between “20000 to 25000” to be used by Application B. Those ports in between “10000 to 15000 ” and ” 20000 to 25000″ are going to be exclusively reserved for Application A and B.

In CentOS/RHEL operating system side one have to reserve a range of ports needed by the third-party application, and it is important to be aware that the port range will not strictly reserve the port for a any specific application but in the application side is where one has to set the port to be used by that specific application.

To change the port range simply modify the file proc/sys/net/ipv4/ip_local_port_range and change the respective desired values.

1. Check the current port range:

    `cat /proc/sys/net/ipv4/ip_local_port_range`

    For Example:

    ```shell script
    # cat /proc/sys/net/ipv4/ip_local_port_range
    32768 61000
    ```

    or

    `# sysctl net.ipv4.ip_local_port_range`

    For Example:

    ```shell script
    # sysctl net.ipv4.ip_local_port_range
    net.ipv4.ip_local_port_range = 32768 61000
    ```

2. Modify the port range with desired values:

    `# echo 10000 25000 > /proc/sys/net/ipv4/ip_local_port_range`

    or

    `# sudo sysctl -w net.ipv4.ip_local_port_range="10000 25000"`

3. Modify /etc/sysctl.conf file
    Edit the configuration file /etc/sysctl.conf file, to make changes permanently and add the following line:

    ```shell script
    # vi /etc/sysctl.conf
    net.ipv4.ip_local_port_range = 10000 25000
    ```

    To reserve one or more specific ports out of the port range reserved under ‘ip_local_port_range” for an specific purpose, add the port to the following file:

    `/proc/sys/net/ipv4/ip_local_reserved_ports`

## Notes

### ip_local_port_range – 2 INTEGERS

Defines the local port range that is used by TCP and UDP to choose the local port. The first number is the first, the second the last local port number. If possible, it is better these numbers have different parity (one even and one odd values) The default values are 32768 and 60999 respectively.

### ip_local_reserved_ports – list of comma separated ranges.

Specify the ports which are reserved for known third-party applications. These ports will not be used by automatic port assignments (e.g. when calling connect() or bind() with port number 0). Explicit port allocation behaviour is unchanged.

The format used for both input and output is a comma separated list of ranges (e.g. “1,2-4,10-10” for ports 1, 2, 3, 4 and 10). Writing to the file will clear all previously reserved ports and update the current list with the one given in the input.

Note: ip_local_port_range and ip_local_reserved_ports settings are independent and both are considered by the kernel when determining which ports are available for automatic port assignments.

You can reserve ports which are not in the current ip_local_port_range, e.g.:

```shell script
$ cat /proc/sys/net/ipv4/ip_local_port_range
32000 60999
$ cat /proc/sys/net/ipv4/ip_local_reserved_ports
8080,9148
```

although this is redundant. However such a setting is useful if later the port range is changed to a value that will include the reserved ports.

Note: Sequential numbers will be combined by '-'.

```shell script
# echo "8080,8081,9148" > /proc/sys/net/ipv4/ip_local_reserved_ports
# cat /proc/sys/net/ipv4/ip_local_reserved_ports
8080-8081,9148
```

Reference: `https://www.thegeekdiary.com/how-to-reserve-a-port-range-for-a-third-party-application-in-centos-rhel/`

Related topic: `https://mozillazg.com/2019/05/linux-what-net.ipv4.ip_local_port_range-effect-or-mean.html`
