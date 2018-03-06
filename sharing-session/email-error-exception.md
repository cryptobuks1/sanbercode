# Mengirim Email Error Exception

#### _by Abdul Alim_

Anda telah membuat aplikasi **Laravel** baru untuk klien Anda dan sudah _**deploy**_ aplikasi tersebut di _**production server**_. Semuanya bekerja dengan baik sampai customer/klien anda memiliki masalah dengan aplikasi karena bug atau error. hal ini tidak masalah jika anda sebagai web developer memperbaikinya dengan cepat, tetapi jika tidak klien/customer akan meninggalkan aplikasi tersebut.

Tapi bagaimana jika Anda mendapatkan dengan cepat mendapatkan notifikasi e-mail tentang bug dan anda dapat memperbaikinya secepatnya. Di Laravel, ini bisa dilakukan dengan mudah.

Di Laravel,  semua _**exceptions**_ oleh App\Exceptions\Handler _class_. _Class_ ini berisi dua _method_: _report_ dan _render_. kita akan fokus pada _report method, \_Ini digunakan untuk mencatat_ exceptions_ atau mengirimnya ke \_external service_ seperti _Bugsnag_ atau _Sentry. _Secara _default_, report method _hanya melewati_ exceptions_ ke \_base class_ dimana _exceptions_ dicatat. Namun, kita bisa menggunakannya untuk mengirim email ke developer _tentang exceptions tersebut_. Cara menggunakannya seperti dibawah ini:

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

disini kita menggunakan

Each type of email sent by the application is represented as a “mailable” class in Laravel. So, we need to create our mailable class using the`make:mail`command:

```
$ php artisan make:mail ExceptionOccured
```

This will create a class`ExceptionOccured`in the`app/Mail`directory.

Merely sending the mail will not solve the problem. We need the full stack trace of the exception. And for that, we can use the Symfony’s Debug component.

```
public
function
sendEmail
(Exception $exception)
{

try
 {
        $e = FlattenException::create($exception);

        $handler = 
new
 SymfonyExceptionHandler();

        $html = $handler-
>
getHtml($e);

        Mail::to(
'developer@gmail.com'
)-
>
send(
new
 ExceptionOccured($html));
    } 
catch
 (
Exception
 $ex) {
        dd($ex);
    }
}
```

Make sure you add the following code at the top of the file:

```
use
Mail
;

use
Symfony
\
Component
\
Debug
\
Exception
\
FlattenException
;

use
Symfony
\
Component
\
Debug
\
ExceptionHandler
as
SymfonyExceptionHandler
;

use
App
\
Mail
\
ExceptionOccured
;
```

_Note—We have used the_`try`_block to avoid the infinite loop if the mail command fails._

Then, in your`ExceptionOccured`mailer class:

```
<
?php
namespace
App
\
Mail
;


use
Illuminate
\
Bus
\
Queueable
;

use
Illuminate
\
Mail
\
Mailable
;

use
Illuminate
\
Queue
\
SerializesModels
;

use
Illuminate
\
Contracts
\
Queue
\
ShouldQueue
;


class
ExceptionOccured
extends
Mailable
{

use
Queueable
, 
SerializesModels
;


/**
     * The body of the message.
     *
     * 
@var
 string
     */
public
 $content;


/**
     * Create a new message instance.
     *
     * 
@return
 void
     */
public
function
__construct
($content)
{

$this
-
>
content = $content;
    }


/**
     * Build the message.
     *
     * 
@return
 $this
     */
public
function
build
()
{

return
$this
-
>
view(
'emails.exception'
)
                    -
>
with(
'content'
, 
$this
-
>
content);
    }
}
```

Add the following code in your`emails.exception`view file:

```
{!! 
$content
 !!}
```

Now, whenever an exception is thrown in your application, you will receive an email with full stack trace. Cool!

