---
sidebar_position: 13
---

# A.13. Seleksi Kondisi


Seleksi kondisi digunakan untuk mengontrol alur eksekusi flow program. Analoginya mirip seperti fungsi rambu lalu lintas di jalan raya. Kapan kendaraan diperbolehkan melaju dan kapan harus berhenti diatur oleh rambu tersebut. Seleksi kondisi pada program juga kurang lebih sama, kapan sebuah blok kode dieksekusi dikontrol.

Yang dijadikan acuan oleh seleksi kondisi adalah nilai bertipe  `bool`, bisa berasal dari variabel, ataupun hasil operasi perbandingan. Nilai tersebut menentukan blok kode mana yang akan dieksekusi.

Go memiliki 2 macam keyword untuk seleksi kondisi, yaitu  **if else**  dan  **switch**. Pada chapter ini kita akan mempelajari keduanya.

>Go tidak mendukung seleksi kondisi menggunakan **ternary**.  
Statement seperti `var data = (isExist ? "ada" : "tidak ada")` adalah invalid dan menghasilkan error.


## A.13.1. Seleksi Kondisi Menggunakan Keyword  `if`,  `else if`, &  `else`

Cara penerapan if-else di Go sama seperti pada bahasa pemrograman lain. Yang membedakan hanya tanda kurungnya  _(parentheses)_, di Go tidak perlu ditulis. Kode berikut merupakan contoh penerapan seleksi kondisi if else, dengan jumlah kondisi 4 buah.
```
var point = 8

if point == 10 {
    fmt.Println("lulus dengan nilai sempurna")
} else if point > 5 {
    fmt.Println("lulus")
} else if point == 4 {
    fmt.Println("hampir lulus")
} else {
    fmt.Printf("tidak lulus. nilai anda %d\n", point)
}
```
Dari ke-empat kondisi di atas, yang terpenuhi adalah `if point > 5`, karena nilai variabel `point` memang lebih besar dari `5`. Maka blok kode tepat di bawah kondisi tersebut akan dieksekusi (blok kode ditandai kurung kurawal buka dan tutup), hasilnya text `"lulus"` muncul sebagai output.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcheChqFK9j349gbyUl2elG0AYQdZm8iBT-yFarh8kNfmw4AjSV4StpPZ5XQr6R-KRPhvP5x79ZGcIqAnPT5GhuQHtyn4ISOcj7RPVjr2JoZ8q02-BoV-GMZ06XYbArObFxC0RFxoMw-cjBfVHZPLoXnOK6?key=d3s-vJLBsYtwvRvGfZhdnw)**
Penulisan if else Go diawali dengan keyword `if` kemudian diikuti nilai seleksi kondisi dan blok kode ketika kondisi terpenuhi. Ketika kondisinya tidak terpenuhi akan blok kode `else` dipanggil (jika blok kode `else` tersebut ada). Ketika ada banyak kondisi, gunakan `else if`.

## A.13.2. Variabel Temporary Pada  `if`  -  `else`

Variabel temporary adalah variabel yang hanya bisa digunakan pada deretan blok seleksi kondisi di mana ia ditempatkan. Penggunaan variabel ini membawa beberapa manfaat, antara lain:

-   Scope atau cakupan variabel jelas, hanya bisa digunakan pada blok seleksi kondisi itu saja
-   Kode menjadi lebih rapi
-   Ketika nilai variabel tersebut didapat dari sebuah komputasi, perhitungan tidak perlu dilakukan di dalam blok masing-masing kondisi.

```
var point = 8840.0

if percent := point / 100; percent >= 100 {
    fmt.Printf("%.1f%s perfect!\n", percent, "%")
} else if percent >= 70 {
    fmt.Printf("%.1f%s good\n", percent, "%")
} else {
    fmt.Printf("%.1f%s not bad\n", percent, "%")
}
```
Variabel `percent` nilainya didapat dari hasil perhitungan, dan hanya bisa digunakan di deretan blok seleksi kondisi itu saja yang mencakup blok `if`, `else if`, dan `else`.


>Deklarasi variabel temporary hanya bisa dilakukan lewat metode type inference yang menggunakan tanda `:=`. Penggunaan keyword `var` di situ tidak diperbolehkan karena menyebabkan error.


## A.13.3. Seleksi Kondisi Menggunakan Keyword  `switch`  -  `case`

Switch merupakan seleksi kondisi yang sifatnya fokus pada satu variabel, lalu kemudian di-cek nilainya. Contoh sederhananya seperti penentuan apakah nilai variabel  `x`  adalah:  `1`,  `2`,  `3`, atau lainnya.

```
var point = 6

switch point {
case 8:
    fmt.Println("perfect")
case 7:
    fmt.Println("awesome")
default:
    fmt.Println("not bad")
}
```

Pada kode di atas, tidak ada kondisi atau  `case`  yang terpenuhi karena nilai variabel  `point`  tetap  `6`. Ketika hal seperti ini terjadi, blok kondisi  `default`  dipanggil. Bisa dibilang bahwa  `default`  merupakan  `else`  dalam sebuah switch.

Perlu diketahui, switch pada pemrograman Go memiliki perbedaan dibanding bahasa lain. Di Go, ketika sebuah case terpenuhi, tidak akan dilanjutkan ke pengecekan case selanjutnya, meskipun tidak ada keyword  `break`  di situ. Konsep ini berkebalikan dengan switch pada umumnya pemrograman lain (yang ketika sebuah case terpenuhi, maka akan tetap dilanjut mengecek case selanjutnya kecuali ada keyword  `break`).

## A.13.4. Pemanfaatan  `case`  Untuk Banyak Kondisi

Sebuah  `case`  dapat menampung banyak kondisi. Cara penerapannya yaitu dengan menuliskan nilai pembanding-pembanding variabel yang di-switch setelah keyword  `case`  dipisah tanda koma (`,`).

```
var point = 6

switch point {
case 8:
    fmt.Println("perfect")
case 7, 6, 5, 4:
    fmt.Println("awesome")
default:
    fmt.Println("not bad")
}
```

Kondisi  `case 7, 6, 5, 4:`  akan terpenuhi ketika nilai variabel  `point`  adalah 7 atau 6 atau 5 atau 4.

## A.13.5. Kurung Kurawal Pada Keyword  `case`  &  `default`

Tanda kurung kurawal (`{ }`) bisa diterapkan pada keyword  `case`  dan  `default`. Tanda ini opsional, boleh dipakai boleh tidak. Bagus jika dipakai pada blok kondisi yang di dalamnya ada banyak statement, dengannya kode akan terlihat lebih rapi.

Perhatikan kode berikut, bisa dilihat pada keyword  `default`  terdapat kurung kurawal yang mengapit 2 statement di dalamnya.

```
var point = 6

switch point {
case 8:
    fmt.Println("perfect")
case 7, 6, 5, 4:
    fmt.Println("awesome")
default:
    {
        fmt.Println("not bad")
        fmt.Println("you can be better!")
    }
}
```

## A.13.6. Switch Dengan Gaya  `if`  -  `else`

Uniknya di Go, switch bisa digunakan dengan gaya ala if-else. Nilai yang akan dibandingkan tidak dituliskan setelah keyword  `switch`, melainkan akan ditulis langsung dalam bentuk perbandingan dalam keyword  `case`.

Pada kode di bawah ini, kode program switch di atas diubah ke dalam gaya  `if-else`. Variabel  `point`  dihilangkan dari keyword  `switch`, lalu kondisi-kondisinya dituliskan di tiap  `case`.

```
var point = 6

switch {
case point == 8:
    fmt.Println("perfect")
case (point < 8) && (point > 3):
    fmt.Println("awesome")
default:
    {
        fmt.Println("not bad")
        fmt.Println("you need to learn more")
    }
}
```

## A.13.7. Penggunaan Keyword  `fallthrough`  Dalam  `switch`

Seperti yang sudah dijelaskan sebelumnya, bahwa switch pada Go memiliki perbedaan dengan bahasa lain. Ketika sebuah  `case`  terpenuhi, pengecekan kondisi tidak akan diteruskan ke case-case setelahnya.

Keyword  `fallthrough`  digunakan untuk memaksa proses pengecekan tetap diteruskan ke  `case`  selanjutnya dengan  **tanpa menghiraukan nilai kondisinya**, efeknya adalah case di pengecekan selanjutnya selalu dianggap  `true`  (meskipun aslinya bisa saja kondisi tersebut tidak terpenuhi, akan tetap dianggap  `true`).

```
var point = 6

switch {
case point == 8:
    fmt.Println("perfect")
case (point < 8) && (point > 3):
    fmt.Println("awesome")
    fallthrough
case point < 5:
    fmt.Println("you need to learn more")
default:
    {
        fmt.Println("not bad")
        fmt.Println("you need to learn more")
    }
}
```

Di contoh, setelah pengecekan  `case (point < 8) && (point > 3)`  selesai, dilanjut ke pengecekan  `case point < 5`, karena ada  `fallthrough`  di situ. Dan kondisi  `case < 5`  tersebut dianggap  `true`  meskipun secara logika harusnya tidak terpenuhi.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf6jNa-fpD_4Cv5qK2307xVdVCKHD6lzKxHlEVPcrSR03_WhXlF3Zs76t9aeaAA3ecbqlCKfSmgEyMH3NyIDfmPjfCwRqQxOjj1PRfB9Mcn7rhh5WWXCwksx9G1yUHpQtsw57C4jvJZVj5w24USXpXYoQI?key=d3s-vJLBsYtwvRvGfZhdnw)**

Pada `case` dalam sebuah `switch`, diperbolehkan terdapat lebih dari satu `fallthrough`.

## A.13.8. Seleksi Kondisi Bersarang

Seleksi kondisi bersarang adalah seleksi kondisi, yang berada dalam seleksi kondisi, yang mungkin juga berada dalam seleksi kondisi, dan seterusnya. Seleksi kondisi bersarang bisa dilakukan pada  `if`  -  `else`,  `switch`, ataupun kombinasi keduanya.

```
var point = 10

if point > 7 {
    switch point {
    case 10:
        fmt.Println("perfect!")
    default:
        fmt.Println("nice!")
    }
} else {
    if point == 5 {
        fmt.Println("not bad")
    } else if point == 3 {
        fmt.Println("keep trying")
    } else {
        fmt.Println("you can do it")
        if point == 0 {
            fmt.Println("try harder!")
        }
    }
}
```