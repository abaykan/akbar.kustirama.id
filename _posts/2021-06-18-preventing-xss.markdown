---
layout: post
title:  "Preventing XSS"
date:   2021-06-18 06:23:02 +0530
categories: XSS
---
Intro. Ini intro biar muncul di homepage. Deskripsi lah gampangnya. Ini isi pertama abis Lorem Ipsum, diisi beginian biar keliatan agak bermanfaat.

Ini cuma beberapa cara mencegah XSS, masih ada banyak cara lain yang bisa dipake.


Escaping
----------------
```
"   >	&#34
#   >	&#35
&   >	&#38
'   >	&#39
(   >	&#40
)   >	&#41
/   >	&#47
;   >	&#59
<   >	&#60
>   >	&#62
```


URL Escaping
----------------

Jika mau menampilkan inputan user pada halaman, terutama di dalam tag HTML, contoh:
```html
<a href="http://www.website.com/?test=...ESCAPE INPUTAN PENGGUNA DISINI...">link</a>
```

Sebelumnya saya ingatkan terlebih dahulu agar tidak meng-encode semua isi URL, karena yang dibutuhkan hanya meng-encode inputan pengguna sehingga tidak terbaca sebagai script.


HTML Sanitizer
----------------

- PHP HTML Purifier - [http://htmlpurifier.org/](http://htmlpurifier.org/)
- JavaScript/Node.js Bleach - [https://github.com/ecto/bleach](https://github.com/ecto/bleach)
- Python Bleach - [https://pypi.python.org/pypi/bleach](https://pypi.python.org/pypi/bleach)


XSS Protection Header
----------------

HTTP response header ini memungkinkan filter XSS ke beberapa browser web. Peran header ini adalah untuk mengaktifkan kembali filter untuk situs web tertentu ini jika dinonaktifkan oleh pengguna.

`X-XSS-Protection "1; mode=block"`


PHP
----------------
```php
urlencode($_GET['input'])
filter_input(INPUT_GET, 'input', FILTER_SANITIZE_URL)
htmlspecialchars($_GET['input'])
strip_tags($_GET['input'])
htmlentities($_GET['input'])
```
