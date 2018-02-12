# Manipulasi Tanggal Menggunakan Carbon PHP

_by: Khairun_

Biasanya kita cukup sulit untuk mengatur cara menampilkan tanggal di web. Akan tetapi, ada extensi PHP yaitu Carbon yang bisa mempermudah kita dalam mengatur tanggal.

di laravel, ada 2 format yang sering kita jumpai, yaitu :

1. input dengan type="date", misal untuk menunjukkan 28 Desember 2018, format yang muncul seperti ini: 2018-12-28
2. input timestamp misal pada _created\_at \_dan_ updated\_at \_, contoh valuenya: 2018-01-05 17:56:43

kedua contoh ini tentu kurang _user friendly_ untuk ditampilkan di front-end web..

Nah, berikut beberapa trik pengaturan tanggal menggunakan **Carbon**

### Ubah Format dalam Bahasa Indonesia

jangan lupa untuk memanggil library carbon

```php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Carbon\Carbon;
```

kemudian di dalam function, pastikan sistem server mengenali bahwa kita menggunakan bahasa indonesia.. kemudian convert tanggal menggunakan Carbon

```php
setlocale (LC_TIME, 'id_ID');
setlocale (LC_TIME, 'INDONESIA');

$created_at = "2018-01-05 17:56:43";

$ConvertedDate = Carbon::parse($created_at)->formatLocalized('%d %B %Y, %H:%M WIB');
// output : 05 January 2018, 17:56 WIB

$ConvertedDate2 = Carbon::parse($created_at)->formatLocalized('%d %b %y, %H:%M WIB');




```



