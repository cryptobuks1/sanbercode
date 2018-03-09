# Mengirim Email Error Exception

#### _by Abdul Alim_

Anda telah membuat aplikasi **Laravel** baru untuk klien Anda dan sudah _**deploy**_ aplikasi tersebut di _**production server**_. Semuanya bekerja dengan baik sampai customer/klien anda memiliki masalah dengan aplikasi karena bug atau error. hal ini tidak masalah jika anda sebagai web developer memperbaikinya dengan cepat, tetapi jika tidak klien/customer akan meninggalkan aplikasi tersebut.

Tapi bagaimana jika Anda mendapatkan dengan cepat mendapatkan notifikasi e-mail tentang bug dan anda dapat memperbaikinya secepatnya. Di Laravel, ini bisa dilakukan dengan mudah.

Di Laravel,  semua `exceptions` oleh `App\Exceptions\Handler` **Class**. **Class** ini berisi dua method: `report`dan `render`. kita akan fokus pada `report`, Ini digunakan untuk mencatat `exceptions` atau mengirimnya ke `external service` seperti Bugsnag atau Sentry. Secara `default`, `report` hanya melewati `exceptions` ke `base class` dimana `exceptions` dicatat. Namun, kita bisa menggunakannya untuk mengirim email ke `developer` tentang `exceptions` tersebut. Cara menggunakannya seperti dibawah ini:

```php
/**
 * Report or log an exception.
 *
 * This is a great spot to send exceptions to Emails.
 *
 * @param  \Exception  $exception
 * @return void
 */
public function report(Exception $exception)
{
    if ($this->shouldReport($exception)) {
        $this->sendEmail($exception); // sends an email
    }

    return parent::report($exception);
}

/**
 * Sends an email to the developer about the exception.
 *
 * @param  \Exception  $exception
 * @return void
 */
public function sendEmail(Exception $exception)
{
    // sending email
}
```

Di sini kita menggunakan metode shouldReport untuk mengabaikan pengecualian yang tercantum dalam properti  $dontReport dari handler exceptions.

Setiap email yang dikirim aplikasi direpresentasikan sebagai “mailable” class in Laravel. jadi kita perlu untuk membuat mailable class dengan menggunakan command`make:mail`:

```
$ php artisan make:mail ExceptionOccured
```

Ini akan membuat class`ExceptionOccured`di dalam direktori`app/Mail`.

Dengan hanya mengirim email tidak akan menyelesaikan masalah. Kita membutuhkan full stack trace dari exceptions. Dan untuk itu, kita bisa menggunakan komponen Debug milik Symfony.

```php
public function sendEmail(Exception $exception)
{
    try {
        $e = FlattenException::create($exception);

        $handler = new SymfonyExceptionHandler();

        $html = $handler->getHtml($e);

        Mail::to('developer@gmail.com')->send(new ExceptionOccured($html));
    } catch (Exception $ex) {
        dd($ex);
    }
}
```

Pastikan anda menambahkan kode dibawah ini diatas file:

```php
use Mail;
use Symfony\Component\Debug\Exception\FlattenException;
use Symfony\Component\Debug\ExceptionHandler as SymfonyExceptionHandler;
use App\Mail\ExceptionOccured;
```

lalu, dalam`ExceptionOccured`mailer class:

```php
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Mail\Mailable;
use Illuminate\Queue\SerializesModels;
use Illuminate\Contracts\Queue\ShouldQueue;

class ExceptionOccured extends Mailable
{
    use Queueable, SerializesModels;

    /**
     * The body of the message.
     *
     * @var string
     */
    public $content;

    /**
     * Create a new message instance.
     *
     * @return void
     */
    public function __construct($content)
    {
        $this->content = $content;
    }

    /**
     * Build the message.
     *
     * @return $this
     */
    public function build()
    {
        return $this->view('emails.exception')
                    ->with('content', $this->content);
    }
}
```

Tambahkan kode berikut di file`emails.exception`dalam view:

```
{!! $content !!}
```

Sekarang, kapanpun exception dikeluarkan dalam aplikasi anda, anda akan menerima  email dengan full stack trace nya.

Referensi : [https://laravel-news.com/email-on-error-exceptions](https://laravel-news.com/email-on-error-exceptions)

