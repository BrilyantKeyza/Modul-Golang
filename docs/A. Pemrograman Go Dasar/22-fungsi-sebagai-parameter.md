---
sidebar_position: 22
---

# A.22. Fungsi Sebagai parameter


Pada chapter sebelumnya kita telah belajar tentang fungsi yang mengembalikan nilai balik berupa fungsi. Kali ini topiknya tidak kalah unik, yaitu tentang fungsi yang memiliki parameter sebuah fungsi.

Di Go, fungsi bisa dijadikan sebagai tipe data variabel, maka sangat memungkinkan untuk menjadikannya sebagai parameter.

## A.22.1. Penerapan Fungsi Sebagai Parameter

Cara membuat parameter fungsi adalah dengan langsung menuliskan skema fungsi nya sebagai tipe data. Contohnya bisa dilihat pada kode berikut.

```
package main

import "fmt"
import "strings"

func filter(data []string, callback func(string) bool) []string {
    var result []string
    for _, each := range data {
        if filtered := callback(each); filtered {
            result = append(result, each)
        }
    }
    return result
}
```

Parameter  `callback`  merupakan sebuah closure yang dideklarasikan bertipe  `func(string) bool`. Closure tersebut dipanggil di tiap perulangan dalam fungsi  `filter()`.

Fungsi  `filter()`  sendiri kita buat untuk filtering data array (yang datanya didapat dari parameter pertama), dengan kondisi filter bisa ditentukan sendiri. Di bawah ini adalah contoh pemanfaatan fungsi tersebut.

```
func main() {
    var data = []string{"wick", "jason", "ethan"}
    var dataContainsO = filter(data, func(each string) bool {
        return strings.Contains(each, "o")
    })
    var dataLenght5 = filter(data, func(each string) bool {
        return len(each) == 5
    })

    fmt.Println("data asli \t\t:", data)
    // data asli : [wick jason ethan]

    fmt.Println("filter ada huruf \"o\"\t:", dataContainsO)
    // filter ada huruf "o" : [jason]

    fmt.Println("filter jumlah huruf \"5\"\t:", dataLenght5)
    // filter jumlah huruf "5" : [jason ethan]
}
```
Ada cukup banyak hal yang terjadi di dalam tiap pemanggilan fungsi  `filter()`  di atas. Berikut adalah penjelasannya:

1.  Data array (yang didapat dari parameter pertama) akan di-looping.
2.  Di tiap perulangannya, closure  `callback`  dipanggil, dengan disisipkan data tiap elemen perulangan sebagai parameter.
3.  Closure  `callback`  berisikan kondisi filtering, dengan hasil bertipe  `bool`  yang kemudian dijadikan nilai balik dikembalikan.
4.  Di dalam fungsi  `filter()`  sendiri, ada proses seleksi kondisi (yang nilainya didapat dari hasil eksekusi closure  `callback`). Ketika kondisinya bernilai  `true`, maka data elemen yang sedang diulang dinyatakan lolos proses filtering.
5.  Data yang lolos ditampung variabel  `result`. Variabel tersebut dijadikan sebagai nilai balik fungsi  `filter()`.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfk603mXMX6L74lBr2LljfIhh2v8C1b1spoXWPkvpY6P6VXfKibVuaVQ1zvnTq2bMyPE__67TbAUyosSKEzbj8SifIYBXqfnTst-IiGq4Y_ZQBzBohWDoRr9y1vVcgAHgXHD1YQEhwv55YswrkclVTyCdT3?key=d3s-vJLBsYtwvRvGfZhdnw)**

Pada  `dataContainsO`, parameter kedua fungsi  `filter()`  berisikan statement untuk deteksi apakah terdapat substring  `"o"`  di dalam nilai variabel  `each`  (yang merupakan data tiap elemen), jika iya, maka kondisi filter bernilai  `true`, dan sebaliknya.

Pada contoh ke-2 (`dataLength5`), closure  `callback`  berisikan statement untuk deteksi jumlah karakter tiap elemen. Jika ada elemen yang jumlah karakternya adalah 5, berarti elemen tersebut lolos filter.

Memang butuh usaha ekstra untuk memahami pemanfaatan closure sebagai parameter fungsi. Tapi setelah paham, penerapan teknik ini pada kondisi yang tepat akan sangat berguna.

## A.22.2. Alias Skema Closure

Kita sudah mempelajari bahwa closure bisa dimanfaatkan sebagai tipe parameter, contohnya seperti pada fungsi  `filter()`. Di fungsi tersebut kebetulan skema tipe parameter closure-nya tidak terlalu panjang, hanya ada satu buah parameter dan satu buah nilai balik.

Untuk fungsi yang skema-nya cukup panjang, akan lebih baik jika menggunakan alias dalam pendefinisiannya, apalagi ketika ada parameter fungsi lain yang juga menggunakan skema yang sama, maka kita tidak perlu menuliskan skema panjang fungsi tersebut berulang-ulang.

Membuat alias fungsi berarti menjadikan skema fungsi tersebut menjadi tipe data baru. Caranya dengan menggunakan keyword  `type`. Contoh:

```
type FilterCallback func(string) bool

func filter(data []string, callback FilterCallback) []string {
    // ...
}
```

Skema  `func(string) bool`  diubah menjadi tipe dengan nama  `FilterCallback`. Tipe tersebut kemudian digunakan sebagai tipe data parameter  `callback`.

## A.22.3. Penjelasan tambahan

Di bawah ini merupakan penjelasan tambahan mengenai fungsi  `strings.Contains()`.

#### ◉ Penggunaan Fungsi  `string.Contains()`

Inti dari fungsi ini adalah untuk deteksi apakah sebuah substring adalah bagian dari string, jika iya maka akan bernilai  `true`, dan sebaliknya. Contoh penggunaannya:

```
var result = strings.Contains("Golang", "ang")
// true
```

Variabel  `result`  bernilai  `true`  karena string  `"ang"`  merupakan bagian dari string  `"Golang"`.