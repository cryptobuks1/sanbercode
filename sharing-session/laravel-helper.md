## **Helper di Laravel -  SanberTEDx 2 Februari 2017 by Abdul Alim**

#### 



#### **Apa itu Helper?**

Secara bahasa artinya penolong atau pembantu

lalu apa fungsinya dalam laravel?

pada dasarnya, helper di Laravel adalah fungsi utilitas bawaan yang dapat Anda panggil dari manapun dalam aplikasi Anda

#### Helper di Laravel

Laravel memiliki “Global” helper yang tersedia di inti kerangka Laravel. Mereka dikelompokkan bersama berdasarkan fungsi yang mereka berikan. Berikut daftar grup helper:

* Arrays & Objects
* Paths
* Strings
* URLs
* Miscellaneous

Referensi: [https://laravel.com/docs/5.5/helpers](https://laravel.com/docs/5.5/helpers)

#### **Membuat Helper sendiri**

jika ada helper yang dibutuhkan tapi tidak ada dalam global helper laravel, kita bisa membuat helper sendiri dengan cara:

1. membuat file helper sendiri misal menggunakan nama helpers.php dan disimpan di folder tujuan misal di app/Http/helpers.php

2. menambahkan dan mendaftarkan file helper di composer.json di dalam autoload  
   `"autoload": {`

   `// your autoload`

   `"files": [`

   `"app/Http/helpers.php" //Add This Line`

   `]`

   `},`

3. run composer dump-autoload dalam terminal

4. buatlah funsi yang anda ingin gunakan dalam helpers.php

Referensi:

[https://code.tutsplus.com/id/tutorials/how-to-create-a-laravel-helper--cms-28537](https://code.tutsplus.com/id/tutorials/how-to-create-a-laravel-helper--cms-28537)

[http://itsolutionstuff.com/post/laravel-5-simple-user-access-control-using-middlewareexample.html](http://itsolutionstuff.com/post/laravel-5-simple-user-access-control-using-middlewareexample.html)

