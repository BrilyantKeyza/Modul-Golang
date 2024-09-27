---
sidebar_position: 28
---

# A.28. Any / interface{} / Interface Kosong


Interface kosong atau  _empty interface_  yang dinotasikan dengan  `interface{}`  atau  `any`, merupakan tipe data yang sangat spesial karena variabel bertipe ini bisa menampung segala jenis data, baik itu numerik, string, bahkan array, pointer, apapun.

> Dalam konsep pemrograman umum, konsep variabel yang bisa menampung banyak jenis tipe data disebut dengan  **dynamic typing**.

## A.28.1. Penggunaan  `any`  /  `interface{}`

`any`  atau  `interface{}`  merupakan tipe data, sehingga cara penggunaannya sama seperti tipe data pada umumnya, perbedaannya pada variabel bertipe ini nilainya bisa diisi dengan apapun. Contoh:

```
package main

import "fmt"

func main() {
    var secret interface{}

    secret = "ethan hunt"
    fmt.Println(secret)

    secret = []string{"apple", "manggo", "banana"}
    fmt.Println(secret)

    secret = 12.4
    fmt.Println(secret)
}
```

Keyword  `interface`  seperti yang kita tau, digunakan untuk pembuatan interface. Tetapi ketika ditambahkan kurung kurawal (`{}`) di belakang-nya (menjadi  `interface{}`), maka kegunaannya akan berubah, yaitu sebagai tipe data.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeWgwhjjqOeFuI4dhLHaVWmMusNS0190i-vC7m2HoW-dEVXH4Z2-t_hob3HjmkwrBtz8lalUnsfR6OD3oizvrcHSUqr6oTUvhzlE8f_u2wEkUyC_YEwqw72Rtj0GvpzjfxazfCISHtNOBmDG6muoS6xjU8?key=d3s-vJLBsYtwvRvGfZhdnw)**

Agar tidak bingung, coba perhatikan kode berikut.

```
var data map[string]interface{}

data = map[string]interface{}{
    "name":      "ethan hunt",
    "grade":     2,
    "breakfast": []string{"apple", "manggo", "banana"},
}
```

Pada kode di atas, disiapkan variabel  `data`  dengan tipe  `map[string]interface{}`, yaitu sebuah koleksi dengan key bertipe  `string`  dan nilai bertipe interface kosong  `interface{}`.

Kemudian variabel tersebut di-inisialisasi, ditambahkan lagi kurung kurawal setelah keyword deklarasi untuk kebutuhan pengisian data,  `map[string]interface{}{ /* data */ }`.

Dari situ terlihat bahwa  `interface{}`  bukanlah sebuah objek, melainkan tipe data.

## A.28.2. Type Alias  `Any`

Tipe  `any`  merupakan alias dari  `interface{}`, keduanya adalah sama.

```
var data map[string]any

data = map[string]any{
    "name":      "ethan hunt",
    "grade":     2,
    "breakfast": []string{"apple", "manggo", "banana"},
}
```

## A.28.3. Casting Variabel Any / Interface Kosong

Variabel bertipe  `interface{}`  bisa ditampilkan ke layar sebagai  `string`  dengan memanfaatkan fungsi print, seperti  `fmt.Println()`. Tapi perlu diketahui bahwa nilai yang dimunculkan tersebut bukanlah nilai asli, melainkan bentuk text dari nilai aslinya.

Hal ini penting diketahui, karena untuk melakukan operasi yang membutuhkan nilai asli pada variabel yang bertipe  `interface{}`, diperlukan casting ke tipe aslinya. Contoh seperti pada kode berikut.

```
package main

import "fmt"
import "strings"

func main() {
    var secret interface{}

    secret = 2
    var number = secret.(int) * 10
    fmt.Println(secret, "multiplied by 10 is :", number)

    secret = []string{"apple", "manggo", "banana"}
    var gruits = strings.Join(secret.([]string), ", ")
    fmt.Println(gruits, "is my favorite fruits")
}
```
Pertama, variabel  `secret`  menampung nilai bertipe numerik. Ada kebutuhan untuk mengalikan nilai yang ditampung variabel tersebut dengan angka  `10`. Maka perlu dilakukan casting ke tipe aslinya, yaitu  `int`, setelahnya barulah nilai bisa dioperasikan, yaitu  `secret.(int) * 10`.

Pada contoh kedua,  `secret`  berisikan array string. Kita memerlukan string tersebut untuk digabungkan dengan pemisah tanda koma. Maka perlu di-casting ke  `[]string`  terlebih dahulu sebelum bisa digunakan di  `strings.Join()`, contohnya pada  `strings.Join(secret.([]string), ", ")`.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcN4nto_ZoLRPiugUhVoBbnfeB5qkqWoTmu8vZ0e5atynrE09MAZOMqlrIrm3EAddzvFjw6cu-gaTsenB3JINa3dlWEXSVAoxgxIZvpMM1ts_avFxcvLBBa-8N4Zj-tqmuyLXneGQ8rV-WlpMJayGJaQcQi?key=d3s-vJLBsYtwvRvGfZhdnw)**

Teknik casting pada `any` disebut dengan **type assertions**.

## A.28.4. Casting Variabel Interface Kosong Ke Objek Pointer

Variabel  `interface{}`  bisa menyimpan data apa saja, termasuk data objek, pointer, ataupun gabungan keduanya. Di bawah ini merupakan contoh penerapan interface untuk menampung data objek pointer.

```
type person struct {
    name string
    age  int
}

var secret interface{} = &person{name: "wick", age: 27}
var name = secret.(*person).name
fmt.Println(name)
```

Variabel  `secret`  dideklarasikan bertipe  `interface{}`  menampung referensi objek cetakan struct  `person`. Cara casting dari  `interface{}`  ke struct pointer adalah dengan menuliskan nama struct-nya dan ditambahkan tanda asterisk (`*`) di awal, contohnya seperti  `secret.(*person)`. Setelah itu barulah nilai asli bisa diakses.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcGQX1zQd8ULR3Tgho9qDNl-sP97yAzzNOuvcnTZyTQDTB7l-cy2kA2bfktBs-OA9vNG5iHr1vYQyMIQALjvOzJ9iOrpHkkJ9KNjc_kf4JqnidR8axbHy9_-z4Wnno9HvHvcKeLoPvw2AIpoV2qNAlDszmG?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.28.5. Kombinasi Slice,  `map`, dan  `interface{}`

Tipe  `[]map[string]interface{}`  adalah salah satu tipe yang paling sering digunakan untuk menyimpan sekumpulan data berbasis  _key-value_. Tipe tersebut merupakan alternatif dari slice struct.

Pada contoh berikut, variabel  `person`  dideklarasikan berisi data slice  `map`  berisikan 2 item dengan key adalah  `name`  dan  `age`.

```
var person = []map[string]interface{}{
    {"name": "Wick", "age": 23},
    {"name": "Ethan", "age": 23},
    {"name": "Bourne", "age": 22},
}

for _, each := range person {
    fmt.Println(each["name"], "age is", each["age"])
}
```

Dengan memanfaatkan slice dan  `interface{}`, kita bisa membuat data array yang isinya adalah bisa apa saja. Silakan perhatikan contoh berikut.

```
var fruits = []interface{}{
    map[string]interface{}{"name": "strawberry", "total": 10},
    []string{"manggo", "pineapple", "papaya"},
    "orange",
}

for _, each := range fruits {
    fmt.Println(each)
}
``` 