---
layout: post
title:  "Struktur Project Golang Menggunakan Go Mod"
date:   2020-10-14 17:03:44 +0700
categories: golang
---


# Struktur Project Golang Menggunakan Go Mod 

Pada bahasa pemrograman Go sejak versi 1.11, kita dapat menggunakan struktur modular yang lebih 
fleksibel menggunakan `go mod` dibandingkan dengan versi sebelumnya yang membuat kita selalu 
terpaut dengan struktur `GOPATH`. Kemudahan yang diberikan oleh `go mod` menurut hemat saya 
cukup krusial di dalam mempermudah developer di dalam menentukan struktur project yang diinginkan.

Pada tulisan ini saya akan mencoba menjelaskan mengenai cara menggunakan `go mod` pada project 
sederhana kita.

## Inisialisasi

Misalkan kita telah membuat direktori baru bernama `hellp`, dan kita 
sudah berada di dalam direktori tersebut. Untuk melakukan inisialisasi, 
gunakan perintah `go mod`:

```bash
$ go mod init some-repo.co.id/donixo/hellp
```

Perintah `go mod` akan menghasilkan satu berkas baru dengan nama `go.mod` pada 
direktori kita berada. Isi berkas tersebut kira-kira seperti di bawah ini:

```txt
module some-repo.co.id/donixo/hellp

go 1.14
```

## Struktur Project

Misalkan kita ingin membuat struktur project dengan satu berkas program utama `hellp.go` 
dan dua buah modul dengan nama `lala` dan `susu`:

```
.
├── go.mod
├── hellp.go
├── lala
│   ├── ahoy.go
│   └── ahoy_test.go
└── susu
    └── jinx.go
```


## Berkas Utama

Misal, pada berkas utama, kita ingin mengimport modul `susu`, maka format import yang 
dapat kita lakukan adalah `<nama-modul-di-go-mod-kita>/<folder-modul>`, dalam struktur direktori contoh di atas, maka hasilnya akan menjadi sebagai berikut: `some-repo.co.id/donixo/hellp/susu`.


Untuk lebih jelasnya, kita dapat melihat isi dari berkas `hellp.go` di bawah ini:

```go
package main

import "fmt"
import "some-repo.co.id/donixo/hellp/susu"

func main() {
    fmt.Println(susu.Jinx())
	
}
```

## Direktori Modul

Jika pada bagian di atas kita melihat cara mendefinisikan pemanggilan modul dari dalam berkas utama, 
maka pada bagian ini kita akan melihat bagaimana cara mendefinisikan berkas dari dalam modul. 

Pada contoh di bawah ini kita akan melihat kode dari dua buah modul, `lala` dan `susu`. Modul 
`susu` membutuhkan satu fungsi, yaitu `Ahoy()` dari modul `lala`:
 

lala/ahoy.go:

```go
package lala

func Ahoy() string {
    return "ahoy!"
}
```

lala/ahoy_test.go:

```go
package lala

import "testing"

func TestAhoy(t *testing.T) {
	got := Ahoy()
	if got != "ahoy!" {
		t.Errorf("we want ahoy")
	}
}
```

Pada modul `susu`, kita dapat melakukan import modul `lala` dengan format  `<nama-modul-di-go-mod-kita>/<folder-modul>`, atau mengacu pada contoh di bawah ini, 
`some-repo.co.id/donixo/hellp/lala`.

susu/jinx.go:

```go
package susu

import "some-repo.co.id/donixo/hellp/lala"

func Jinx() string {
    return lala.Ahoy() + " jinx!"
}
```