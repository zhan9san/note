# Pip issue

[UnicodeEncodeError: 'ascii' codec can't encode character '\xe9' in position 117: ordinal not in range(128)](https://github.com/pypa/pip/issues/10219)

Reproduce

```Dockerfile
FROM centos:7

LABEL maintainer="Amin Vakil <info@aminvakil.com>"

ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN yum -y install python3-pip sudo && yum clean all

RUN pip3 install --upgrade pip && pip3 install ansible

VOLUME ["/sys/fs/cgroup"]

CMD ["/usr/sbin/init"]
```

Add environments in a centos 7 dockerfile

```Dockerfile
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
```
