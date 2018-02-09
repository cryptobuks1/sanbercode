## Menggunakan _Sweet Alert_ pada _Laravel_

**9 Februari 2017 by Andrika**

Kalian pasti pernah menggunakan aplikasi? khususnya \(_Website_\). Pernah tidak kepikiran untuk membuat feedback sebagai informasi yang akan didapatkan oleh user ketika user melakukan aktivitas di aplikasi \(_website_\)-nya ?

Jika tidak, ayo mulai memikirkannya, dan belajar membuatnya

### _Sweet Alert_

Yup, kalian pasti sudah tau kan apa itu_ Sweet Alert_ ? Oke, Saya Jelaskan. \_Sweet  Alert \_adalah sebuah alert yang** **sudah di design menarik dan mudah untuk digunakan. Referensi: [packagist.org](https://packagist.org/packages/uxweb/sweet-alert) \(terimakasih banyak\).

Langsung aja kali ya"

Langkah pertama siapin [Composer ](https://getcomposer.org)biar bisa bikin _Command Line._

> `composer require uxweb/sweet-alert`

Nah sambil nunggu hasil command line yang diatas \(lumyan lama\), mending buka folder config/app.php terus copas dah tuh code yg di bawah ke providers array

> `UxWeb\SweetAlert\SweetAlertServiceProvider::class,`

Oh iya satu lagi code yang mesti di copas, tapi beda tempat ^^ code yg bawah simpen di _facade alias_

> `UxWeb\SweetAlert\SweetAlertServiceProvider::class,`

Oke jangan lupa download css dan js [disini](https://drive.google.com/file/d/11ollFhAQEms2BfU1R68xCCOuIzuFdfjN/view?usp=sharing), teru kalian simpen dah tuh code dibawah itu  ke template kalian.

> `<link rel="stylesheet" href="{{ url('sweetalert/sweetalert.min.css') }}">`
>
> `<script src="{{ url('sweetalert/sweetalert.min.js') }}"></script>`





