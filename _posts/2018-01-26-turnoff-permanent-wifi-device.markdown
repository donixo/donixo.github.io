---
layout: post
title:  "Mematikan Secara Permanen Onboard Wifi Device"
date:   2018-01-26 18:04:39 +0700
categories: wifi network onboard
---


Apabila kita menggunakan laptop dengan Mint/Ubuntu, ada kalanya perangkat wifi bawaan laptop berhenti bekerja dikarenakan tidak cocok dengan kernel ataupun driver linux kita.

Biasanya kalau saya dikarenakan butuh cepat, biasanya langsung beli usb wifi yang tinggal colok dan bekerja. Merk TP-Link biasanya selalu berjalan dengan lancar apabila dipasang di laptop. 

Yang buat agak menyebalkan adalah, setiap selesai reboot kita harus secara 
manual menonaktifkan onboard wifi device yang sebenarnya sudah tidak kita gunakan lagi.

Pertama-tama, kita harus menentukan terlebih dahulu nama perangkat wifi kita tersebut via perintah
`ifconfig`, biasanya isinya adalah variasi dari `wlan0`.

Kita dapat secara permanen menonaktifkan wifi device tersebut pada `/etc/network/interfaces`:

```
$ sudo vim /etc/network/interfaces
```

kemudian tambahkan baris berikut ini:

```
iface wlan0 inet manual
```

simpan, kemudian restart sistem. Setelah itu kita tidak usah lagi repot-repot untuk manual mematikan interface wifi onboard tersebut.

Setelah ini *mungkin* bisa mulai menabung untuk beli Dell XPS Developer Edition. 
