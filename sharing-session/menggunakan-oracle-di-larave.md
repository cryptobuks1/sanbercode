# Menggunakan Oracle di Laravel

#### 08/Mei/2018 \(By: Andrika\)

### Step 1

Untuk mengintegrasikan laravel dengan oracle, saran saya menggunakan laravel versi 5.4 atau 5.3, karena sedikit sekali permasalahan yang kalian akan jumpai nantinya ketika mengistall package dari Mas Yajra \( [https://yajrabox.com/ ](https://yajrabox.com/)\). Hal yang harus kalian lakukan adalah mempersiapkan tools yang dibutuhkan pastinya, cek dibawah \*pastikan kalian memnpunyai project laravel :

1. Oracle : [http://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html](http://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html)
2. Untuk lebih mengoptimalkan oracle Download Sql Developer : [http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html)

Keterangan:

* untuk memudahkan dalam mengisntallnya coba tonton video, cek link ini [https://www.youtube.com/watch?v=Fr4pPlZnbFI&t=384s](https://www.youtube.com/watch?v=Fr4pPlZnbFI&t=384s)

### Step 2

Sebelum mencoba, setting terlebih dahulu xampp untuk memudahkan menjalankan package yajra di project kalian:

* buka php.ini di folder xampp atau bisa mengikuti gambar dibawah

![](/assets/import.png)

* kemudian cari extension=php\_\_oci8\_\_12c.dll kemudian hapus ; \(titik koma\)

![](/assets/php_ini.png)

Jika sudah dilakukan semua \*saran yang diatas, kalian bisa langsung mengaplikasikan oracle pada laravel dengan  menggunakan package yajra \([https://github.com/yajra/laravel-oci8](https://github.com/yajra/laravel-oci8)\).

