# Upload File

_by: Khairun ft Abdul Alim_

Ada 2 cara untuk upload file :

#### **Menggunakan code manual PHP**

```php
// fungsi ini menerima kiriman request dari form

public function functionName(Request $request)
{

    // masukkan semua isian form (request) ke dalam variabel input
    $input = $request->all();

    // cek apakah ada input dengan type file yang memiliki atribut name="file-x"
    if ($request->hasFile('file-x')) 
    {
            // file akan mengambil value dari input tsb
            $file = $request['file-x'];            

            // tentukan tempat penyimpanan file, misal di folder public/images
            $uploadPath = public_path('/images');

            // ambil jenis extensi file menggunakan fungsi getClientOriginalExtension() yang disediakan laravel
            $extension = $file->getClientOriginalExtension();

            // tentukan nama file, bisa menggunakan random string php, atau agar unik, menggunakan slug halaman
            $fileName = $request['slug'] . '_' . 'image' . '.' . $extension;

            // ambil file yang sudah diberi nama dan simpan ke tempat yg sudah diset sebelumnya
            $file->move($uploadPath, $fileName);

            // set di variabel $input agar memiliki atribut 'file-x' yang berupa path + filename  
            $input['file-x'] = $uploadPath . '/' . $fileName;

    }

}
```

#### Menggunakan package [**Laravel File Manager by Unisharp**](https://unisharp.github.io/laravel-filemanager/)

1. buatlah sebuah button, input, and image preview holder jika akan memilih gambar. tentukan id yang akan digunakan dalam input dan image berdasarkan `data-input` dan `data-preview`

   ```php
   <div class="input-group">
      <span class="input-group-btn">
        <a id="lfm" data-input="thumbnail" data-preview="holder" class="btn btn-primary">
          <i class="fa fa-picture-o"></i> Choose
        </a>
      </span>
      <input id="thumbnail" class="form-control" type="text" name="filepath">
    </div>
    <img id="holder" style="margin-top:15px;max-height:100px;">
   ```

2. Import lfm.js pada view \(jalankan php artisan vendor:publish jika dibutuhkan\).

   ```php
   <script src="/vendor/laravel-filemanager/js/lfm.js"></script>
   ```

3. Init filemanager dengan type. \(membutuhkan jQuery\)

   ```js
    $('#lfm').filemanager('image');
   ```

   atau

   ```js
    $('#lfm').filemanager('file');
   ```



