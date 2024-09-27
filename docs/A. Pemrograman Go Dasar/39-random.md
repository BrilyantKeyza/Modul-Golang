---
sidebar_position: 39
---

# A.39. Random


Pada chapter ini kita akan belajar pemanfaatan package `math/rand` untuk pembuatan data acak atau random.

## A.39.1. Definisi

Random Number Generator (RNG) merupakan sebuah perangkat (bisa software, bisa hardware) yang menghasilkan data deret/urutan angka yang sifatnya acak.

RNG bisa berupa hardware yang murni bisa menghasilkan data angka acak, atau bisa saja sebuah  [pseudo-random](https://en.wikipedia.org/wiki/Pseudorandom_number_generator)  yang menghasilkan deret angka-angka yang  **terlihat acak**  tetapi sebenarnya tidak benar-benar acak. Deret angka tersebut sebenarnya merupakan hasil kalkulasi algoritma deterministik dan probabilitas. Jadi untuk pseudo-random ini, asalkan kita tau  _state_-nya maka kita akan bisa menebak hasil deret angka random-nya.

Dalam per-randoman-duniawi terdapat istilah  **seed**  atau titik mulai (_starting point_). Seed ini digunakan oleh RNG untuk pembuatan angka random.

Sedikit ilustrasi mengenai korelasi antara seed dengan RNG, agar lebih jelas.

-   Dimisalkan saya menggunakan seed yaitu angka  `10`, maka ketika fungsi RNG dijalankan untuk pertama kalinya, output angka yang dihasilkan pasti  `5221277731205826435`. Angka random tersebut pasti  _fix_  dan akan selalu menjadi hasil pertama ketika seed yang digunakan adalah angka  `10`.
-   Misalnya lagi, fungsi RNG di-eksekusi untuk ke-dua kalinya, maka angka random kedua yang dihasilkan adalah pasti  `3852159813000522384`. Dan seterusnya.
-   Misalkan lagi, fungsi RNG di-eksekusi lagi, maka angka random ketiga pasti  `8532807521486154107`.
-   Jadi untuk seed angka  `10`, akan selalu menghasilkan angka random ke-1:  `5221277731205826435`, ke-2:  `3852159813000522384`, ke-3  `8532807521486154107`. Meskipun fungsi random dijalankan di program yang berbeda, di waktu yang berbeda, di environment yang berbeda, jika seed adalah  `10`  maka deret angka random yang dihasilkan pasti sama seperti contoh di atas.


## A.39.2. Package  `math/rand`

Go menyediakan package  `math/rand`, isinya banyak sekali API untuk keperluan pembuatan angka random. Package ini mengadopsi  **PRNG**  atau  _pseudo-random_  number generator. Deret angka random yang dihasilkan sangat tergantung dengan angka  **seed**  yang digunakan.

Cara penggunaan package ini sangat mudah, cukup import  `math/rand`, lalu tentukan nilai seed, kemudian panggil fungsi untuk generate angka random-nya. Lebih jelasnya silakan cek contoh berikut.

```
package main

import (
    "fmt"
    "math/rand"
)

func main() {
    randomizer := rand.New(rand.NewSource(10))
    fmt.Println("random ke-1:", randomizer.Int()) // 5221277731205826435
    fmt.Println("random ke-2:", randomizer.Int()) // 3852159813000522384
    fmt.Println("random ke-3:", randomizer.Int()) // 8532807521486154107
}
```
Fungsi  `rand.New(rand.NewSource(x))`  digunakan untuk membuat object randomizer sekaligus penentuan nilai seed-nya. Dari object randomizer, method  `Int()`  bisa diakses, gunanya untuk generate angka random dalam bentuk numerik bertipe  `int`. Statement  `randomizer.Int()`  ini setiap kali dipanggil akan menghasilkan angka berbeda, tapi jika diperhatikan angka-angka tersebut tidak berubah, pasti hanya angka-angka itu saja yang muncul.

Silakan coba sendiri kode di atas di local masing-masing, hasilnya pasti:

-   Angka random ke-1 akan selalu  `5221277731205826435`
-   Angka random ke-2 akan selalu  `3852159813000522384`
-   Angka random ke-3 akan selalu  `8532807521486154107`

Jika perlu jalankan program di atas beberapa kali, hasilnya selalu sama untuk angka random ke-1, ke-2, dan seterusnya.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXczd1pxL0zQFESEXP9OB7d4gorCppOycO4K_war1G80oqXjKVNAHvnkPMnq1WW2zXuporQ2FPnEXSgX4vFg3jca38o4KjtY_XAd4LlpyzX2o25tpm8Gah0eePkmod-4s6nXQ_5f8DerNqHve9E5SCxssLNh?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.39.3. Unique Seed

Lalu bagaimana cara agar angka yang dihasilkan selalu berbeda setiap kali dipanggil? Apakah harus set ulang seed-nya? Jangan, karena kalau seed di-set ulang maka urutan deret random akan berubah. Seed hanya perlu di set sekali di awal. Lalu apa solusi yang benar?

Jadi begini, setiap kali  `randomizer.Int()`  dipanggil, hasilnya itu selalu berbeda, tapi sangat bisa diprediksi jika kita tau seed-nya. Ada cara agar angka random yang dihasilkan tidak berulang-ulang seperti yang ada di contoh, caranya yaitu dengan menggunakan angka unik  _unique_/unik sebagai seed, contohnya seperti angka  [unix nano](https://en.wikipedia.org/wiki/GNU_nano)  yang didapat dari informasi waktu sekarang.

Coba modifikasi program dengan kode berikut, lalu jalankan ulang. Jangan lupa meng-import package  `time`  ya.

```
randomizer := rand.New(rand.NewSource(time.Now().UTC().UnixNano()))
fmt.Println("random ke-1:", randomizer.Int())
fmt.Println("random ke-2:", randomizer.Int())
fmt.Println("random ke-3:", randomizer.Int())
```

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdl41fiKY_WfiLAwSh21yY0jb_D8XVUI53-mK7Lx8UW2MMpYGDChr6QPHCWtyEJMPPu8mAn3VgFxf4zUsFvgZ-UQd2VSGyAsVlXCUDdMiesKKR7_KYZX03RUSjmMJnA9uue6xtzK0t44Ju9-9S0VVkdFWH1?key=d3s-vJLBsYtwvRvGfZhdnw)**

Bisa dilihat, setiap program dieksekusi angka random nya selalu berbeda, hal ini karena seed yang digunakan pasti berbeda di setiap eksekusi program. Disitu seed yang digunakan adalah data numerik unix nano dari informasi waktu sekarang.

## A.39.4. Random Tipe Data Numerik Lainnya

Di dalam package  `math/rand`, ada banyak fungsi untuk generate angka random. Method  `Int()`  milik object randomizer hanya salah satu dari fungsi yang tersedia di dalam package tersebut, yang gunanya adalah menghasilkan angka random bertipe  `int`.

Selain itu, ada juga  `randomizer.Float32()`  yang menghasilkan angka random bertipe  `float32`. Ada juga  `randomizer.Uint32()`  yang menghasilkan angka random bertipe  _unsigned_  int, dan lainnya.

Contoh penerapan fungsi-fungsi tersebut:

```
randomizer := rand.New(rand.NewSource(time.Now().UTC().UnixNano()))
fmt.Println("random int:", randomizer.Int())
fmt.Println("random float32:", randomizer.Float32())
fmt.Println("random uint:", randomizer.Uint32())

```

lebih detailnya silakan merujuk ke  [https://golang.org/pkg/math/rand/](https://golang.org/pkg/math/rand/)

## A.39.5. Angka Random Index Tertentu

Gunakan  `randomizer.Intn(n)`  untuk mendapatkan angka random dengan batas  `0`  hingga  `n - 1`, contoh:  `randomizer.Intn(100)`  akan mengembalikan angka acak dari 0 hingga 99.

## A.39.6. Random Tipe Data String

Untuk menghasilkan data random string, ada banyak cara yang bisa diterapkan, salah satunya adalah dengan memafaatkan alfabet dan hasil random numerik.

```
var randomizer = rand.New(rand.NewSource(time.Now().UTC().UnixNano()))
var letters = []rune("abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ")

func randomString(length int) string {
    b := make([]rune, length)
    for i := range b {
        b[i] = letters[randomizer.Intn(len(letters))]
    }
    return string(b)
}

func main() {
    fmt.Println("random string 5 karakter:", randomString(5))
}
```

Dengan fungsi di atas kita bisa dengan mudah meng-generate string random dengan panjang karakter yang sudah ditentukan, misal  `randomString(10)`  akan menghasilkan random string 10 karakter.