---
layout: post
title:  "Javascript Template Menggunakan Handlebars.js dan JQuery"
date:   2015-06-17 16:08:39 +0700
categories: js handlebars template
---

Handlebars.js merupakan templating library yang dapat kita gunakan di sisi client. Manfaat yang dapat diambil adalah, dengan menggunakan template library, kode javascript kita tidak akan tercampur dengan html. Hal ini dapat membuat organisasi kode sumber menjadi lebih rapi dan lebih mudah di maintain.

Pada kesempatan kali ini saya akan menunjukkan cara penggunaan [Handlebars.js][1] dan JQuery dengan membuat sebuah address book sederhana. Address book yang akan dibuat akan berupa satu tabel sederhana berisi nama dan alamat. Operasi yang dapat dilakukan pada address book ini adalah operasi CRUD (create read update delete) dari data address book. Untuk lebih jelasnya lihat gambar hasil akhir di bawah ini:

![gambar-app-jadi](/assets/handlebars-hasil-akhir.png)



### Persiapan

Untuk memulai, kita membutuhkan handlebars.js dan JQuery. Setelah itu kita tinggal memasukkan script untuk memanggil kedua script tersebut pada bagian bawah file html yang akan dibuat

```html
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript" src="handlebars-v1.3.0.js"></script>
```

Setelah selesai, kita dapat mulai melakukan desain tampilan antar muka.

### User Interface
Pada kesempatan ini, ada 4 event yang akan kita kelola untuk menyelesaikan address book ini. Untuk lebih jelasnya dapat dilihat pada gambar di bawah ini

![mockup-ui](/assets/handlebars-mockup.png)

Pada dasarnya event yang akan kita tangkap adalah event pada saat tambah, edit, hapus, dan menampilkan form data. Setelah kita menyelesaikan desain antar muka, berikutnya yang dapat kita selesaikan adalah desain template untuk kemudian diimplementasikan menggunakan handlebars.js.


### Template
Pada contoh ini, hanya template row data tabel yang ditampilkan, sisanya pembaca dapat melihat langsung pada gist yang ada di akhir posting. Pada handlebar.js, cara melakukan inisialisasi template adalah sebagai berikut:

{% highlight txt %}
{% raw %}
<script id="row-adbook" type="text/x-handlebars-template">
{{#each data}}
  <tr>
    <td>{{nama}}</td>
    <td>{{alamat}}</td>
    <td align="center">
      <a href="#edit" class="rowedit" data-index="{{@index}}">Edit</a>
      || 
      <a href="#hapus" class="rowdelete" data-index="{{@index}}">Hapus</a>
    </td>
  </tr>
  {{else}}
    <tr>
      <td colspan="3" align="center">Tidak ada entry.</td>
    </tr>
{{/each}}
</script>
{% endraw %}
{% endhighlight %}

template akan dapat dibaca oleh library handlebar melalui `id="row-adbook"` dan `type="text/x-handlebars-template"`. Setelah selesai membuat template, berikutnya kita dapat melakukan kompilasi template ke dalam variabel:

```javascript
var rows = Handlebars.compile(
	$('#row-adbook').html()
);
```
Variabel `rows` saat ini telah berisi method hasil compile dari `$('#row-adbook').html()`. Untuk dapat menggunakannya dalam kode kita adalah sebagai berikut:

```javascript
//buat data dummy untuk kita masukkan ke dalam rows
var adressbook = [
	{nama: 'Alice', alamat: 'Jakarta'},
	{nama: 'Bob', alamat: 'Bogor'},
	{nama: 'Carl', alamat: 'Cirebon'},
];

//kita proses data ke dalam rows
var hasil = rows({ data: addressbook });

//lihat hasil di dalam console:
console.log(hasil);

```

### Kesimpulan 
Demikian contoh sederhana di dalam memanfaatkan handlebar.js. Sebenarnya masih banyak contoh template script yang dapat diterapkan pada kode template kita, untuk hal tersebut saya menyerahkan kepada pembaca untuk melihat sendiri pada dokumentasi handlebar.js di situsnya. 


gist untuk keseluruhan source code posting blog ini ada di [https://gist.github.com/donixo/8898521][2]

[1]: http://handlebarsjs.com/
[2]: https://gist.github.com/donixo/8898521



