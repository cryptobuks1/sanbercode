# Membuat template di Laravel

by: Andrika

Sistem Templating laravel telah dirancang sedemikian rupa yang akan memudahkan kita dalam membangun layout-layout untuk front-end sistem atau web yang kita buat apalagi pada sistem templating laravel ini telah ditanamankan pada **Blade. **Biar kita lebih “jelas”  bagaimana system templating pada Laravel ini bekerja, kita akan langsung praktekkan saja.

## Layout

Persiapkan project Laravel, kemudian kita buat satu file di dalam direktori `resources/views/layouts`dengan nama`template.blade.php` , dan tulislah code dibawah:

```
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8">
		<title>Belajar Template Laravel</title>
	</head>
	<body>
		<ul>
			@section('sidebar')
			  <li>HTML</li>
			  <li>CSS</li>
			  <li>JS</li>
			@show
		</ul>
		<div class="container">
			@yield('content')
		</div>
	</body>
</html>
```



