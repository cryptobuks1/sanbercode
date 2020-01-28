---
description: 'pada tutorial kali ini, diasumsikan sudah pada install docker ya..'
---

# Setting new centos 7 container

## How to run CentOS with systemd inside a Docker container

* **Pull centos image** Saat ini centos image ketika di pull, maka akan mengambil versi yang terbaru yaitu centos 8, yang mana saat ini masih terbilang baru dan banyak library yang belum compatible.. maka kita akan gunakan image spesifik **centos:7** 
* Set up a docker file like the one below

```
$ vi mydockerfile
```

* setelah membuat file baru untuk setting docker, edit file dengan menambahkan kode berikut:

```
FROM centos:7
MAINTAINER "Yourname" <youremail@address.com>
ENV container docker
RUN yum -y update; yum clean all
RUN yum -y install systemd; yum clean all; \
(cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
EXPOSE 9080:80
EXPOSE 9443:443
EXPOSE 9022:22
```

* Build it - `docker build --rm -t centos7-systemd - < mydockerfile`
* Run a container with `docker run --privileged -ti -e container=docker -v /sys/fs/cgroup:/sys/fs/cgroup centos7-systemd /usr/sbin/init`
* You should have systemd in your container

