---
layout: post
title:  "React Native Android Setup"
date:   2019-05-31 22:38:00 +0700
categories: react react-native android
---

Saya baru mulai belajar untuk memulai pengembangan di ranah mobile, dan terus terang <i>learning curve</i>nya lumayan menantang. Untuk lebih mempersingkat waktu belajar, seperti developer react yang lain, saya memutuskan untuk belajar react-native. 

Di lingkungan react-native, ada dua pilihan platform pengembangan. Menggunakan Expo SDK atau langsung saja antara react-native dan perangkat.

Kelebihan menggunakan Expo SDK adalah proses pengembangan terasa lebih mudah, terutama pada saat menggunakan komponen-komponen yang spesifik ke perangkat android/iOS. Namun hal ini dibayar dengan degradasi performa yang bisa saya bilang cukup lambat, apalagi untuk perangkat dengan tenaga komputasi yang tidak terlalu besar. Oleh karena itu, pada saat proses belajar saya lebih memilih untuk tidak menggunakan Expo SDK.

Dalam proses setup terdapat beberapa bagian yang harus kita persiapkan, react-native itu sendiri, android studio, dan emulator/perangkat fisik untuk menjalankan aplikasi


## SDK Setup

* unduh dan install [android studio](https://developer.android.com/studio/)

* setup android emulator pada menu `tools > avd manager`

![menu-avd-manager](/assets/menu-avd-manager.png)

* jalankan perintah `adb reverse tcp:8081 tcp:8081` untuk memungkinan react native untuk mengirimkan live reload ke perangkat lewat port `8081`


### Setup Perangkat Fisik

Proses setup device fisik sendiri sedikit berliku, namun kira-kira langkah-langkahnya
sebagai berikut (dengan asumsi kita menggunakan OS Linux Ubuntu 16.04):

* hubungkan perangkat android kita dengan kabel

* aktifkan fitur usb debugging pada konfigurasi developer mode

* apabila semua berjalan dengan lancar, dengan perintah `adb devices` kita dapat melihat
     device android yang sudah terhubung

* untuk mengkonfigurasikan os kita agar dapat terhubung dengan device, jalankan perintah
     `lsusb` untuk melihat id perangkat kita di os:

```bash
 $ lsusb

 Bus 001 Device 004: ID 04f2:b341 Chicony Electronics Co., Ltd
 Bus 001 Device 054: ID 18d2:4ee7 Google Inc.
 Bus 001 Device 002: ID 0bde:8149 Realtek Semiconductor Corp. RTLXXXXXEUS 802.11n Wireless Network Adapter
 Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

pada kasus ini perangkat saya adalah `Google Inc.` dengan id `18d1:4ee7`, maka kita dapat
mencatat pengaturan pada `udev` sbb:

```bash
$ echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="18d2", MODE="0666", GROUP="plugdev"' | sudo tee /etc/udev/rules.d/51-android-usb.rules
```


## Instalasi React Native

Karena react-native merupakan package global yang diinstall melalui npm/yarn, maka perintah yang dapat dijalankan adalah sebagai berikut:

```bash
$ npm i -g react-native
```



## Membuat Project Baru

Untuk membuat project baru tanpa expo, kita dapat menggunakan perintah `init`:

```bash
$ react-native init HelloReactNative
$ cd HelloReactNative
```

kemudian untuk menjalankan react-native pada android (saya disini mengasumsikan bahwa emulator/koneksi fisik perangkat telah terhubung):

```bash
$ emulator -avd Nexus_4_API_25
```

pada tab/jendela terminal baru:

```bash
$ react-native run-android
```

untuk melihat log seperti `console.log`, kita dapat menjalankan perintah ini di tab/jendela terminal baru:

```bash
$ react-native log-android
```

Mungkin kira-kira seperti ini gambaran setup yang harus kita lakukan untuk dapat melakukan pengembangan react-native di android. Sebagai kesimpulan, kita memang tetap membutuhkan android studio untuk menjalankan emulator dan pada saatnya ketika aplikasi siap dirilis, digunakan untuk signing artifak aplikasi.

demikian, happy coding! :)
