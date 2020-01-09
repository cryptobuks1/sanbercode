# Recommended tutorial for setting centos 8

## Setting Let's Encrypt HTTPS + Apache 2.4

{% embed url="https://linuxize.com/post/secure-apache-with-let-s-encrypt-on-centos-8/" %}

## Install PHP-mbstring 

{% embed url="https://linuxconfig.org/install-php-mbstring-on-redhat-8" %}

## install php-dom and php-zip

```text
yum install php-xml
```

```text
yum install php-pecl-zip
```

## Install MySQL

{% embed url="https://linuxize.com/post/how-to-install-mysql-on-centos-8/" %}

## Install phpMyAdmin

{% embed url="https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-phpmyadmin-on-rhel-8.html" %}

## Ubah Direktori Default Apache 2.4



Untuk mengubah DocumentRoot Apache, cukup atur di virtualhost dan ditambahkan di config httpd.. biasanya akan ada error forbidden.. hal ini dikarenakan blocking oleh Selinux \(sistem keamanan di linux\). untuk mengatasi hal ini, Selinux perlu diset agar tidak terlalu ketat pengamanannya:

```text
getenforce
```

if the result is "Enforcing"

temporally change it to permissive

```text
setenforce 0
```

