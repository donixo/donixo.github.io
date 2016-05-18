---
layout: post
title:  "Behaviour Driven Development di Node.js"
date:   2016-02-03 20:00:39 +0700
categories: js bdd
---

## BDD di Node.js

Maksudnya behaviour driven development atau BDD itu adalah terdapat satu file referensi dalam plain teks yang menjelaskan bagaimana suatu “kelakuan” fitur dalam aplikasi bekerja.

Kelebihan apabila menggunakan BDD adalah developer, tester, dan pemilik proses bisnis (client) dapat memiliki suatu pengertian dan pemahaman yang sama mengenai behaviour sistem aplikasi. Contohnya adalah sebagai berikut:

```txt
Feature: Warteg Lunch
As orang laper, I want to buy myself lunch from warteg

     Scenario: Dine-in at nearby local warteg
          Given I already seated in warteg's long stool
          
          When I pick food item "sayur asem"
               And I pick food item "tempe goreng"
               And I pick food item "sambal terasi"
               
          Then I am charged Rp "15000" by shopkeeper

```

Plain teks di atas adalah contoh dari Gherkin script yang digunakan pada cucumber BDD. Karena terdiri dari teks plain feature dan mendekati bahasa sehari-hari dan terdiri dari scenario dan action text (given, and, when, then) maka BDD dapat mengurangi potensi kesalahan pengertian antara developer, tester serta pemilik proses bisnis.

## Tools

Pada aplikasi berbasis web yang dibangun menggunakan node.js, untuk dapat mengimplementasikan BDD dapat menggunakan banyak pilihan perangkat. Namun yang akan digunakan disini adalah Cucumber + WebdriverIO + Selenium Server atau Phantomjs. 

### Cucumber
Merupakan tools yang mengatur jalannya BDD. Utamanya yang berkaitan langsung pada implementasi kita adalah hubungan antara plain text behaviour definition dengan kode sumber step definition. 

Yang dimaksud dengan step definition itu sendiri merupakan jembatan antara teks behaviour dengan kode sumber testing sebenarnya. Sebagai contoh adalah terjemahan step definitions dari teks behaviour makan di warteg yang ada pada awal artikel ini:

```js
this.Given(/^I already seated in warteg's long stool$/, cb => {
  cb.pending();
});

this.When(/^I pick food item "([^"]*)"$/, (arg1, cb) => {
  cb.pending();
});

this.Then(/^I am charged Rp "([^"]*)" by shopkeeper$/, (arg1, cb) => {
  cb.pending();
});
```

### WebdriverIO + Selenium Server / Phantomjs
Untuk implementasi cucumber pada aplikasi berbasis web, maka dibutuhkan implementasi otomasi web browser untuk setiap step definition yang sudah ada di atas, untuk ini kita membutuhkan  WebdriverIO yang merupakan binding antar muka pemrograman ke Selenium server.


## Implementasi

Untuk lebih jelasnya, kita dapat melakukan langkah-langkah implementasi BDD di Node.js sbb:

- Instalasi Selenium Server / Phantomjs
- Instalasi webdriverio
- instalasi cucumber.js
- project setup
- membuat sample BDD Feature
- integrasi dengan grunt task runner

### Instalasi Selenium Server / Phantomjs

di Mac OSX via brew instalasi dapat dilakukan dengan mudah via

```bash
$ brew install selenium-server-standalone
$ brew install chromedriver
```

untuk menjalankan selenium dapat melalui perintah `$ selenium-server`

Apabila ingin menggunakan headless browser via phantomjs:

```bash
$ brew install phantomjs
```
Untuk menjalankannya pada port yang ekuivalen dengan selenium adalah dengan perintah `$ phantomjs —webdriver=4444`

### Instalasi webdriverio

```bash
$ npm install —save-dev webdriverio
```

### Instalasi cucumber.js

```bash
$ npm install —save-dev cucumber
```

### Project Setup

Pada direktori root project, pertama-tama kita harus membuat folder test dengan struktur direktori sebagai berikut:

```text
features/
     our-own-feature-app.feature
     support/
     step_definitions/
```

File `our-own-feature-app.feature` berisi Gherkin DSL file yang kita definisikan di awal yang berisi `given-when-then-and-but`. satu file dot feature hendaknya berisi satu buah feature dan beberapa scenario

Direktori `support/` berisi file-file global yang akan di load pada saat cucumber BDD test dijalankan. Cucumber juga menyediakan `World` object yang dapat diakses oleh setiap file step definitions yang ada.

Direktori `step_definitions/` berisi kode sumber dari feature `given-when-then-and-but` yang ada pada setiap file dot feature

### Sample BDD Feature


#### cucumber.js

Setelah selesai melakukan setup file, maka kita dapat mulai melakukan implementasi secara langsung. Untuk contohnya kita akan menggunakan feature `makan di warteg` yang sudah kita bahas di atas. Langkah-langkah implementasinya apabila dituliskan adalah sebagai berikut:

##### setup `World` object dan `env` pada direktori `features/support/` untuk pertama kali

pada `cucumber.js` terdapat direktori support yang dapat digunakan untuk untuk mendefinisikan konfigurasi dan shared object/variable yang dapat digunakan pada seluruh step definition.

Buat file baru `features/support/env.js`, dan ketikkan baris di bawah ini:

 
 ```js
 koding isi file env.js disini
 ```



##### buat file `warteg.feature` pada direktori `features/` 

##### jalankan `$ ./node_modules/cucumber/bin/cucumber.js` pada root project untuk menyalin sample step definitions

##### buat file `warteg.step.js` pada direktori `features/step_definitions/`


#### Dummy warteg web project

#### Development process, BDD style

