# Membuat jquery.parallel-scroll untuk Animasi Sederhana

Untuk membuat website semakin menarik, kita bisa membuat animasi sederhana untuk elemen-elemen pada laman web menggunakan jquery.parallel-scroll. Jquery.parallax-scroll adalah animasi untuk halaman web vertikal lewat scroll.

### Cara Penggunaan

Masukkan script jquery.parallax-scroll.js ke dalam halaman Anda.  Tambahkan attribute "data-parallax" pada elemen DOM yang ingin dibuatkan animasi. Lengkapi juga dengan parameter dan properti untuk animasinya.

### Parameter

* **from-scroll**: posisi scroll ketika animasi dimulai\(default:ketika elemen terlihat di laman\)
* distance: jarak scroll selama animasi berjalan\(default: tinggi laman terlihat\)

### Contoh

* Menggerakan gambar ke bawah sejauh 230 pixels ketika scroll vertikal ketika pertama terlihat di bagian bawah laman sampai ke terakhir terlihat di bagian atas laman 

```
<img src="img/paris.jpg" alt="Paris" data-parallax='{"y" : 230}'/>
```

* Perpindahan  ke kanan 650px secara 



