---
title: "Menambahkan Atribut Size (Width dan Height) pada Tag Image"
date: "2021-09-14"
tags: ['PHP']
image: /menambahkan-atribut-width-dan-height-pada-gambar/images/screenshot-1.png
---

**Menambahkan Atribut Size (Width dan Height) pada Tag Image** - Tulisan ini cuma catatan pribadi karena saya ngga ngerti _regex_.

Saya mendapat sebuah _case_ menambahkan atribut ke dalam tag `<img>` yang tidak mempunyai `height` dan `width` spesifik. Setelah mencoba beberapa cara, akhirnya ditemukan cara yang paling sederhana adalah menggunakan `preg_replace()`.

Kode yang saya gunakan:
```
$html_content = preg_replace('/(<img(?:(?!height|width="\d+").)*?)(\/)?>/', '$1 width="35%" height="35%"></img>', $html_content);
```

Contoh keseluruhan kode:

```php
<?php
$html_content = '
<!DOCTYPE html>
<html>
<head>
	<title>Title</title>
</head>
<body>
	<img src="https://assets.codelatte.net/images/uploads/dino.jpeg" class="ini-anggep-aja-class bla-bla">
	<br/>
	<img src="https://assets.codelatte.net/images/uploads/dinoo.jpeg" class="ini-anggep-aja-class bla-bla">
</body>
</html>';

$html_content = preg_replace('/(<img(?:(?!height|width="\d+").)*?)(\/)?>/', '$1 width="35%" height="35%"></img>', $html_content);
echo $html_content;
```

Hasilnya seperti yang terlihat di bawah ini.

<img src="images/screenshot-1.png" width="100%" height="100%" alt="Menambahkan Atribut Size (Width dan Height) pada Tag Image">