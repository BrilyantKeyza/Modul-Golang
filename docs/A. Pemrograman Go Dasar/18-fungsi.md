---
sidebar_position: 18
---

# A.18. Fungsi


Dalam konteks pemrograman, fungsi adalah sekumpulan blok kode yang dibungkus dengan nama tertentu. Penerapan fungsi yang tepat akan menjadikan kode lebih modular dan juga  _dry_  (singkatan dari  _don't repeat yourself_) yang artinya kita tidak perlu menuliskan banyak kode untuk kegunaan yang sama berulang kali. Cukup deklarasikan sekali saja blok kode sebagai suatu fungsi, lalu panggil sesuai kebutuhan.

Pada chapter ini kita akan belajar tentang penerapannya di Go.

## A.18.1. Penerapan Fungsi

Mungkin pembaca sadar, bahwa sebenarnya kita sudah mengimplementasikan fungsi pada banyak praktek sebelumnya, yaitu fungsi  `main()`. Fungsi  `main()`  sendiri merupakan fungsi utama pada program Go, yang akan dieksekusi ketika program dijalankan.

Selain fungsi  `main()`, kita juga bisa membuat fungsi lainnya. Dan caranya cukup mudah, yaitu dengan menuliskan keyword  `func`  kemudian diikuti nama fungsi, lalu kurung  `()`  (yang bisa diisi parameter), dan diakhiri dengan kurung kurawal untuk membungkus blok kode.

Parameter merupakan variabel yang menempel di fungsi yang nilainya ditentukan saat pemanggilan fungsi tersebut. Parameter sifatnya opsional, suatu fungsi bisa tidak memiliki parameter, atau bisa saja memeliki satu atau banyak parameter (tergantung kebutuhan).

> Data yang digunakan sebagai value parameter saat pemanggilan fungsi biasa disebut dengan argument parameter (atau argument).

Agar lebih jelas, silakan lihat dan praktekan kode contoh implementasi fungsi berikut ini:

```
package main

import "fmt"
import "strings"

func main() {
    var names = []string{"John", "Wick"}
    printMessage("halo", names)
}

func printMessage(message string, arr []string) {
    var nameString = strings.Join(arr, " ")
    fmt.Println(message, nameString)
}
```

Pada kode di atas, sebuah fungsi baru dibuat dengan nama  `printMessage()`  memiliki 2 buah parameter yaitu string  `message`  dan slice string  `arr`.

Fungsi tersebut dipanggil dalam  `main()`, dalam pemanggilannya disisipkan dua buah argument parameter.

1.  Argument parameter pertama adalah string  `"halo"`  yang ditampung parameter  `message`
2.  Argument parameter ke-2 adalah slice string  `names`  yang nilainya ditampung oleh parameter  `arr`

Di dalam  `printMessage()`, nilai  `arr`  yang merupakan slice string digabungkan menjadi sebuah string dengan pembatas adalah karakter  **spasi**. Penggabungan slice dapat dilakukan dengan memanfaatkan fungsi  `strings.Join()`  (berada di dalam package  `strings`).


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfTI_ejK1nACEhmPm9hF4LQ5Q8-2yQ0gzGaLlC4XsPlR-bz7weY1zmeLVkGxwLZvmsf_RmqujGwj3Lvr_JikhbR9yYCI2yJo-akE0s2KLgfzZm9ok6Tce-FUqOUETGelJDqVA60r9-8cAZFs_umSl-rYzE?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.18.2. Fungsi Dengan Return Value / Nilai Balik

Selain parameter, fungsi bisa memiliki attribute  **return value**  atau nilai balik. Fungsi yang memiliki return value, saat deklarasinya harus ditentukan terlebih dahulu tipe data dari nilai baliknya.

> Fungsi yang tidak mengembalikan nilai apapun (contohnya seperti fungsi  `main()`  dan  `printMessage()`) biasa disebut dengan  **void function**

Program berikut merupakan contoh penerapan fungsi yang memiliki return value.

```
package main

import (
    "fmt"
    "math/rand"
    "time"
)

var randomizer = rand.New(rand.NewSource(time.Now().Unix()))

func main() {
    var randomValue int

    randomValue = randomWithRange(2, 10)
    fmt.Println("random number:", randomValue)

    randomValue = randomWithRange(2, 10)
    fmt.Println("random number:", randomValue)

    randomValue = randomWithRange(2, 10)
    fmt.Println("random number:", randomValue)
}

func randomWithRange(min, max int) int {
    var value = randomizer.Int()%(max-min+1) + min
    return value
}
```
Fungsi `randomWithRange()` didesain untuk _generate_ angka acak sesuai dengan range yang ditentukan lewat parameter, yang kemudian angka tersebut dijadikan nilai balik fungsi.


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdpsiZedmGkfBh6LTweLQhxPqOyZlBcYhqXMCFwsHAPb5DNhUnqQsJeylrgthzMEw-r5GRzNp_7Cuv1XOJyB76Pq59gP-miRG6-Q72OAtKlM6PQUNnojNV8UVphoXK1kLvoKhL_dWcYWGT25g9Uj0-GA7vQ?key=d3s-vJLBsYtwvRvGfZhdnw)**


Cara menentukan tipe data nilai balik fungsi adalah dengan menuliskan tipe data yang diinginkan setelah kurung parameter. Bisa dilihat pada kode di atas, bahwa  `int`  merupakan tipe data nilai balik fungsi  `randomWithRange()`.

```
func randomWithRange(min, max int) int
```

Sedangkan cara untuk mengembalikan nilai itu sendiri adalah dengan menggunakan keyword  `return`  diikuti data yang dikembalikan. Pada contoh di atas,  `return value`  artinya nilai variabel  `value`  dijadikan nilai kembalian fungsi.

Eksekusi keyword  `return`  akan menjadikan proses dalam blok fungsi berhenti pada saat itu juga. Semua statement setelah keyword tersebut tidak akan dieksekusi.

Dari kode di atas mungkin ada beberapa hal yang belum pernah kita lakukan pada pembahasan-pembahasan sebelumnya, kita akan bahas satu-persatu.

## A.18.3. Penggunaan Fungsi  `rand.New()`

Fungsi  `rand.New()`  digunakan untuk membuat object randomizer, yang dari object tersebut kita bisa mendapatkan nilai random/acak hasil generator. Dalam penerapannya, fungsi  `rand.New()`  membutuhkan argument yaitu random source seed, yang bisa kita buat lewat statement  `rand.NewSource(time.Now().Unix())`.

```
var randomizer = rand.New(rand.NewSource(time.Now().Unix()))
```

> Dalam penggunaan fungsi  `rand.NewSource()`, argument bisa diisi dengan nilai apapun, salah satunya adalah  `time.Now().Unix()`.
> 
> Lebih detailnya mengenai random dan apa peran seed dibahas pada chapter  A.39. Random.

Fungsi  `rand.New()`  berada dalam package  `math/rand`. Package tersebut harus di-import terlebih dahulu sebelum bisa menggunakan fungsi-fungsi yang ada didalamnya. Package  `time`  juga perlu di-import karena di contoh ini fungsi  `(time.Now().Unix())`  digunakan.

## A.18.4. Import Banyak Package

Penulisan keyword  `import`  untuk banyak package bisa dilakukan dengan dua cara, dengan menuliskannya di tiap package, atau cukup sekali saja, bebas silakan pilih sesuai selera.

```
import "fmt"
import "math/rand"
import "time"

// atau

import (
    "fmt"
    "math/rand"
    "time"
)
```

## A.18.5. Deklarasi Parameter Bertipe Data Sama

Khusus untuk fungsi yang tipe data parameternya sama, bisa ditulis dengan gaya yang unik. Tipe datanya dituliskan cukup sekali saja di akhir. Contohnya bisa dilihat pada kode berikut.

```
func nameOfFunc(paramA type, paramB type, paramC type) returnType
func nameOfFunc(paramA, paramB, paramC type) returnType

func randomWithRange(min int, max int) int
func randomWithRange(min, max int) int
```

## A.18.6. Penggunaan Keyword  `return`  Untuk Menghentikan Proses Dalam Fungsi

Selain sebagai penanda nilai balik, keyword  `return`  juga bisa dimanfaatkan untuk menghentikan proses dalam blok fungsi di mana ia ditulis. Contohnya bisa dilihat pada kode berikut.

```
package main

import "fmt"

func main() {
    divideNumber(10, 2)
    divideNumber(4, 0)
    divideNumber(8, -4)
}

func divideNumber(m, n int) {
    if n == 0 {
        fmt.Printf("invalid divider. %d cannot divided by %d\n", m, n)
        return
    }

    var res = m / n
    fmt.Printf("%d / %d = %d\n", m, n, res)
}
```
Fungsi  `divideNumber()`  dirancang tidak memiliki nilai balik. Fungsi ini dibuat untuk membungkus proses pembagian 2 bilangan, lalu menampilkan hasilnya.

Di dalamnya terdapat proses validasi nilai variabel pembagi, jika nilainya adalah 0, maka akan ditampilkan pesan bahwa pembagian tidak bisa dilakukan, lalu proses dihentikan pada saat itu juga (dengan memanfaatkan keyword  `return`). Jika nilai pembagi valid, maka proses pembagian diteruskan.


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcbJcqD02U6I3pbjDgGVCIvGM6XJpP6tEN8PNXdfQhg6XfSARgUA2bw8NJTFl6YuQR9jAFjz56Lj6dfPU2d5TqV5HK7Enm-OS-I5e1dExg2iGcnRJKgW-04Nwx7oZpzAe0ErjQxfsNDaT4HijGZmCQuRUB9?key=d3s-vJLBsYtwvRvGfZhdnw)**