# Upload File

_by: Khairun_

Berikut code yang digunakan untuk upload file

```php
// fungsi ini menerima kiriman request dari form

public function functionName(Request $request)
{
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

            // set kembali agar nama file masuk dalam array $request dari form 
            $request['file-x'] = $fileName;

    }

}
```



