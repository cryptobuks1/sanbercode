# Tambahan : Kapan Membuat Middleware?

2 Maret 2018

## Kapan Membuat Middleware?

**oleh : Bang Fady \(@fady-ni\)**

middleware memang cukup powerful untuk melakukan pengecekan dari request yang masuk ke website kita. tapi, walaupun begitu, tidak semua pengecekan cukup baik menggunakan middleware. contohnya saja ketika kita ingin membuat sebuah sistem dimana member harus diapprove terlebih dahulu oleh admin untuk bisa masuk. member yang belum mendapat approval akan dinilai sama dengan visitor biasa. apakah kita perlu membuat middleware untuk mengatasi hal ini?

jawabannya : lebih baik tidak. memang kita bisa menggunakan middleware untuk menjawab masalah ini, tapi itu terlalu overkill. alasannya karena pengecekan status approval ini hanya perlu dilakukan saat approval belum didapat saja. berbeda dengan pengecekan status admin

