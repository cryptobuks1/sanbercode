# Upload File

Berikut code yang digunakan untuk upload file

```
// fungsi ini menerima kiriman request dari form

public function functionName(Request $request)
{
    // cek apakah ada input dengan type file yang memiliki atribut name="file-x"
    if ($request->hasFile('featured_image')) 
    {
    
            $file = $request['featured_image']; // file akan mengambil value dari input tsb
            $uploadPath = public_path('images/featured-image');

            $extension = $file->getClientOriginalExtension();
            $fileName = $request['slug'] . '_' . 'featured_image' . '.' . $extension;

            $file->move($uploadPath, $fileName);
            $input['featured_image'] = $fileName;
            
    }


}
```



