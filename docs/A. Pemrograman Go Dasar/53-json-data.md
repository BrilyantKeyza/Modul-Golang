---
sidebar_position: 53
---

# A.53. JSON Data


**JSON**  atau  _Javascript Object Notation_  adalah notasi standar penulisan data yang umum digunakan untuk komunikasi antar aplikasi/service. JSON sendiri sebenarnya merupakan subset dari  _javascript_.

Go menyediakan package  `encoding/json`  yang berisikan banyak fungsi untuk kebutuhan operasi json.

Pada chapter ini, kita akan belajar cara untuk konverstri string yang ditulis dalam format json menjadi objek Go, dan sebaliknya.

## A.53.1. Decode JSON Ke Variabel Objek Struct

Di Go, data json dituliskan sebagai  `string`. Dengan menggunakan  `json.Unmarshal`, json string bisa dikonversi menjadi bentuk objek, entah itu dalam bentuk  `map[string]interface{}`  ataupun objek struct.

Program berikut ini adalah contoh cara decoding json ke bentuk objek. Pertama import package yang dibutuhkan, lalu siapkan struct  `User`.

```
package main

import "encoding/json"
import "fmt"

type User struct {
    FullName string `json:"Name"`
    Age      int
}
```

Struct  `User`  ini nantinya digunakan untuk membuat variabel baru penampung hasil decode json string. Proses decode sendiri dilakukan lewat fungsi  `json.Unmarshal()`, dalam penggunaannya data json string dimasukan sebagai argument pemanggilan fungsi.

Contoh praktiknya bisa dilihat di bawah ini.
```
func main() {
    var jsonString = `{"Name": "john wick", "Age": 27}`
    var jsonData = []byte(jsonString)

    var data User

    var err = json.Unmarshal(jsonData, &data)
    if err != nil {
        fmt.Println(err.Error())
        return
    }

    fmt.Println("user :", data.FullName)
    fmt.Println("age  :", data.Age)
}
```

Fungsi unmarshal hanya menerima data json dalam bentuk  `[]byte`, maka dari itu data json string perlu di-casting terlebih dahulu ke tipe  `[]byte`, sebelum akhirnya digunakan pada pemanggilan fungsi  `json.Unmarshal()`.

Perlu diperhatikan, argument ke-2 pemanggilan fungsi tersebut harus diisi dengan variabel  **pointer**  yang nantinya akan menampung hasil operasi decoding.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcNj7CYfm6N55sueS1xs3nxgOKcqXSobwelDZi_3aUHNBFzJbOoPzvdvIije_HzofSKNEyWXnZbVOzhB_e9U0d4rAWLv08Ze_Z6SExgCS3RopIzS4N79RyGtqowolkI_ILADy9yhU-MeOtOkvHgv63K99lS?key=d3s-vJLBsYtwvRvGfZhdnw)**

Property  `FullName`  milik struct  `User`  memiliki  **tag**  `json:"Name"`. Tag tersebut digunakan untuk mapping informasi field json ke property struct.

Data json yang akan di-parsing memiliki 2 property yaitu  `Name`  dan  `Age`. Di contoh, penulisan  `Age`  di data json dan pada struktur struct adalah sama, berbeda dengan  `Name`  yang ada di data json tapi tidak ada di struct.

Dengan menambahkan tag json, maka property  `FullName`  struct akan secara cerdas menampung data json property  `Name`.

> Pada operasi decoding data json string ke variabel objek struct, semua level akses property struct penampung harus publik.

## A.53.2. Decode JSON Ke  `map[string]interface{}`  &  `interface{}`

Tak hanya ke objek cetakan struct, target decoding data json juga bisa berupa variabel bertipe  `map[string]interface{}`.

```
var data1 map[string]interface{}
json.Unmarshal(jsonData, &data1)

fmt.Println("user :", data1["Name"])
fmt.Println("age  :", data1["Age"])
```

Variabel bertipe  `interface{}`  juga bisa digunakan untuk menampung hasil decode. Dengan catatan pada pengaksesan nilai property, harus dilakukan casting terlebih dahulu ke  `map[string]interface{}`.

```
var data2 interface{}
json.Unmarshal(jsonData, &data2)

var decodedData = data2.(map[string]interface{})
fmt.Println("user :", decodedData["Name"])
fmt.Println("age  :", decodedData["Age"])
```

## A.53.3. Decode Array JSON Ke Array Objek

Operasi decode data dari array json ke slice/array objek caranya juga sama. Langsung praktek saja agar lebih jelas. Siapkan sebuah variabel baru untuk menampung hasil decode dengan tipe slice struct, lalu gunakan pada fungsi  `json.Unmarshal()`.

```
var jsonString = `[
    {"Name": "john wick", "Age": 27},
    {"Name": "ethan hunt", "Age": 32}
]`

var data []User

var err = json.Unmarshal([]byte(jsonString), &data)
if err != nil {
    fmt.Println(err.Error())
    return
}

fmt.Println("user 1:", data[0].FullName)
fmt.Println("user 2:", data[1].FullName)
```

## A.53.4. Encode Objek Ke JSON String

Setelah sebelumnya dijelaskan beberapa cara decode data dari json string ke objek, sekarang kita akan belajar cara  **encode**  data objek di Go ke bentuk json string.

Fungsi  `json.Marshal()`  digunakan untuk encoding data ke json string. Sumber data bisa berupa variabel objek cetakan struct, data bertipe  `map[string]interface{}`, slice, atau lainnya.

Pada contoh berikut, data slice struct dikonversi ke dalam bentuk json string. Hasil konversi adalah data bertipe  `[]byte`, maka pastikan untuk meng-casting terlebih dahulu ke tipe  `string`  agar bisa ditampilkan bentuk json string-nya.

```
var object = []User{{"john wick", 27}, {"ethan hunt", 32}}
var jsonData, err = json.Marshal(object)
if err != nil {
    fmt.Println(err.Error())
    return
}

var jsonString = string(jsonData)
fmt.Println(jsonString)
```

Output program:

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcKe1cfvjLqTEqdC26jUJrAjeagN9dXg1xeXhihI12df0rYGMshk2fiyLg7q-Gi4C-ljV6Rl_wJkkWqdpvXZfE5SWV3Dx8tOoVyOTxmm1TuKcIKnstzXFCqSVIixUbxhIIX8iDitrepm5odwm-HLjsWZd_9?key=d3s-vJLBsYtwvRvGfZhdnw)**