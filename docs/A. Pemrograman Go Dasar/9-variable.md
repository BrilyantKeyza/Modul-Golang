---
sidebar_position: 9
---

# A.9. Variabel


Go mengadopsi dua jenis penulisan variabel, yaitu yang dituliskan tipe data-nya dan yang tidak. Kedua cara tersebut valid dan tujuannya sama yaitu untuk deklarasi variabel, pembedanya hanya pada cara penulisannya saja.

Pada chapter ini akan dikupas tuntas tentang macam-macam cara deklarasi variabel.

## A.9.1. Deklarasi Variabel Beserta Tipe Data

Go memiliki aturan cukup ketat dalam hal penulisan variabel. Ketika deklarasi, tipe data yg digunakan harus dituliskan juga. Istilah dari metode deklarasi variabel ini adalah  **manifest typing**.

Berikut adalah contoh cara pembuatan variabel yang tipe datanya harus ditulis. Silakan tulis pada project baru atau pada project yang sudah ada, bebas. Pastikan pada setiap pembuatan project baru untuk tidak lupa menginisialisasi project menggunakan command  `go mod init <nama-project>`.

```
package main

import "fmt"

func main() {
    var firstName string = "john"

    var lastName string
    lastName = "wick"

    fmt.Printf("halo %s %s!\n", firstName, lastName)
}
```

Keyword  `var`  di atas digunakan untuk deklarasi variabel, contohnya bisa dilihat pada  `firstName`  dan  `lastName`.

Nilai variabel  `firstName`  diisi langsung ketika deklarasi, berbeda dibanding  `lastName`  yang nilainya diisi setelah baris kode deklarasi, hal seperti ini diperbolehkan di Go.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfnUh0oEsHeJtMN9mgiDZxTx-ofa3Pi3y7P-8uO0Yupi7Q4yaBppmRys_Z8Lus7WTlOoCwpULCCdBRHARF4-iggfVJ1HzVIgUCGDF5ka5xthy-wIr_mV6utE-vtTbipxoC-i-8YQstTJyfbv4OyNPKCLn5A?key=d3s-vJLBsYtwvRvGfZhdnw)**
## A.9.2. Deklarasi Variabel Menggunakan Keyword  `var`

Pada kode di atas bisa dilihat bagaimana sebuah variabel dideklarasikan dan diisi nilainya. Keyword  `var`  digunakan untuk membuat variabel baru.

Skema penggunaan keyword var:
```
var <nama-variabel> <tipe-data>
var <nama-variabel> <tipe-data> = <nilai>
```
Contoh:

```
var lastName string
var firstName string = "john"
```
Nilai variabel bisa di-isi langsung pada saat deklarasi variabel.

#### ◉ Penggunaan Fungsi  `fmt.Printf()`

Fungsi ini digunakan untuk menampilkan output dalam bentuk tertentu. Kegunaannya sama seperti fungsi  `fmt.Println()`, hanya saja struktur outputnya didefinisikan di awal.

Perhatikan bagian  `"halo %s %s!\n"`, karakter  `%s`  di situ akan diganti dengan data  `string`  yang berada di parameter ke-2, ke-3, dan seterusnya.

Contoh lain, ketiga baris kode berikut ini akan menghasilkan output yang sama, meskipun cara penulisannya berbeda.

```
fmt.Printf("halo john wick!\n")
fmt.Printf("halo %s %s!\n", firstName, lastName)
fmt.Println("halo", firstName, lastName + "!")
```

Tanda plus (`+`) jika digunakan untuk penghubung 2 data string fungsinya adalah untuk operasi penggabungan string atau  _string concatenation_.

Fungsi  `fmt.Printf()`  tidak menghasilkan baris baru di akhir text, oleh karena itu digunakanlah literal  _newline_  yaitu  `\n`, untuk memunculkan baris baru di akhir. Hal ini sangat berbeda jika dibandingkan dengan fungsi  `fmt.Println()`  yang secara otomatis menghasilkan new line (baris baru) di akhir.

## A.9.3. Deklarasi Variabel Tanpa Tipe Data
Selain _manifest typing_, Go juga mengadopsi konsep **type inference**, yaitu metode deklarasi variabel yang tipe data-nya diketahui secara otomatis dari data/nilai variabel. Cara ini kontradiktif jika dibandingkan dengan cara pertama. Dengan metode jenis ini, keyword `var` dan tipe data tidak perlu ditulis.

```
var firstName string = "john"
lastName := "wick"

fmt.Printf("halo %s %s!\n", firstName, lastName)
```
Variabel `lastName` dideklarasikan dengan menggunakan metode type inference. Penandanya tipe data tidak dituliskan pada saat deklarasi. Pada penggunaan metode ini, operand `=` harus diganti dengan `:=` dan keyword `var` dihilangkan.

Tipe data `lastName` secara otomatis akan ditentukan menyesuaikan value atau nilai-nya. Jika nilainya adalah berupa `string` maka tipe data variabel adalah `string`. Pada contoh di atas, nilainya adalah string `"wick"`.

Diperbolehkan untuk tetap menggunakan keyword  `var`  pada saat deklarasi meskipun tanpa menuliskan tipe data, dengan ketentuan tidak menggunakan tanda  `:=`, melainkan tetap menggunakan  `=`.

```
// menggunakan var, tanpa tipe data, menggunakan perantara "="
var firstName = "john"

// tanpa var, tanpa tipe data, menggunakan perantara ":="
lastName := "wick"
```
Kedua deklarasi di atas maksudnya sama. Silakan pilih sesuai preferensi.

Tanda  `:=`  hanya digunakan sekali di awal pada saat deklarasi. Untuk assignment nilai selanjutnya harus menggunakan tanda  `=`, contoh:

```
lastName := "wick"
lastName = "ethan"
lastName = "bourne"
```
>Deklarasi menggunakan `:=` hanya bisa dilakukan di dalam blok fungsi, misalnya dalam blok fungsi `main()`

## A.9.4. Deklarasi Multi Variabel

Go mendukung metode deklarasi banyak variabel secara bersamaan, caranya dengan menuliskan variabel-variabel-nya dengan pembatas tanda koma (`,`). Untuk pengisian nilainya-pun diperbolehkan secara bersamaan.

```
var first, second, third string
first, second, third = "satu", "dua", "tiga"
```
Pengisian nilai juga bisa dilakukan bersamaan pada saat deklarasi. Caranya dengan menuliskan nilai masing-masing variabel berurutan sesuai variabelnya dengan pembatas koma (`,`).

```
var fourth, fifth, sixth string = "empat", "lima", "enam"
```
Kalau ingin lebih ringkas:

```
seventh, eight, ninth := "tujuh", "delapan", "sembilan"
```
Dengan menggunakan teknik type inference, deklarasi multi variabel bisa dilakukan untuk variabel-variabel yang tipe data satu sama lainnya berbeda.

```
one, isFriday, twoPointTwo, say := 1, true, 2.2, "hello"
```

## A.9.5. Variabel Underscore  `_`

Go memiliki aturan unik yang jarang dimiliki bahasa lain, yaitu tidak boleh ada satupun variabel yang menganggur. Artinya, semua variabel yang dideklarasikan harus digunakan. Jika ada variabel yang tidak digunakan tapi dideklarasikan, error akan muncul pada saat kompilasi dan program tidak akan bisa di-run.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc_EOswhCUewp1KW6piVhQv10oLyjH1imnl5OXIkVi2VHocMPW1u4CsPMHlkzgKYnXn9Px2Cw0Icq0AsEIhqLWdZoHkd5arysmJvhdVPZDqCu8PqpGYp2JCzzwr1pTVq4ox-z1nBBszsAAJh_3KY5bb43y7?key=d3s-vJLBsYtwvRvGfZhdnw)**
_Underscore_ (`_`) adalah _reserved variable_ yang bisa dimanfaatkan untuk menampung nilai yang tidak dipakai. Bisa dibilang variabel ini merupakan keranjang sampah.
```
_ = "belajar Golang"
_ = "Golang itu mudah"
name, _ := "john", "wick"
```
Pada contoh di atas, variabel  `name`  akan berisikan text  `john`, sedang nilai  `wick`  ditampung oleh variabel underscore, menandakan bahwa nilai tersebut tidak akan digunakan.

Variabel underscore adalah  _predefined_, jadi tidak perlu menggunakan  `:=`  untuk pengisian nilai, cukup dengan  `=`  saja. Namun khusus untuk pengisian nilai multi variabel yang dilakukan dengan metode type inference, boleh di dalamnya terdapat variabel underscore.

Biasanya variabel underscore sering dimanfaatkan untuk menampung nilai balik fungsi yang tidak digunakan.

Perlu diketahui, bahwa isi variabel underscore tidak dapat ditampilkan. Data yang sudah masuk variabel tersebut akan hilang. Ibarat variabel underscore ini seperti blackhole, objek apapun yang masuk ke dalamnya, akan terjebak selamanya di-dalam singularity dan tidak akan bisa keluar

## A.9.6. Deklarasi Variabel Menggunakan Keyword  `new`

Fungsi  `new()`  digunakan untuk membuat variabel  **pointer**  dengan tipe data tertentu. Nilai data default-nya akan menyesuaikan tipe datanya.

```
name := new(string)

fmt.Println(name)   // 0x20818a220
fmt.Println(*name)  // ""
```

Variabel  `name`  menampung data bertipe  **pointer string**. Jika ditampilkan yang muncul bukanlah nilainya melainkan alamat memori nilai tersebut (dalam bentuk notasi heksadesimal). Untuk menampilkan nilai aslinya, variabel tersebut perlu di-**dereference**  terlebih dahulu, caranya dengan menuliskan tanda asterisk (`*`) sebelum nama variabel.

Mungkin untuk sekarang banyak yang akan bingung tentang apa itu pointer, namun tak apa, karena nantinya pada chapter A.23. Pointer akan dikupas habis topik tersebut.

## A.9.7. Deklarasi Variabel Menggunakan Keyword  `make`

Fungsi  `make()`  ini hanya bisa digunakan untuk pembuatan beberapa jenis variabel saja, yaitu:

-   channel
-   slice
-   map

Nantinya kita akan bahas lebih detail ketika sudah masuk ke pembahasan masing-masing poin tersebut.