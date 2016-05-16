---
layout: post
title:  "Instalasi Phantomjs di Mac OSX El Capitan"
date:   2015-10-14 20:10:39 +0700
categories: js osx
---

Phantomjs merupakan tool headless browser yang dapat kita gunakan untuk melakukan pengujian aplikasi berbasis web. Biasanya digunakan side-by-side dengan tool dari masing-masing bahasa pemrograman, contohnya adalah via codeception di PHP 

## Instalasi

Untuk dapat menjalankan phantomjs, sang developer telah menyediakan [binary package](http://phantomjs.org/download.html) yang dapat kita unduh ke dalam lingkungan Mac. Sebenarnya apabila kita menggunakan `brew`, ada beberapa paket yang sepertinya merupakan distribusi phantomjs. Namun ketika dicoba untuk diinstall, terdapat pesan bahwa versi yang ada di `brew` tidak cocok untuk diinstall di Yosemite/El Capitan.

```bash
$ brew search phantomjs
homebrew/versions/phantomjs17		homebrew/versions/phantomjs198
homebrew/versions/phantomjs182		phantomjs
homebrew/versions/phantomjs192
Caskroom/cask/phantomjs
```

Kemudian ketika kita ingin mencoba melakukan instalasi, terdapat pesan bahwa versi yang ada di `brew` tidak cocok dengan OS.

```bash
$ brew install phantomjs
phantomjs: OS X Yosemite or older is required.
Error: An unsatisfied requirement failed this build.
```

Untuk sementara sembari menunggu update dari para kontributor `brew`, kita dapat melakukan unduh phantomjs secara manual.

Langkah pertama yang dilakukan adalah unduh phantomjs disini. 
Kemudian setelah itu ekstrak unduhan

```bash
$ mv phantomjs.zip ~
$ unzip phantomjs.zip 
```

Setelah selesai, kita dapat melakukan setting pada `~/.bash_profile` agar perintah `phantomjs` dapat diakses tanpa harus mencantumkan path dari tempat kita menyimpan `phantomjs`. Buka editor pilihan, kemudian tambahkan baris berikut:

```bash
export PATH=$PATH:$HOME/phantomjs/bin
```

Selanjutnya, jalankan perintah `source` untuk memaksa shell untuk membaca ulang konfigurasi di `.bash_profile`

```bash
$ source ~/.bash_profile
```


Untuk menjalankan, eksekusi perintah di bawah ini untuk menjalankan phantomjs:

```bash
$ phantomjs --webdriver=4444
```



## Problem Pada Saat menjalankan Phantomjs

Saya menemukan masalah ketika mencoba menjalankan phantomjs, yaitu ketika dieksekusi selalu muncul pesan error:

```bash
$ phantomjs --webdriver=4444
Killed: 9
```

Setelah dicari di [google](http://stackoverflow.com/questions/28267809/phantomjs-getting-killed-9-for-anything-im-trying), ternyata banyak yang mengalami masalah serupa, dan dapat diselesaikan dengan menggunakan executable unpacker via `upx`, yang dapat diinstall via `brew`

```bash
$ brew install upx
```

Berikutnya, kita jalankan `upx` ke `phantomjs`:

![start-upx](/assets/upx.png)

Setelah selesai, kita dapat mencoba menjalankan kembali `phantomjs`:

![phantom-start](/assets/phantom-start.png)

Ok, tampaknya kini `phantomjs` sudah dapat digunakan. 

Happy Coding :-)




