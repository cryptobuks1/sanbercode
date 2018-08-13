# Membuat Middleware Sendiri

2 Maret 2018

## Membuat Middleware Sendiri

#### studi kasus : middleware Admin

### oleh : Bang Fady \(@fady-ni\)

Assalaamu'alaykum wr wb...

Kawan-kawan coder sekalian pasti pernah menggunakan make:auth untuk membuat fitur login kan? Fitur ini bisa dibilang sudah pasti dibutuhkan dalam membuat sebuah web yang dinamis dan dengan Laravel kita cukup mewujudkannya lewat command `make:auth`. Command ini menyediakan perangkat-perangkat yang kita butuhkan untuk membedakan 2 jenis user : non-logged-in user \(visitor\) dan logged-in user \(member\). Tapi, bagaimana bila kita butuh 3 jenis user : **visitor**, **member**, dan **admin** ? Nah, kali ini abang akan membagikan cara untuk mewujudkannya menggunakan middleware...

Sebelum lanjut ke kasus admin, sebetulnya apa sih **middleware** itu? [laravel.id](http://id-laravel.com/post/middleware-manfaat-dan-penggunaannya) menyebutkan bahwa middleware adalah _sebutan untuk perangkat lunak yang berperan sebagai “penengah” antara sebuah aplikasi dengan aplikasi lain untuk mempermudah proses integrasi antara aplikasi-aplikasi tersebut_. Abang pribadi suka menganalogikan middleware ini seperti **satpam**. Pak satpam bertugas untuk mengecek orang-orang \(**request**\) yang datang sebelum masuk ke suatu tempat \(**controller**\). Kalau sesuai kriteria, pak satpam mempersilahkan orang tersebut masuk. Tapi kalau tidak, dia akan memberikan \_treatment \_tertentu kepada orang tersebut.

Sebetulnya, kita sudah biasa loh menggunakan middleware. Saat membuat login dengan `make:auth`, kita juga diberikan sebuah middleware bernama _Authenticate_. selain itu, di file berikut juga akan muncul tambahan kode ini :

```php
//routes/web.php

Route::get('/home', 'HomeController@index');


//app/Http/Controllers/HomeController

public function __construct() {

    $this->middleware('auth');

}
```

Dari sana bisa dilihat bahwa ketika kita meminta untuk masuk ke`/home`, middleware Authenticate akan dipanggil. Authenticate bertugas mengecek apakah request ini sudah tercatat login atau belum. Bila sudah login, maka akan memanggil fungsi `index`di `HomeController`. tapi kalau belum, maka akan diarahkan ke halaman login. Sederhana kan?

Oke, sekarang kita masuk ke kasus membuat middleware untuk pengecekan admin. Tahapannya :

* [x] Menambahkan kolom is\_admin bertipe boolean di tabel users

kolom ini berfungsi untuk menandakan apakah user tersebut adalah seorang admin atau bukan. buat migration baru dan masukkan kode berikut di dalamnya

```php
Schema::table('users', function($table) {

    $table->boolean('is_admin')->default(0); //defaultnya bukan admin

});
```

* [x] membuat middleware Admin

buat middleware dengan menggunakan command `php artisan make:middleware Admin` . Command ini memberikan sebuah kelas Middleware bernama `Admin`di folder `app/Http/Middleware`.

* [x] buat fungsi `isAdmin()` di model User.

selanjutnya, kita perlu membuat fungsi `isAdmin()` untuk mengecek apakah sebuah user adalah seorang admin atau bukan. fungsi ini memberikan nilai `true`bila user adalah seorang admin dan nilai `false`bila bukan. Buka model User dan tambahkan ke dalamnya

```php
// app/User.php

public function isAdmin()
{
    return $this->is_admin;
}
```

* [x] tambahkan pengecekan status admin di middleware Admin

Pengecekan dilakukan di dalam fungsi `handle`dari middleware. Ubah isi fungsi tersebut dengan kode berikut

```php
//cek apakah user sudah login dan dia termasuk admin atau bukan

if (Auth::check() && Auth::user()->isAdmin())
{

    return $next($request);

}

return redirect('welcome');
```

Di sini, user dicek apakah dia sudah login dan apakah dia termasuk admin atau bukan. Bila termasuk admin, maka diantarkan ke proses berikutnya. Tapi bila selainnya, maka akan diantarkan ke route welcome.

yeaay... middleware kita sudah jadi... apa bisa langsung digunakan? belum, masih ada tahap di bawah ini.

* [x] daftarkan Middleware ke Kernel.php

Untuk bisa digunakan, kita harus mendaftarkan middleware kita terlebih dahulu di file `app/Http/Kernel.php` . Kita tinggal cantumkan saja middleware baru kita di property `$routeMiddleware` seperti ini

```php
protected $routeMiddleware = [

    //...

    'admin' => \App\Http\Middleware\Admin::class,

];
```

* [x] panggil middleware dari route atau controller yang diinginkan

Terakhir, kita tinggal terapkan pengecekan ini untuk route atau controller yang kita inginkan. Penerapan di route cukup dengan menambahkan fungsi middleware seperti ini :

```php
Route::get('/admin/dashboard', function() {

    view('admin.home');

})->middleware('admin'); //ini penggunaan middleware
```

sedangkan penggunaan di controller adalah dengan memanggilnya di fungsi constructor seperti yang terdapat di file `HomeController`

```php
//app/Http/Controllers/Controller-Anda

public function __construct()
{

    $this->middleware('auth');

}
```

well, that's all folks... cukup 6 tahapan untuk bisa menerapkan pengecekan request ini. mudah kan?

Referensi :

[http://id-laravel.com/post/middleware-manfaat-dan-penggunaannya](http://id-laravel.com/post/middleware-manfaat-dan-penggunaannya)

[https://laravel.com/docs/5.5/middleware](https://laravel.com/docs/5.5/middleware)

