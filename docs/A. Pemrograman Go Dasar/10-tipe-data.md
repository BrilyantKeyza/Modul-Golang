---
sidebar_position: 10
---

# A.10. Tipe Data


Go mengenal beberapa jenis tipe data, di antaranya adalah tipe data numerik (desimal & non-desimal), string, dan boolean.

Pada pembahasan-pembahasan sebelumnya secara tak sadar kita sudah mengaplikasikan beberapa tipe data, diantaranya ada  `string`  dan tipe numerik  `int`.

Pada chapter ini akan dijelaskan beberapa macam tipe data standar yang disediakan oleh Go, disertai juga contohnya.

## A.10.1. Tipe Data Numerik Non-Desimal

Tipe data numerik non-desimal atau  **non floating point**  di Go ada beberapa jenis. Secara umum ada 2 tipe data kategori ini yang perlu diketahui.

-   `uint`, tipe data untuk bilangan cacah (bilangan positif).
-   `int`, tipe data untuk bilangan bulat (bilangan negatif dan positif).

Kedua tipe data di atas kemudian dibagi lagi menjadi beberapa jenis, dengan pembagian berdasarkan lebar cakupan nilainya, detailnya bisa dilihat di tabel berikut.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf_lC3xDiwIaEF1R96cFp9d4tg1rew2TC8wg5z4S3kxiqX5uYh-qI7byK86peaw3Ci8c0qeU5P8e8dpt3KPrQ89JpRoFzfnQRePWwnVxbHJaWDr1HefN9eLeFLePPUcfA_SWyXiDNpSS6XRU15roU5JTLsN?key=d3s-vJLBsYtwvRvGfZhdnw)**
Dianjurkan untuk tidak sembarangan dalam menentukan tipe data variabel, sebisa mungkin tipe yang dipilih harus disesuaikan dengan nilainya, karena efeknya adalah ke alokasi memori variabel. Pemilihan tipe data yang tepat akan membuat pemakaian memori lebih optimal, tidak berlebihan.

```
var positiveNumber uint8 = 89
var negativeNumber = -1243423644

fmt.Printf("bilangan positif: %d\n", positiveNumber)
fmt.Printf("bilangan negatif: %d\n", negativeNumber)
```

Variabel  `positiveNumber`  bertipe  `uint8`  dengan nilai awal  `89`. Sedangkan variabel  `negativeNumber`  dideklarasikan dengan nilai awal  `-1243423644`. Compiler secara cerdas akan menentukan tipe data variabel tersebut sebagai  `int32`  (karena angka tersebut masuk ke cakupan tipe data  `int32`).

String format  `%d`  pada  `fmt.Printf()`  digunakan untuk memformat data numerik non-desimal.

## A.10.2. Tipe Data Numerik Desimal

Tipe data numerik desimal yang perlu diketahui ada 2,  `float32`  dan  `float64`. Perbedaan kedua tipe data tersebut berada di lebar cakupan nilai desimal yang bisa ditampung. Untuk lebih jelasnya bisa merujuk ke spesifikasi  [IEEE-754 32-bit floating-point numbers](http://www.h-schmidt.net/FloatConverter/IEEE754.html).

```
var decimalNumber = 2.62

fmt.Printf("bilangan desimal: %f\n", decimalNumber)
fmt.Printf("bilangan desimal: %.3f\n", decimalNumber)
```
Pada kode di atas, variabel `decimalNumber` akan memiliki tipe data `float32`, karena nilainya berada di cakupan tipe data tersebut.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdeCIpSCmB3g2hUwnm1ABpGTeyUbJL_EuRTqdZQI_0Ll-nXJ06uGxsTXp0P9UdHX1s7lRUUJsxdFC0MhFDthIJAM7FBALc1JldfJKxMXekhkMI-0Mh_23zu9MrH_b5ptRGa-jmintWYMCnRKOeSfeG-p34i?key=d3s-vJLBsYtwvRvGfZhdnw)**
String format `%f` digunakan untuk memformat data numerik desimal menjadi string. Digit desimal yang akan dihasilkan adalah **6 digit**. Pada contoh di atas, hasil format variabel `decimalNumber` adalah `2.620000`. Jumlah digit yang muncul bisa dikontrol menggunakan `%.nf`, tinggal ganti `n` dengan angka yang diinginkan. Contoh: `%.3f` maka akan menghasilkan 3 digit desimal, `%.10f` maka akan menghasilkan 10 digit desimal.

## A.10.3. Tipe Data  `bool`  (Boolean)

Tipe data  `bool`  berisikan hanya 2 variansi nilai,  `true`  dan  `false`. Tipe data ini biasa dimanfaatkan dalam seleksi kondisi dan perulangan (yang nantinya akan kita bahas pada  A.13. Seleksi Kondisi dan A.14. Perulangan)
```
var exist bool = true
fmt.Printf("exist? %t \n", exist)
```

Gunakan  `%t`  untuk memformat data  `bool`  menggunakan fungsi  `fmt.Printf()`.

## A.10.4. Tipe Data  `string`

Ciri khas dari tipe data string adalah nilainya di apit oleh tanda  _quote_  atau petik dua (`"`). Contoh penerapannya:

```
var message string = "Halo"
fmt.Printf("message: %s \n", message)
```
Selain menggunakan tanda quote, deklarasi string juga bisa dengan tanda _grave accent/backticks_ (`` ` ``), tanda ini terletak di sebelah kiri tombol 1. Keistimewaan string yang dideklarasikan menggunakan backtics adalah membuat semua karakter di dalamnya **tidak di escape**, termasuk `\n`, tanda petik dua dan tanda petik satu, baris baru, dan lainnya. Semua akan terdeteksi sebagai string.

```
var message = `Nama saya "John Wick".
Salam kenal.
Mari belajar "Golang".`

fmt.Println(message)
```

Ketika dijalankan, output akan muncul sama persis sesuai nilai variabel `message` di atas. Tanda petik dua akan muncul, baris baru juga muncul, sama persis.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdXae_GdMJ0ip_hlQUZD9Mrsry2sPzKTpIbjoi-Om0QImTcjSl5M6NeWDrj0KHvVPKhcwracdSfMRndJvLBP5c_YMtxS5eFeNDqxaYUUXbxPhLo38W7kTO-Ow_RBdWsGECbARkLbLtcIkovee2CsZ41SSDh?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.10.5. Nilai  `nil`  & Zero Value

`nil`  bukan merupakan tipe data, melainkan sebuah nilai. Variabel yang isi nilainya  `nil`  berarti memiliki nilai kosong.

Semua tipe data yang sudah dibahas di atas memiliki zero value (nilai default tipe data). Artinya meskipun variabel dideklarasikan dengan tanpa nilai awal, tetap akan ada nilai default-nya.

-   Zero value dari  `string`  adalah  `""`  (string kosong).
-   Zero value dari  `bool`  adalah  `false`.
-   Zero value dari tipe numerik non-desimal adalah  `0`.
-   Zero value dari tipe numerik desimal adalah  `0.0`.

Selain tipe data yang disebutkan di atas, ada juga tipe data lain yang zero value-nya adalah  `nil`.  `Nil`  merepresentasikan nilai kosong, benar-benar kosong.  `nil`  tidak bisa digunakan pada tipe data yang sudah dibahas di atas.

Beberapa tipe data yang bisa di-set nilainya dengan  `nil`, di antaranya:

-   pointer
-   tipe data fungsi
-   slice
-   `map`
-   `channel`
-   interface kosong atau  `any`  (yang merupakan alias dari  `interface{}`)

Nantinya kita akan sering bertemu dengan nilai  `nil`  setelah masuk pada pembahasan-pembahasan tersebut.
