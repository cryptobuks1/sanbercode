# Mengirim Email Error Exception

#### _by Abdul Alim_

Dalam proses **web development** menggunakan **laravel** tentu kita sering menemui **error exception**, **error exception** itu berguna dalam proses _debug_ atau mencari _bug_ yang harus kita benarkan. tetapi kadang ketika sebuat project dalam _environment production _dalam proses fix bug harus dilakukan dengan cepat, permasalahannya kita belum tentu selalu tahu apakah dalam production terdapat error exception, maka dari itu perlu sebuah pencatatan error exception atau hal lain seperti itu. hal yang sering dilakukan kebanyakan _web developer _adalah mengirim error exception dari production ke email.

Dalam laravel terdapat handler error exception, dan disimpan di App\Exceptions\Handler class. dan kita dapat mengirim email error exception melalui itu, seperti dibawah ini:

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

_Note—We have used the`try`block to avoid the infinite loop if the mail command fails._

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

