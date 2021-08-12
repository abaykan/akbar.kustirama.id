---
title: "Membuat List Password Menggunakan CUPP"
date: "2018-10-03"
tags: ['Security']
---

**Membuat List Password Menggunakan CUPP** - Manusia, seberapa unik pun mereka berpikir, seringkali menggunakan pola yang sama ketika membahas password. Biasanya kita memilih password yang mudah diingat, jadi kita bawa barang pribadi ke password kita. Misalnya, seseorang bisa dengan mudah mengingat kata sandi yang berisi hari ulang tahunnya dan nama istrinya.

#### Membuat List Password

Apa yang akan kita gunakan dari list password tersebut? Banyak! Seperti melakukan bruteforce pada suatu halaman login.  Kata sandi yang lemah mungkin memang sangat pendek atau hanya menggunakan karakter alfanumerik. Sandi yang lemah juga bisa menjadi salah satu yang mudah ditebak oleh seseorang.

Kebanyakan orang akan menambahkan karakter seperti tanggal lahir, nama panggilan, alamat, nama hewan peliharaan atau saudara, atau kata umum seperti Tuhan, cinta, uang atau kata sandi. Kita akan membuat list password menggunakan [CUPP](https://github.com/Mebus/cupp) (Common User Passwords Profiler).

#### Apa itu CUPP?

Bentuk otentikasi yang paling umum adalah kombinasi dari nama pengguna dan kata sandi. Jika kedua nilai cocok disimpan dalam tabel yang disimpan secara lokal, pengguna diautentikasi untuk koneksi. Kekuatan kata sandi adalah ukuran kesulitan yang terlibat dalam menebak atau memecahkan kata sandi melalui teknik kriptografi atau pengujian otomatis berbasis-perpustakaan dari nilai-nilai alternatif. Itulah mengapa CUPP lahir, dan itu dapat digunakan dalam situasi seperti tes penetrasi hukum atau penyelidikan kejahatan forensik.

#### Menginstall CUPP

Hal paling utama yang kita butuh kan adalah Python `3.x`. Selanjutnya tinggal men-download file nya atau lalu buat list passwordnya!

```
git clone https://github.com/Mebus/cupp.git
cd cupp
python3 cupp.py -h
```

Beberapa option yang ada dalam CUPP.

```
    -h      this menu

    -i      Interactive questions for user password profiling

    -w      Use this option to profile existing dictionary,
            or WyD.pl output to make some pwnsauce :)

    -l      Download huge wordlists from repository

    -a      Parse default usernames and passwords directly from Alecto DB.
            Project Alecto uses purified databases of Phenoelit and CIRT which where merged and enhanced.

    -v      Version of the program
```

Jika masih bingung, silahkan simak video demo nya dibawah ini.

<script src="https://asciinema.org/a/204318.js" id="asciicast-204318" async><span data-mce-type="bookmark" style="display: inline-block; width: 0px; overflow: hidden; line-height: 0;" class="mce_SELRES_start">﻿</span></script>

Pada video diatas, saya merekan terminal saya menggunakan ASCIINEMA. Jika ingin membuat rekaman pada terminal kalian, ikutin cara-caranya di [sini](https://codelatte.org/cara-menggunakan-asciinema/).
