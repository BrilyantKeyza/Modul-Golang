---
sidebar_position: 8
---

# A.8. Komentar


Komentar biasa dimanfaatkan untuk untuk menyisipkan catatan pada kode program, atau untuk menulis penjelasan/deskripsi mengenai suatu blok kode, atau bisa juga digunakan untuk me-_remark_  kode (men-non-aktifkan kode yg tidak digunakan). Komentar selalu diabaikan ketika kompilasi maupun eksekusi program.

Ada 2 jenis komentar di Go,  _inline_  &  _multiline_. Pada pembahasan ini akan dijelaskan tentang penerapan dan perbedaan kedua jenis komentar tersebut.

## A.8.1. Komentar  _Inline_

Penulisan komentar jenis ini di awali dengan tanda  **double slash**  (`//`) lalu diikuti pesan komentarnya. Komentar inline hanya berlaku untuk satu baris pesan saja. Jika pesan komentar lebih dari satu baris, maka tanda  `//`  harus ditulis lagi di baris selanjutnya.

```
package main

import "fmt"

func main() {
    // komentar kode
    // menampilkan pesan hello world
    fmt.Println("hello world")

    // fmt.Println("baris ini tidak akan dieksekusi")
}
```

Mari kita praktekan kode di atas. Siapkan file program baru dalam project folder (bisa buat project baru atau gunakan project yang sudah ada). Kemudian isi file dengan kode di atas, lalu jalankan.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdzbmY4kue4X8H6hkYmBFI_o3DVBKOicVQem7y2g5nF0gr5yZKDa26I7B2dAYwhsgeMuQhQtMU0Pv5z5c9jE94qAyLTVwFjAtgWix8G8g7WeYRY-ao2o2WMGI3cX8L9GhTY6O21IsDi_quzygXf0gXnZhI7?key=d3s-vJLBsYtwvRvGfZhdnw)**
Hasilnya hanya tulisan **hello world** saja yang muncul di layar, karena semua yang di awali tanda double slash `//` diabaikan oleh compiler.

## A.8.2. Komentar  _Multiline_

Komentar yang cukup panjang akan lebih rapi jika ditulis menggunakan teknik komentar multiline. Ciri dari komentar jenis ini adalah penulisannya diawali dengan tanda  `/*`  dan diakhiri  `*/`.

```
/*
    komentar kode
    menampilkan pesan hello world
*/
fmt.Println("hello world")

// fmt.Println("baris ini tidak akan dieksekusi")
```
Sifat komentar ini sama seperti komentar inline, yaitu sama-sama diabaikan oleh compiler.