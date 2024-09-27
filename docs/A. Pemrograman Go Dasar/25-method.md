---
sidebar_position: 25
---

# A.25. Method


**Method**  adalah fungsi yang menempel pada suatu tipe data, misalnya custom  `struct`. Method bisa diakses lewat variabel objek yang dibuat dari tipe custom struct tersebut.

Keunggulan method dibanding fungsi biasa adalah method memiliki akses ke property struct hingga level akses  _private_. Selain itu, dengan menggunakan method, suatu proses bisa di-enkapsulasi dengan baik.

> Perihal topik level nantinya dibahas secara terpisah pada chapter berikutnya

## A.25.1. Penerapan Method

Cara penerapan method sedikit berbeda dibanding fungsi. Saat proses deklarasi, pada method perlu ditentukan juga siapa pemiliknya. Contohnya bisa dilihat pada kode berikut, dua method diciptakan sebagai property dari struct bernama  `student`.

```
package main

import "fmt"
import "strings"

type student struct {
    name  string
    grade int
}

func (s student) sayHello() {
    fmt.Println("halo", s.name)
}

func (s student) getNameAt(i int) string {
    return strings.Split(s.name, " ")[i-1]
}
```
Cara deklarasi method mirip seperti fungsi, tapi dalam penulisannya perlu ditambahkan deklarasi variabel objek di sela-sela keyword  `func`  dan nama fungsi. Pada contoh di atas struct  `student`  ditentukan sebagai pemilik method.

`func (s student) sayHello()`  maksudnya adalah fungsi  `sayHello`  dideklarasikan sebagai method milik struct  `student`. Di contoh, struct  `student`  memiliki dua buah method yaitu  `sayHello()`  dan  `getNameAt()`.

Contoh pemanfaatan method bisa dilihat pada kode berikut.

```
func main() {
    var s1 = student{"john wick", 21}
    s1.sayHello()

    var name = s1.getNameAt(2)
    fmt.Println("nama panggilan :", name)
}
```

Output program:

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfYRkGbtFiiDflr9uvC8mtywoc1bFzYymnFK4hcQStA9FAe8Ei_QFNnBLSTN64HteWqDnlBOUx67ole9MpuAheSjV82O6S9RNbqudwIUvzE19SnFlWYpq8ANbIoo17f7JYbPcw0vtSioof2Wead0_LOBjxF?key=d3s-vJLBsYtwvRvGfZhdnw)**


Cara mengakses method sama seperti pada pengaksesan property, yaitu dengan cukup panggil saja nama methodnya.

```
s1.sayHello()
var name = s1.getNameAt(2)
```

Method memiliki sifat yang sama persis dengan fungsi biasa, yaitu bisa memiliki parameter, nilai balik, dan sifat-sifat lainnya.

Dari segi sintaks, perbedaan yang paling terlihat hanya di bagian penulisan deklarasi dan cara pengaksesan. Silakan lihat kode berikut agar lebih jelas:

```
func sayHello() { }
func (s student) sayHello() { }

func getNameAt(i int) string { }
func (s student) getNameAt(i int) string { }
```

## A.25.2. Method Pointer

Method pointer adalah method yang dimana variabel objek pemilik method tersebut adalah berbentuk pointer.

Kelebihan method jenis ini adalah ketika kita melakukan manipulasi nilai pada property lain yang masih satu struct, nilai pada property tersebut bisa diubah di-level reference-nya. Lebih jelasnya perhatikan kode berikut.

```
package main

import "fmt"

type student struct {
    name  string
    grade int
}

func (s student) changeName1(name string) {
    fmt.Println("---> on changeName1, name changed to", name)
    s.name = name
}

func (s *student) changeName2(name string) {
    fmt.Println("---> on changeName2, name changed to", name)
    s.name = name
}

func main() {
    var s1 = student{"john wick", 21}
    fmt.Println("s1 before", s1.name)
    // john wick

    s1.changeName1("jason bourne")
    fmt.Println("s1 after changeName1", s1.name)
    // john wick

    s1.changeName2("ethan hunt")
    fmt.Println("s1 after changeName2", s1.name)
    // ethan hunt
}
```

Output program:

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe-6lCpbQDYshHHpNZNyad9sc8G_c9PZYcNSY6RcP3Re4yWvQX8hK2YKfbJNfFuSqHgnKQgdJqRe3zzhyFbGCNduOD5lorUQnWV-61pKkjlaZoWSsGh-e_tD32VlJ1JLikvpU7BVbC_PotRXTegjaxTD7M?key=d3s-vJLBsYtwvRvGfZhdnw)**


Setelah statement  `s1.changeName1("jason bourne")`  dieksekusi, nilai  `s1.name`  tidak berubah. Sebenarnya nilainya berubah tapi hanya dalam method  `changeName1()`  saja, nilai pada reference objek-nya tidak berubah.

Keistimewaan lain method pointer adalah method itu sendiri bisa dipanggil dari objek pointer maupun objek biasa.

```
// pengaksesan method dari variabel objek biasa
var s1 = student{"john wick", 21}
s1.sayHello()

// pengaksesan method dari variabel objek pointer
var s2 = &student{"ethan hunt", 22}
s2.sayHello()
``` 

## A.25.3. Penjelasan tambahan

Berikut merupakan penjelasan tambahan untuk beberapa hal dari kode yang sudah dipraktekan:

#### ◉ Penggunaan Fungsi  `strings.Split()`

Pada chapter ini ada fungsi baru yang kita gunakan saat praktek, yaitu  `strings.Split()`. Fungsi ini berguna untuk memisahkan string menggunakan pemisah yang kita tentukan sendiri. Hasilnya berupa array berisikan kumpulan substring.

```
strings.Split("ethan hunt", " ")
// ["ethan", "hunt"]
```

Pada contoh di atas, string  `"ethan hunt"`  dipisah menggunakan separator spasi  `" "`, hasilnya adalah array berisikan 2 elemen,  `"ethan"`  dan  `"hunt"`.

## A.25.4. Apakah  `fmt.Println()`  &  `strings.Split()`  Juga Merupakan Method?

Setelah tahu apa itu method dan bagaimana penggunaannya, mungkin akan muncul di benak kita bahwa kode seperti  `fmt.Println()`,  `strings.Split()`  dan lainnya-yang-berada-pada-package-lain adalah merupakan method. Jawabannya,**bukan!**.  `fmt`  di situ bukanlah variabel objek, dan  `Println()`  bukan merupakan method.

`fmt`  adalah nama  **package**  yang di-import (bisa dilihat pada kode  `import "fmt"`). Sedangkan  `Println()`  adalah  **nama fungsi**. Untuk mengakses fungsi yang berada pada package lain, harus dituliskan juga nama package-nya, contoh:

-   Statement  `fmt.Println()`  berarti pengaksesan fungsi  `Println()`  yang berada di package  `fmt`
-   Statement  `strings.Split()`  berarti pengaksesan fungsi  `Split()`  yang berada di package  `strings`

Lebih detailnya dibahas pada chapter selanjutnya.