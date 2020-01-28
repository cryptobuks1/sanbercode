---
description: 'pada tutorial kali ini, diasumsikan sudah pada install docker ya..'
---

# Setting new centos 7 container

## How to run CentOS with systemd inside a Docker container

1. **Pull centos image** Saat ini centos image ketika di pull, maka akan mengambil versi yang terbaru yaitu centos 8, yang mana saat ini masih terbilang baru dan banyak library yang belum compatible.. maka kita akan gunakan image spesifik **centos:7** 
2. Set up a docker file like the one below

```
$ vi mydockerfile
```

setelah membuat file baru untuk setting docker, edit file dengan menambahkan kode berikut:



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
```

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}



