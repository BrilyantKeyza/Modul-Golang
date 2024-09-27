---
sidebar_position: 24
---

# A.24. Struct


Go tidak mengadopsi konsep class seperti pada beberapa bahasa pemrograman OOP lainnya. Namun Go memiliki tipe data struktur Struct.

Struct adalah kumpulan definisi variabel (atau property) dan atau fungsi (atau method), yang dibungkus sebagai tipe data baru dengan nama tertentu. Property dalam struct, tipe datanya bisa bervariasi. Mirip seperti  `map`, hanya saja key-nya sudah didefinisikan di awal, dan tipe data tiap itemnya bisa berbeda.

Dari sebuah struct, kita bisa buat variabel baru, yang memiliki atribut sesuai skema struct tersebut. Kita sepakati dalam buku ini, variabel tersebut dipanggil dengan istilah  **object**  atau  **variabel object**.

> Konsep struct di golang mirip dengan konsep  **class**  pada OOP, meski sebenarnya memiliki perbedaan. Di sini penulis menggunakan konsep OOP sebagai analogi, untuk mempermudah pembaca untuk memahami pembelajaran di chapter ini.

Dengan memanfaatkan struct, penyimpanan data yang sifatnya kolektif menjadi lebih mudah, lebih rapi, dan mudah untuk dikelola.

## A.24.1. Deklarasi Struct

Kombinasi keyword  `type`  dan  `struct`  digunakan untuk deklarasi struct. Di bawah ini merupakan contoh cara penerapannya.

```
type student struct {
    name string
    grade int
}
```

Struct  `student`  dideklarasikan memiliki 2 property, yaitu  `name`  dan  `grade`. Property adalah istilah untuk variabel yang menempel ke struct.

## A.24.2. Penerapan Struct Untuk Membuat Object

Struct  `student`  yang sudah disiapkan di atas kita gunakan untuk membuat variabel objek. Variabel tersebut tipe datanya adalah  `student`. Kemudian dari variabel object, kita bisa mengakses isi property variabel. Contoh:

```
func main() {
    var s1 student
    s1.name = "john wick"
    s1.grade = 2

    fmt.Println("name  :", s1.name)
    fmt.Println("grade :", s1.grade)
}
```

Cara membuat variabel objek sama seperti pembuatan variabel biasa. Tinggal tulis saja nama variabel diikuti nama struct, contoh:  `var s1 student`.

Semua property variabel objek pada awalnya memiliki zero value sesuai tipe datanya. Misalnya, 0 untuk tipe  `int`, dan string kosong  `""`  untuk string.

Property variabel objek bisa diakses nilainya menggunakan notasi titik, contohnya  `s1.name`. Nilai property-nya juga bisa diubah, contohnya  `s1.grade = 2`.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcNIFwcQjeN3oPJeovhc4h68kmpuk-wZV7Ac3OrAkyKt6cDE3av6VzKWh3jdfdCDu0XR71vouhLb7fYuOtcjU9rYxYxY-U-2qJcTzGPyZjNNEQC8l7gCXLSLeYmwzNP2uiwFD7Bu3EG47t5bIdKQgiycsQ?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.24.3. Inisialisasi Object Struct

Cara inisialisasi variabel objek adalah dengan menuliskan nama struct yang telah dibuat diikuti dengan kurung kurawal. Nilai masing-masing property bisa diisi pada saat inisialisasi.

Pada contoh berikut, terdapat 3 buah variabel objek yang dideklarasikan dengan cara berbeda.

```
var s1 = student{}
s1.name = "wick"
s1.grade = 2

var s2 = student{"ethan", 2}

var s3 = student{name: "jason"}

fmt.Println("student 1 :", s1.name)
fmt.Println("student 2 :", s2.name)
fmt.Println("student 3 :", s3.name)
```

Pada kode di atas, variabel  `s1`  menampung objek cetakan  `student`. Variabel tersebut kemudian di-set nilai property-nya.

Variabel objek  `s2`  dideklarasikan dengan metode yang sama dengan  `s1`, pembedanya di  `s2`  nilai propertinya di isi langsung ketika deklarasi. Nilai pertama akan menjadi nilai property pertama (yaitu  `name`), dan selanjutnya berurutan.

Pada deklarasi  `s3`, dilakukan juga pengisian property ketika pencetakan objek. Hanya saja, yang diisi hanya  `name`  saja. Cara ini cukup efektif jika digunakan untuk membuat objek baru yang nilai property-nya tidak semua harus disiapkan di awal. Keistimewaan lain menggunakan cara ini adalah penentuan nilai property bisa dilakukan dengan tidak berurutan. Contohnya:

```
var s4 = student{name: "wayne", grade: 2}
var s5 = student{grade: 2, name: "bruce"}
```

## A.24.4. Variabel Objek Pointer

Objek yang dibuat dari tipe struct bisa diambil nilai pointer-nya, dan bisa disimpan pada variabel objek yang bertipe struct pointer. Contoh penerapannya:

```
var s1 = student{name: "wick", grade: 2}

var s2 *student = &s1
fmt.Println("student 1, name :", s1.name)
fmt.Println("student 4, name :", s2.name)

s2.name = "ethan"
fmt.Println("student 1, name :", s1.name)
fmt.Println("student 4, name :", s2.name)
```

`s2`  adalah variabel pointer hasil cetakan struct  `student`.  `s2`  menampung nilai referensi  `s1`, menjadikan setiap perubahan pada property variabel tersebut, akan juga berpengaruh pada variabel objek  `s1`.

Meskipun  `s2`  bukan variabel asli, property nya tetap bisa diakses seperti biasa. Inilah keistimewaan property dalam objek pointer, tanpa perlu di-dereferensi nilai asli property tetap bisa diakses. Pengisian nilai pada property tersebut juga bisa langsung menggunakan nilai asli, contohnya seperti  `s2.name = "ethan"`.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfl3gc3Nnpohc_5LVqBZlyLovYDEyZ9MFXe7Ez3Y8Jv__EV--z4SjSdI3qA182DI_c1AAwOVftVUo-ZgngphwLqdD7FYT3IAHHijwY9TfP2U_YLLEWsEBuWlEYTildXBeoKo_G4GVEM3zXQsRAljI5wsu4?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.24.5. Embedded Struct

**Embedded**  struct adalah mekanisme untuk menempelkan sebuah struct sebagai properti struct lain. Agar lebih mudah dipahami, mari kita bahas kode berikut.

```
package main

import "fmt"

type person struct {
    name string
    age  int
}

type student struct {
    grade int
    person
}

func main() {
    var s1 = student{}
    s1.name = "wick"
    s1.age = 21
    s1.grade = 2

    fmt.Println("name  :", s1.name)
    fmt.Println("age   :", s1.age)
    fmt.Println("age   :", s1.person.age)
    fmt.Println("grade :", s1.grade)
}
```

Pada kode di atas, disiapkan struct  `person`  dengan properti yang tersedia adalah  `name`  dan  `age`. Disiapkan juga struct  `student`  dengan property  `grade`. Struct  `person`  di-embed ke dalam struct  `student`. Caranya cukup mudah, yaitu dengan menuliskan nama struct yang ingin di-embed ke dalam body  `struct`  target.

Embedded struct adalah  **mutable**, nilai property-nya nya bisa diubah.

Khusus untuk properti yang bukan merupakan properti asli (melainkan properti turunan dari struct lain), pengaksesannya dilakukan dengan cara mengakses struct  _parent_-nya terlebih dahulu, contohnya  `s1.person.age`. Nilai yang dikembalikan memiliki referensi yang sama dengan  `s1.age`.

## A.24.6. Embedded Struct Dengan Nama Property Yang Sama

Jika salah satu nama properti sebuah struct memiliki kesamaan dengan properti milik struct lain yang di-embed, maka pengaksesan property-nya harus dilakukan secara eksplisit atau jelas. Silakan lihat kode berikut agar lebih jelas.

```
package main

import "fmt"

type person struct {
    name string
    age  int
}

type student struct {
    person
    age   int
    grade int
}

func main() {
    var s1 = student{}
    s1.name = "wick"
    s1.age = 21        // age of student
    s1.person.age = 22 // age of person

    fmt.Println(s1.name)
    fmt.Println(s1.age)
    fmt.Println(s1.person.age)
}
```
Struct `person` di-embed ke dalam struct `student`, dan kedua struct tersebut kebetulan salah satu nama property-nya ada yang sama, yaitu `age`. Cara mengakses property `age` milik struct `person` lewat objek struct `student`, adalah dengan menuliskan nama struct yang di-embed kemudian nama property-nya, contohnya: `s1.person.age = 22`.

## A.24.7. Pengisian Nilai Sub-Struct

Pengisian nilai property sub-struct bisa dilakukan dengan langsung memasukkan variabel objek yang tercetak dari struct yang sama.

```
var p1 = person{name: "wick", age: 21}
var s1 = student{person: p1, grade: 2}

fmt.Println("name  :", s1.name)
fmt.Println("age   :", s1.age)
fmt.Println("grade :", s1.grade)
```

Pada deklarasi  `s1`, property  `person`  diisi variabel objek  `p1`.

## A.24.8. Anonymous Struct

Anonymous struct adalah struct yang tidak dideklarasikan di awal sebagai tipe data baru, melainkan langsung ketika pembuatan objek. Teknik ini cukup efisien digunakan pada  _use case_  pembuatan variabel objek yang struct-nya hanya dipakai sekali.

```
package main

import "fmt"

type person struct {
    name string
    age  int
}

func main() {
    var s1 = struct {
        person
        grade int
    }{}
    s1.person = person{"wick", 21}
    s1.grade = 2

    fmt.Println("name  :", s1.person.name)
    fmt.Println("age   :", s1.person.age)
    fmt.Println("grade :", s1.grade)
}
```
Pada kode di atas, variabel  `s1`  langsung diisi objek anonymous struct yang memiliki property  `grade`, dan property  `person`  yang merupakan embedded struct.

Salah satu aturan yang perlu diingat dalam pembuatan anonymous struct adalah, deklarasi harus diikuti dengan inisialisasi. Bisa dilihat pada  `s1`  setelah deklarasi struktur struct, terdapat kurung kurawal untuk inisialisasi objek. Meskipun nilai tidak diisikan di awal, kurung kurawal tetap harus ditulis.

```
// anonymous struct tanpa pengisian property
var s1 = struct {
    person
    grade int
}{}

// anonymous struct dengan pengisian property
var s2 = struct {
    person
    grade int
}{
    person: person{"wick", 21},
    grade:  2,
}
```

## A.24.9. Kombinasi Slice & Struct

Slice dan  `struct`  bisa dikombinasikan seperti pada slice dan  `map`, caranya penggunaannya-pun mirip, cukup tambahkan tanda  `[]`  sebelum tipe data pada saat deklarasi.

```
type person struct {
    name string
    age  int
}

var allStudents = []person{
    {name: "Wick", age: 23},
    {name: "Ethan", age: 23},
    {name: "Bourne", age: 22},
}

for _, student := range allStudents {
    fmt.Println(student.name, "age is", student.age)
}
```

## A.24.10. Inisialisasi Slice Anonymous Struct

Anonymous struct bisa dijadikan sebagai tipe sebuah slice. Dan nilai awalnya juga bisa diinisialisasi langsung pada saat deklarasi. Berikut adalah contohnya:

```
var allStudents = []struct {
    person
    grade int
}{
    {person: person{"wick", 21}, grade: 2},
    {person: person{"ethan", 22}, grade: 3},
    {person: person{"bond", 21}, grade: 3},
}

for _, student := range allStudents {
    fmt.Println(student)
}
```

## A.24.11. Deklarasi Anonymous Struct Menggunakan Keyword  **var**

Cara lain untuk deklarasi anonymous struct adalah dengan menggunakan keyword  `var`.

```
var student struct {
    person
    grade int
}

student.person = person{"wick", 21}
student.grade = 2
```
Statement  `type student struct`  adalah contoh cara deklarasi struct. Maknanya akan berbeda ketika keyword  `type`  diganti  `var`, seperti pada contoh di atas  `var student struct`, yang artinya dicetak sebuah objek dari anonymous struct kemudian disimpan pada variabel bernama  `student`.

Deklarasi anonymous struct menggunakan metode ini juga bisa dilakukan dengan disertai inisialisasi data.

```
// hanya deklarasi
var student struct {
    grade int
}

// deklarasi sekaligus inisialisasi
var student = struct {
    grade int
} {
    12,
}
```

## A.24.12. Nested struct

Nested struct adalah anonymous struct yang di-embed ke sebuah struct. Deklarasinya langsung di dalam struct peng-embed. Contoh:

```
type student struct {
    person struct {
        name string
        age  int
    }
    grade   int
    hobbies []string
}
```

Teknik ini biasa digunakan ketika decoding data  **JSON**  yang struktur datanya cukup kompleks dengan proses decode hanya sekali.

## A.24.13. Deklarasi Dan Inisialisasi Struct Secara Horizontal

Deklarasi struct bisa dituliskan secara horizontal, caranya bisa dilihat pada kode berikut:

```
type person struct { name string; age int; hobbies []string }
```

Tanda semi-colon (`;`) digunakan sebagai pembatas deklarasi poperty yang dituliskan secara horizontal. Inisialisasi nilai juga bisa dituliskan dengan metode ini. Contohnya:

```
var p1 = struct { name string; age int } { age: 22, name: "wick" }
var p2 = struct { name string; age int } { "ethan", 23 }
```

## A.24.14. Tag property dalam struct

Tag merupakan informasi opsional yang bisa ditambahkan pada property struct.

```
type person struct {
    name string `tag1`
    age  int    `tag2`
}
```

Tag biasa dimanfaatkan untuk keperluan encode/decode data. Informasi tag juga bisa diakses lewat reflect. Nantinya akan ada pembahasan yang lebih detail mengenai pemanfaatan tag dalam struct, terutama ketika sudah masuk chapter JSON.

## A.24.15. Type Alias

Sebuah tipe data, seperti struct, bisa dibuatkan alias baru, caranya dengan  `type NamaAlias = TargetStruct`. Contoh:

```
type Person struct {
    name string
    age  int
}
type People = Person

var p1 = Person{"wick", 21}
fmt.Println(p1)

var p2 = People{"wick", 21}
fmt.Println(p2)
```
Pada kode di atas, sebuah alias bernama  `People`  dibuat untuk struct  `Person`.

Casting dari objek (yang dicetak lewat struct tertentu) ke tipe yang merupakan alias dari struct pencetak, hasilnya selalu valid. Berlaku juga sebaliknya.

```
people := People{"wick", 21}
fmt.Println(Person(people))

person := Person{"wick", 21}
fmt.Println(People(person))
```
Pembuatan struct baru juga bisa dilakukan lewat teknik type alias. Silakan perhatikan kode berikut.

```
type People1 struct {
    name string
    age  int
}
type People2 = struct {
    name string
    age  int
}
```

Struct  `People1`  dideklarasikan, kemudian struct alias  `People2`  juga dideklarasikan. Struct  `People2`  merupakan alias dari anonymous struct. Penggunaan teknik type alias untuk anonymous struct menghasilkan output yang ekuivalen dengan pendeklarasian struct.

Teknik type alias ini tidak dirancang hanya untuk pembuatan alias pada tipe struct saja, semua jenis tipe data bisa dibuatkan alias. Contohnya seperti pada kode berikut, ada tipe data baru bernama  `Number`  yang merupakan alias dari tipe data  `int`.

```
type Number = int
var num Number = 12
```