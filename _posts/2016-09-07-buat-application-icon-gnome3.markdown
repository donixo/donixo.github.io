---
layout: post
title:  "Membuat Icon Aplikasi Pada GNOME3"
date:   2016-09-07 07:32 +0700
categories: fedora24 xpm icons 
---

Ada kalanya ketika kita melakukan instalasi aplikasi pada linux dengan desktop GNOME3 terutama untuk aplikasi 
yang diunduh langsung dan bukan melalui package manager, kita tidak menemukan semacam "desktop icon" yang 
mempermudah kita untuk mengakses aplikasi tersebut dari GNOME activities.


Yang pertama harus dilakukan adalah mengecek path dimana icon applications kita tersimpan, pada OS Fedora 24
saya saat ini, pathnya ada di:

```
/home/user/.local/share/applications

```

Kemudian, buka teks editor anda dan ketikkan teks di bawah ini, (sebagai contoh saya menggunakan [ApacheDirectoryStudio][2]):


```
[Desktop Entry]
Encoding=UTF-8
Name=ApacheDirectoryStudio
Comment=LDAP GUI browser
Type=Application
Exec=ApacheDirectoryStudio
Icon=/home/user/src/ApacheDirectoryStudio/icon.xpm
Name[fr_FR]=ApacheDirectoryStudio
StartupWMClass=ApacheDirectoryStudio
Terminal=false
Categories=

```

`Exec` merupakan path executable kita, bisa berisi full path ke aplikasi, atau hanya berisi nama commandnya saja 
apabila sudah ada pada system `$PATH`.
`Icon` adalah path file icon dot.xpm yang biasanya disertakan pada direktori aplikasi yang diunduh. 


Setelah selesai, simpan sebagai file `ApacheDirectoryStudio.desktop` pada `$HOME/.local/share/applications`.
Untuk lebih detail, silakan kunjungi laman dokumentasi gnome [berikut ini][1].


Demikian, semoga bermanfaat


[1]: https://developer.gnome.org/integration-guide/stable/desktop-files.html.en
[2]: http://directory.apache.org/studio/download/download-linux.html

