---
layout: post
title:  "Composer fxp global error"
date:   2016-09-06 09:42 +0700
categories: PHP composer yii2 fxp 
---

Yang benar saja, sudah beberapa kali dalam setahun terakhir ini fxp plugin yang harus diinstall secara global di yii2 membuat composer saya mengeluarkan pesan galat seperti di bawah ini:


![galat-fxp](/assets/galat-fxp.png)


Solusinya, seperti yang sudah-sudah, hapus semua file vendor global:

```
$ cd ~/.composer
$ rm -rf vendor composer.lock
$ composer global install
```

Sepertinya ada update baru fxp yang harus diupdate. Terkadang memang cukup merepotkan jadinya. 



