---
layout: post
title:  "Certbot LetsEncrypt SSL"
date:   2017-02-04 11:40 +0700
categories: ssl security server 
---

Apabila kita ingin memasang sertifikat SSL namun kekurangan budget, dapat dicoba solusi 
gratisan SSL dari LetsEncrypt, sebuah lembaga publik yang bertujuan untuk meng-https kan 
internet. 

Lebih lanjutnya tentang LetsEncrypt dapat dilihat pada 
laman [situsnya](https://letsencrypt.org/about/).

Untuk toolkit server linuxnya sendiri telah disediakan oleh EFF bernama `certbot`:

Lebih lanjut tentang `certbot` dapat dilihat pada: [https://certbot.eff.org](https://certbot.eff.org)


Pada artikel kali ini akan dibahas mengenai cara pemasangan `certbot` pada server linux. 
Hampir seluruhnya diambil dari dokumentasi certbot yang memang sudah sangat lengkap.


## Instalasi

Sejauh ini `certbot` telah mendukung berbagai macam distribusi linux, 
baik CentOS, Ubuntu, ataupun Debian. Saya asumsikan tidak berbeda jauh untuk eksekusinya.


Untuk instalasi, pertama-tama buat folder baru di /usr/local/autossl, buat agar hanya 
root yang bisa eksekusi. Kita akan menyimpan file `certbot` pada direktori ini. 
Kemudian masuk ke dalam autossl lalu eksekusi perintah dibawah ini:

```sh
$ wget https://dl.eff.org/certbot-auto
$ chmod a+x certbot-auto
```


## Pembuatan Sertifikat

buat file baru dengan nama pada /usr/local/autossl 
dengan nama `server-cert-issue`.

pada file tersebut dapat diisi perintah certbot awal inisiasi pada 
sub domain yang diinginkan untuk dipasang sertifikat untuk pertama kali:

```sh
#!/bin/bash


MY=$(pwd)

$MY/certbot-auto certonly --webroot --email admin@example.com \
-w /some/web/dir -d somedomain.example.com

```

untuk subdomain lainnya mengikuti rule `-w` untuk web direktori dan `-d` 
untuk nama subdomain.

jangan lupa untuk menjalankan perintah sebagai root, karena cerbot memerlukan 
beberapa setup dan mekanisme challenge-response dengan cara menulis file pada 
web direktori kita yang sudah diset via `-w` di atas



pada saat dokumentasi ini dibuat, lamanya berlaku sertifikat hanya 3 bulan,
oleh karena itu, dapat dijalankan perintah dalam cron untuk mengecek renewal 
sebanyak dua kali sehari seperti yang disarankan oleh certbot:

```sh
$ certbot-auto renew --quiet
```

## Pemasangan di web server

sebenarnya cerbot memiliki fitur untuk langsung menulis di konfigurasi apache/nginx 
atau web server lainnya ketika kita melakukan eksekusi perintahnya, namun untuk 
lebih amannya kita akan menggunakan certbot hanya untuk melakukan generate cert saja,
sesuai dengan parameter `certonly` pada pembuatan sertifikat.

Path hasil eksekusi certbot ada pada direktori `/etc/letsencrypt`, sedangkan path 
sertifikat yang akan digunakan ada pada `/etc/letsencrypt/live/nama-domain`.

Kemudian kita dapat memasang sertifikat tersebut pada konfigurasi web server, 
contohnya pada apache `/etc/httpd/conf.d`:

```txt
SSLCertificateFile /etc/letsencrypt/live/some-domain/fullchain.pem
SSLCertificateKeyFile /etc/letsencrypt/live/some-domain/privkey.pem
```

setelah selesai, restart web server, maka dapat dilihat bahwa SSL gratisan dari 
letsencrypt telah dapat digunakan.


Happy SSL-ing :D




