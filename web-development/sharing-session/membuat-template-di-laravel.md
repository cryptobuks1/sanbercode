# Membuat template di laravel

by: Andrika

Sistem Templating laravel telah dirancang sedemikian rupa yang akan memudahkan kita dalam membangun layout-layout untuk front-end sistem atau web yang kita buat apalagi pada sistem templating laravel ini telah ditanamankan pada **Blade.** Biar kita lebih “jelas” bagaimana system templating pada Laravel ini bekerja, kita akan langsung praktekkan saja.

## Layout

Persiapkan project Laravel, kemudian kita buat satu file di dalam direktori `resources/views/layouts`dengan nama`template.blade.php` dan siapkan juga direktori `resources/views/partials` untuk wadah `header.blade.php`, `sidebar.blade.php`, serta `footer.blade.php`jika semua itu sudah disiapkan, maka kalian bisa melakukan layouting, seperti code dibawah

```text
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Belajar Template Laravel</title>
    </head>
    <body>
        <div class ="navbar">
        @include('partials.header)
        </div>
        @include('partials.sidebar)

        <div class="container">
            @yield('content')
        </div>

        <div class="footer">
            @include('partials.footer')
        </div>
    </body>
</html>
```

