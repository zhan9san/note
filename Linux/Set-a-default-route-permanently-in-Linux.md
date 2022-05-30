# How to set a default route permanently in Linux

https://www.xmodulo.com/how-to-set-default-route-in-linux.html

https://x8t4.com/how-to-permanently-add-a-static-route-in-linux/

https://www.vagrantup.com/docs/provisioning/shell

## Set a Default Route Permanently on CentOS, Fedora or RHEL

On a RedHat-based system, you can explicitly declare the default route using DEFROUTE: yes. In addition, you should add DEFROUTE: no to every network interface that is not used as the default route.

```bash
$ sudo vi /etc/sysconfig/network-scripts/ifcfg-eth0
DEFROUTE=yes
```

```bash
$ sudo vi /etc/sysconfig/network-scripts/ifcfg-eth1
DEFROUTE=no
```
