# How to Disable IPv6 on CentOS 7

https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-disable-ipv6-network-on-centos-7/

Disable IPv6 stack on all network interfaces.
Disable IPv6 by default on all network interfaces.

```bash
sysctl -w net.ipv6.conf.all.disable_ipv6=1
sysctl -w net.ipv6.conf.default.disable_ipv6=1
```

Update file

```bash
cat > /usr/lib/sysctl.d/60-disable-ipv6.conf << EOF
net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
net.ipv6.conf.lo.disable_ipv6=1
EOF
```
