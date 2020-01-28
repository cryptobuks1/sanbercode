# Setting Node JS + Apache

untuk setting domain agar apache dapat membaca port node js, misal port: 3000, atau 3333, maka perlu menggunakan VirtualHost

kita menggunakan proxy di apache. adapun modul apache yang perlu dipastikan aktif:

* mod\_proxy
* mod\_http
* mod\_headers
* mod\_html

1. pastikan node js sudah berjalan.. misal di port 3000, gunakan pm2 untuk memastikan agar aplikasi node js tetap berjalan meskipun kita sudah close terminal
2. Coba jalankan  `curl http://localhost:3000`
3. maka akan keluar output node js.. misal hello world dsb..

Selanjutnya adalah edit di conf apache:

```text
<VirtualHost *:80>
  ServerName sanberhost.ip-dynamic.com
  ServerAlias www.sanberhost.ip-dynamic.com
  
  #... other apache config
  
  ProxyPreserveHost On

  ProxyPass "/nodejs" "http://localhost:3000"
  ProxyPassReverse "/nodejs" "http://localhost:3000"
</VirtualHost>
```

perhatikan line 7 sampai 10.. code ini mengandung konfigurasi :

1. ketika mengakses domain : http://sanberhost.ip-dynamic.com/nodejs
2. maka apache akan mengeluarkan output dari localhost:3000

pastikan anda sudah restart apache agar perubahan diload..

