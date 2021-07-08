---
title: "iMacros: Delete XSS Hunter Fires"
date: 2021-07-08 10:00:00 +07:00
tags: [iMacros]
description: Bot delete triggered payload XSS Hunter.
image: /imacros-delete-xsshunter-fires/screencapture-xsshunter-app-2021-07-08.png
---
Sempat kebanyakan page yang ketrigger dari payload XSS Hunter. Sampe akhirnya bingung gimana cara hapusnya. Mungkin bisa pakai Javascript buat trigger button delete, tapi saya ndak bisa Javascript:((

<img src="{{ page.image }}" width="100%">

150 halaman lebih dengan isi halaman yang mirip—kebanyakan sama. Biar ngga kebanyakan, bikin bot delete pakai iMacros.

```
VERSION BUILD=1011 RECORDER=CR
URL GOTO=https://xsshunter.com/app
TAG POS=1 TYPE=BUTTON ATTR=CLASS:"delete_injection_button btn btn-danger btn-block"
TAG POS=2 TYPE=BUTTON ATTR=CLASS:"delete_injection_button btn btn-danger btn-block"
TAG POS=3 TYPE=BUTTON ATTR=CLASS:"delete_injection_button btn btn-danger btn-block"
TAG POS=4 TYPE=BUTTON ATTR=CLASS:"delete_injection_button btn btn-danger btn-block"
TAG POS=5 TYPE=BUTTON ATTR=CLASS:"delete_injection_button btn btn-danger btn-block"
WAIT SECONDS=2
```

Kode di atas berarti menginstruksikan iMacros untuk *klik* HTML Tag dengan class `delete_injection_button btn btn-danger btn-block` selama 5 kali (jumlah item yang harus dihapus di satu halaman). Lalu `WAIT SECONDS=2` untuk menunggu loading saat item dihapus.

Jalankan script secara loop (Play Loop) sesuai jumlah halaman.

<iframe width="100%" height="315" src="https://www.youtube.com/embed/cWwGf4rZEEM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>