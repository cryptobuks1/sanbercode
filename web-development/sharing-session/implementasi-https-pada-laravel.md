---
description: >-
  Halaman ini berisi panduan bagaimana agar setiap orang yang mengunjungi web
  laravel kita, secara otomatis mengakses ke https://
---

# Implementasi HTTPS pada laravel

1. Pastikan domain di server sudah dipasang SSL \(https\). Biasanya di server hosting sudah disediakan SSL gratis =&gt; **let's encrypt**
2. Jika sudah terpasang, coba akses domain gunakan https, jika bisa maka SSL sudah terpasang, jika belum, coba kontak support dari vendor server untuk membantu pemasangan SSL.
3. Pertanyaannya adalah, bagaimana agar setiap pengunjung yang mengakses web, meskipun tidak mengetik https, tapi di-force agar gunakan https
4. jawabannya adalah via **middleware.** buat middleware baru sebagai berikut:

```php
<?php
namespace App\Http\Middleware; // lokasi file HttpsProtocol.php ada di dalam folder middleware
use Closure; 
use Illuminate\Support\Facades\App;

class HttpsProtocol {

    public function handle($request, Closure $next)
    {
            if (!$request->secure() && App::environment() === 'production') {
                return redirect()->secure($request->getRequestUri());
            }
    
            return $next($request); 
    }
}
```

Selanjutnya, buka **kernel.php**, pasang middleware HttpsProtocol yang sudah dibuat di middleware web:

```text
protected $middlewareGroups = [
        'web' => [
            \App\Http\Middleware\EncryptCookies::class,
            \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
            \Illuminate\Session\Middleware\StartSession::class,
            // \Illuminate\Session\Middleware\AuthenticateSession::class,
            \Illuminate\View\Middleware\ShareErrorsFromSession::class,
            \App\Http\Middleware\VerifyCsrfToken::class,
            \Illuminate\Routing\Middleware\SubstituteBindings::class,
            \App\Http\Middleware\HttpsProtocol::class, // *tambahkan baris ini*
        ],

        'api' => [
            'throttle:60,1',
            'bindings',
        ],
];
```

Langkah terakhir, ubah APP\_ENV=**production** di .env server 

=== end ===

setiap pengunjung mengakses route web Anda, pengunjung akan secara otomatis di redirect menggunakan https://  
  


