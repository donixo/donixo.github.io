---
layout: post
title:  "Git Credentials via gnome-keyring"
date:   2016-08-26 07:32 +0700
categories: git gnome fedora24 
---


Git credentials yang sering digunakan untuk menghandle username/password di linux sepertinya tidak otomatis terkoneksi dengan keyring yang ada di OS, sehingga akibatnya pada saat kita melakukan clone, pull atau push kita harus berkali-kali melakukan entri password.

Pada dokumentasi git terdapat cara untuk melakukan konfigurasi pada `gitcredentials`, dimana kita dapat mengkonfigurasi  keyring untuk digunakan oleh google. Keyring ini yang kemudian akan menyimpan password yang telah kita entri, sehingga tidak usah berkali-kali mengetik password.

Untuk konfigurasinya kurang lebih seperti ini:

## Periksa gitcredentials yang tersedia pada sistem

```bash
$ git help -a | grep credential
  credential                remote-ext
  credential-cache          remote-fd
  credential-cache--daemon  remote-ftp
  credential-gnome-keyring  remote-ftps
  credential-store          remote-http
```

Saya sendiri menggunakan `gnome-keyring` untuk default credential

## Set config global 

Secara global, set git config untuk `gnome-keyring`:

```bash
$ git config --global credential.helper gnome-keyring
```

Setelah itu coba lakukan git pull/clone, kita hanya akan diberi prompt satu kali terkait username/password. Selebihnya akan dihandle oleh keyring.


happy coding :-)



