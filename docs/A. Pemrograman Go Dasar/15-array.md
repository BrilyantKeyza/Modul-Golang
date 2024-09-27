---
sidebar_position: 15
---

# A.15. Array


Array adalah kumpulan data bertipe sama, yang disimpan dalam sebuah variabel. Array memiliki kapasitas yang nilainya ditentukan pada saat pembuatan, menjadikan elemen/data yang disimpan di array tersebut jumlahnya tidak boleh melebihi yang sudah dialokasikan.

Default nilai tiap elemen array pada awalnya tergantung dari tipe datanya. Jika  `int`  maka tiap element zero value-nya adalah  `0`, jika  `bool`  maka  `false`, dan seterusnya. Setiap elemen array memiliki indeks berupa angka yang merepresentasikan posisi urutan elemen tersebut. Indeks array dimulai dari 0.

Contoh penerapan array:

```
var names [4]string
names[0] = "trafalgar"
names[1] = "d"
names[2] = "water"
names[3] = "law"

fmt.Println(names[0], names[1], names[2], names[3])
```

Variabel  `names`  dideklarasikan sebagai  `array string`  dengan alokasi kapasitas elemen adalah  `4`  slot. Cara mengisi slot elemen array bisa dilihat di kode di atas, yaitu dengan langsung mengakses elemen menggunakan indeks, lalu mengisinya.


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcHzG0uITXo59ko8OimvBIshYBIDPDiPEuwi5u8lXxnfPJHgovl04oZGP-9RJCShFFGeCPV-Jg1GeQ97JKmyFbUccCLBY2hfmp3xk9ZUKBPAfvRCLPvqSJLtmEOpWI00Om-r-O-NgRKtn-Bq7XmUifZe0s?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.15.1. Pengisian Elemen Array yang Melebihi Alokasi Awal

Pengisian elemen array pada indeks yang tidak sesuai dengan jumlah alokasi menghasilkan error. Contoh: jika array memiliki 4 slot, maka pengisian nilai slot 5 seterusnya adalah tidak valid.

```
var names [4]string
names[0] = "trafalgar"
names[1] = "d"
names[2] = "water"
names[3] = "law"
names[4] = "ez" // baris kode ini menghasilkan error
```

Solusi dari masalah di atas adalah dengan menggunakan keyword  `append`, yang pembahasannya ada pada chapter selanjutnya, (A.16. Slice).

## A.15.2. Inisialisasi Nilai Awal Array

Pengisian elemen array bisa dilakukan pada saat deklarasi variabel. Caranya dengan menuliskan data elemen dalam kurung kurawal setelah tipe data, dengan pembatas antar elemen adalah tanda koma (`,`).

```
var fruits = [4]string{"apple", "grape", "banana", "melon"}

fmt.Println("Jumlah element \t\t", len(fruits))
fmt.Println("Isi semua element \t", fruits)
```

Penggunaan fungsi  `fmt.Println()`  pada data array tanpa mengakses indeks tertentu, menghasilkan output dalam bentuk string dari semua array yang ada. Teknik ini umum digunakan untuk keperluan  _debugging_  data array.


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf_lM0xei5cfePSl0ILG-U1Ic4Yk9zf94EwIgc3NcgtkKY4nb6oWHZ5-mFZMTnWRIK9Z5tXlQHsCavMRnpzOKGi8in1nu3cFwqHPxAoA5H9OsKbe3oEDKk-55t5kaH_OVOuxELjQCXa0CAVnTGU6wvZq10i?key=d3s-vJLBsYtwvRvGfZhdnw)**


Fungsi `len()` berfungsi untuk menghitung jumlah elemen sebuah array.

## A.15.3. Inisialisasi Nilai Array Dengan Gaya Vertikal

Elemen array bisa dituliskan dalam bentuk horizontal (seperti yang sudah dicontohkan di atas) ataupun dalam bentuk vertikal.

```
var fruits [4]string

// cara horizontal
fruits  = [4]string{"apple", "grape", "banana", "melon"}

// cara vertikal
fruits  = [4]string{
    "apple",
    "grape",
    "banana",
    "melon",
}
```

Khusus untuk deklarasi array dengan cara vertikal, tanda koma wajib dituliskan setelah setiap elemen (termasuk elemen terakhir), agar tidak memunculkan syntax error.

## A.15.4. Inisialisasi Nilai Awal Array Tanpa Jumlah Elemen

Deklarasi array yang nilainya diset di awal, boleh tidak dituliskan jumlah lebar array-nya, cukup ganti dengan tanda 3 titik (`...`). Metode penulisan ini membuat kapasitas array otomatis dihitung dari jumlah elemen array yang ditulis.

```
var numbers = [...]int{2, 3, 2, 4, 3}

fmt.Println("data array \t:", numbers)
fmt.Println("jumlah elemen \t:", len(numbers))
```

Variabel  `numbers`  secara otomatis kapasitas elemennya adalah  `5`.


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcc2sxQ6rhs78Qjy3lImJqeac7oOGywc-7VtwGiN8QBz4i-HJPfWg92F_C11QAjHY7GVmU8VoDBYFDsqaZ9k1NYbkWpQcP5taUrW6R7X2GLuXywIDPRvBOWWJtS2JEG4EliKzFo90Rm3DaNNxRINi17iAQN?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.15.5. Array Multidimensi

Array multidimensi adalah array yang tiap elemennya juga berupa array.

> Level kedalaman array multidimensi adalah tidak terbatas, bisa saja suatu array berisi elemen array yang setiap elemennya juga adalah nilai array, dst.

Cara deklarasi array multidimensi secara umum sama dengan array biasa, bedanya adalah pada array biasa, setiap elemen berisi satu nilai, sedangkan pada array multidimensi setiap elemen berisi array.

Khusus penulisan array yang merupakan subdimensi/elemen, boleh tidak dituliskan jumlah datanya. Contohnya bisa dilihat pada deklarasi variabel  `numbers2`  di kode berikut.

```
var numbers1 = [2][3]int{[3]int{3, 2, 3}, [3]int{3, 4, 5}}
var numbers2 = [2][3]int{{3, 2, 3}, {3, 4, 5}}

fmt.Println("numbers1", numbers1)
fmt.Println("numbers2", numbers2)
```

Kedua array di atas memiliki jumlah dan isi elemen yang sama.


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeN1N3EABJfJihzZEU_baSyA4PHvFlamEEglyD9Znk0O6yhr9VfqhzqAvvGHnRnvbv4tdgd4uStQ6v9ibuQ6HqHRNT1oDMUogV1Ei_c-shwP-SIp1o1WJhvH87VQgRQnwgkCFSZFvwW01N02arwlT_WBJR1?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.15.6. Perulangan Elemen Array Menggunakan Keyword  `for`

Keyword  `for`  dan array memiliki hubungan yang sangat erat. Dengan memanfaatkan perulangan/looping menggunakan keyword ini, elemen-elemen dalam array bisa didapat.

Ada beberapa cara yang bisa digunakan untuk me-looping data array, yg pertama adalah dengan memanfaatkan variabel iterasi perulangan untuk mengakses elemen berdasarkan indeks-nya. Contoh:

```
var fruits = [4]string{"apple", "grape", "banana", "melon"}

for i := 0; i < len(fruits); i++ {
    fmt.Printf("elemen %d : %s\n", i, fruits[i])
}
```

Perulangan di atas dijalankan sebanyak jumlah elemen array  `fruits`  (bisa diketahui dari kondisi  `i < len(fruits`). Di tiap perulangan, elemen array diakses lewat variabel iterasi  `i`.


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXePUk34mmm2wDJ_zFtXlknccdl1ngpS_dDShsqKUFM4UCUjPPdAMR8R7ttBg0M7OXKZYxdkwVyeMLVQQmRlis05DMNwvQ-rNsyr4jnJim489-2lxMnZgpKHFnFagi1dfkLDQzsdh2ZaeC7-jAZpp-dC3xKN?key=d3s-vJLBsYtwvRvGfZhdnw)**


## A.15.7. Perulangan Elemen Array Menggunakan Keyword  `for`  -  `range`

Ada cara lain yang lebih sederhana untuk operasi perulangan array, yaitu menggunakan kombinasi keyword  `for`  -  `range`. Contoh pengaplikasiannya bisa dilihat di kode berikut.

```
var fruits = [4]string{"apple", "grape", "banana", "melon"}

for i, fruit := range fruits {
    fmt.Printf("elemen %d : %s\n", i, fruit)
}
```

Array  `fruits`  diambil elemen-nya secara berurutan. Nilai tiap elemen ditampung variabel oleh  `fruit`  (tanpa huruf s), sedangkan indeks nya ditampung variabel  `i`.

Output program di atas, sama persis dengan output program sebelumnya, hanya saja cara yang diterapkan berbeda.

## A.15.8. Penggunaan Variabel Underscore  `_`  Dalam  `for`  -  `range`

Terkadang, dalam penerapan  _looping_  menggunakan  `for`  -  `range`, ada kebutuhan di mana yang dibutuhkan dari perulangan adlah adalah elemen-nya saja, sedangkan indeks-nya tidak, contoh:

```
var fruits = [4]string{"apple", "grape", "banana", "melon"}

for i, fruit := range fruits {
    fmt.Printf("nama buah : %s\n", fruit)
}
```

Hasil dari kode program di atas adalah error, karena Go tidak memperbolehkan adanya variabel yang menganggur atau tidak dipakai.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfMeNF1kbAkntmoYw_JvABlFqivYpgBHA4qFrbKiu3p0p7vNa9Bw7GCImbKW72NJGUvG0JgFioapb5jQoaL5AfNSSBbb5Kpo15xMS0DiF2sQuZE8P4JVMcIoXmWQ-J8oDHdLPklAXwRmHafvv2Je2Wzo6I?key=d3s-vJLBsYtwvRvGfZhdnw)**
Di sinilah salah satu kegunaan dari variabel pengangguran, atau underscore (`_`). Tampung saja nilai yang tidak ingin digunakan ke underscore.

```
var fruits = [4]string{"apple", "grape", "banana", "melon"}

for _, fruit := range fruits {
    fmt.Printf("nama buah : %s\n", fruit)
}
```

Pada kode di atas, yang sebelumnya adalah variabel  `i`  diganti dengan  `_`, karena kebetulan variabel  `i`  tidak digunakan.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc25O6n8L2K0v1eVy1wTNtOECY1py8dmVktNa8Mpu0cnYAUFjmPIV2fSLwUmmZuKxmiLnTRHQHJgy5lvWQWfeCY20VHB6GQtJ5vEx2OKjXh2qJtGvBcKLjy5kNN3Tci7HBwJNVoJPUkh2giq2ZRTk7w1qN-?key=d3s-vJLBsYtwvRvGfZhdnw)**
Bagaiamana jika sebaliknya? Misal, yang dibutuhkan hanya indeks-nya saja, nilainya tidak penting. Maka cukup tulis satu variabel saja setelah keyword  `for`, yaitu variabel penampung nilai indeks.

```
for i, _ := range fruits { }
// atau
for i := range fruits { }
```

## A.15.9. Alokasi Elemen Array Menggunakan Keyword  `make`

Deklarasi sekaligus alokasi kapasitas array juga bisa dilakukan lewat keyword  `make`.

```
var fruits = make([]string, 2)
fruits[0] = "apple"
fruits[1] = "manggo"

fmt.Println(fruits)  // [apple manggo]
```

Parameter pertama keyword  `make`  diisi dengan tipe data elemen array yang diinginkan, parameter kedua adalah jumlah elemennya. Pada kode di atas, variabel  `fruits`  tercetak sebagai array string dengan kapasitas alokasi 2 slot.