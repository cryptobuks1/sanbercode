# Menambahkan SSH pada Gitlab

Jika kita membuat repository di Gitlab maka akan disediakan dua pilihan link untuk menge-clone repository tersebut yaitu "Clone with SSH" dan "Clone with HTTPS". Biasanya jika kita clone menggunakan HTTPS pada saat memberikan perintah `git clone` kita akan diminta untuk memasukkan username Gitlab dan password nya. Tidak hanya itu, kadang ketika kita melalukan push pun kita akan dimintai kembali untuk memasukkan username dan password. Bagi kebanyakan developer, hal tersebut terlalu membuat repot.

Untuk mengatasi kendala dengan menggunakan "clone with HTTPS", kita dapat menggunakan pilihan clone menggunakan SSH. Dengan menggunakan SSH, kita mendaftarkan local development \(komputer PC/laptop\) kita ke Gitlab sehingga Gitlab dapat mengenali jika ada aktivitas git dari local tanpa harus melakukan autentikasi. 

Untuk memulai ikuti langkah langkah berikut ini

## Generate SSH-Key 

* [ ] Buat folder .ssh di root directory \(untuk di windows biasanya ada di C:\Users\namaUser\) . namaUser bergantung dari nama User yang sedang anda pakai sekarang contohnya 

  ```bash
  C:Users\joetest
  ```

  Bagi anda yang memakai ubuntu, anda bisa menuju root directory dengan mengetikan perintah berikut di terminal anda  


  ```bash
  $ cd ~
  ```

  Setelah itu buatlah folder ssh dengan perintah mkdir berikut:   


  ```bash
  $ mkdir .ssh
  ```

  Maka sudah terdapat folder .ssh di C:\Users\joetest\.ssh   

* [ ] Masuk ke folder .ssh yang sudah kita buat barusan

  ```bash
  $ cd .ssh
  ```

* [ ] Ketikkan perintah seperti berikut  


  ```bash
  $ ssh-keygen.exe
  ```

  Jika anda menggunakan linux ubuntu atau MacOS cukup berikan perintah  


  ```bash
  $ ssh-keygen
  ```

* [ ] Ketika diminta untuk memasukkan password, Anda dapat mengisi atau mengosongkannya. Klik enter sampai keluar keterangan seperti berikut  


  ```bash
  $ Generating public/private rsa key pair.
  Enter file in which to save the key (/c/Users/joetest/.ssh/id_rsa): /c/Users/joetest/.ssh/
  Enter passphrase (empty for no passphrase):
  Enter same passphrase again:
  Your identification has been saved in /c/Users/joetest/.ssh/
  Your public key has been saved in /c/Users/joetest/.ssh/
  The key fingerprint is:
  SHA256:jieniOIn20935n0awtn04n002HqEIOnTIOnevHzaI5nak joetest@periwinkle
  The key's randomart image is:

   +---[RSA 2048]----+
   |*= =+.           |
   |O*=.B            |
   |+*o* +           |
   |o +o.  .         |
   | ooo  + S        |
   | .o.ooo* o       |
   |  .+o+*oo .      |
   |   .=+..         |
   |   Eo            |
   +----[SHA256]-----+

  ```

* [ ] Maka di dalam folder .ssh kini terdapat file `id_rsa` dan `id_rsa.pub` yang merupakan ssh-key dari komputer kita

  ```bash
  // di folder .ssh
  $ dir 
  id_rsa id_rsa.pub
  ```

* [ ] Copy nilai dari id\_rsa.pub dengan perintah seperti berikut

  ```bash
  // masih di folder .ssh
  $ cat id_rsa_pub
  ssh-rsa XXXXXXRANDOMXXXXXXX root@your_computer
  ```

  copy ssh-key tersebut dari "ssh-rsa"  sampai ke akhir root@your\_computer. Gunakan drag dan copy dengan cara klik kanan lalu copy atau Ctrl + C \(untuk beberapa bash/terminal:Ctrl + Shift + C\). 

## Upload SSH-key ke Gitlab

Lakukan langkah-langkah seperti berikut:

* [ ] Masuk ke Gitlab, lalu klik akun profile di sebelah kanan atas, pilih "settings"
* [ ] Pada menu sidebar terdapat menu "SSH Keys", klik menu tersebut
* [ ] Setelah diarahkan menuju halaman SSH Keys, Paste ssh-key yang sudah Anda Copy sebelumnya pada kolom isian Key. Biasanya kolom Title akan terisi secara otomatis. Untuk merubah Title hanya opsional. 
* [ ] Klik Tombol "Add key"

Setelah semua langkah berhasil maka kita sudah bisa menggunakan link "clone with SSH" jika ingin clone dari project atau repository di Gitlab.   
  




