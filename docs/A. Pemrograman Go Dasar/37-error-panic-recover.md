---
sidebar_position: 37
---

# A.37. Error, Panic, dan Recover


Error merupakan topik yang sangat penting dalam pemrograman Go, salah satu alasannya karena Go tidak mengadopsi konsep exception.

Pada chapter ini kita akan belajar tentang pemanfaatan error dan cara membuat custom error. Selain itu, kita juga akan belajar tentang penggunaan  **panic**  untuk memunculkan panic error, dan  **recover**  untuk mengatasinya.

## A.37.1. Pemanfaatan Error

Di go,  `error`  merupakan sebuah tipe data. Error memiliki beberapa property yang salah satunya adalah method  `Error()`. Method ini mengembalikan detail pesan error dalam string. Error termasuk tipe yang isinya bisa  `nil`.

Pada praktik pemrograman Go, pembaca akan menemui banyak sekali fungsi yang mengembalikan nilai balik lebih dari satu, yang biasanya salah satunya adalah bertipe  `error`.

Contohnya seperti pada fungsi  `strconv.Atoi()`. Fungsi tersebut digunakan untuk konversi data string menjadi numerik. Fungsi ini mengembalikan 2 nilai balik. Nilai balik pertama adalah hasil konversi, dan nilai balik kedua adalah  `error`. Ketika konversi berjalan mulus, nilai balik kedua akan bernilai  `nil`. Sedangkan ketika konversi gagal, penyebabnya bisa langsung diketahui dari error yang dikembalikan.

Di bawah ini merupakan contoh program sederhana untuk deteksi inputan dari user, apakah numerik atau bukan. Pada kode tersebut kita akan belajar mengenai pemanfaatan error.

```
package main

import (
    "fmt"
    "strconv"
)

func main() {
    var input string
    fmt.Print("Type some number: ")
    fmt.Scanln(&input)

    var number int
    var err error
    number, err = strconv.Atoi(input)

    if err == nil {
        fmt.Println(number, "is number")
    } else {
        fmt.Println(input, "is not number")
        fmt.Println(err.Error())
    }
}
```

Jalankan program, maka muncul tulisan  `"Type some number: "`. Ketik angka bebas, jika sudah maka enter.

Statement  `fmt.Scanln(&input)`  dipergunakan untuk men-capture inputan yang diketik oleh user sebelum dia menekan enter, lalu menyimpannya sebagai string ke variabel  `input`.

Selanjutnya variabel tersebut dikonversi ke tipe numerik menggunakan  `strconv.Atoi()`. Fungsi tersebut mengembalikan 2 data, ditampung oleh  `number`  dan  `err`.

Data pertama (`number`) berisi hasil konversi. Dan data kedua  `err`, berisi informasi errornya (jika memang terjadi error ketika proses konversi).

Setelah itu dilakukan pengecekkan, ketika tidak ada error,  `number`  ditampilkan. Dan jika ada error,  `input`  ditampilkan beserta pesan errornya.

Pesan error bisa didapat dari method  `Error()`  milik tipe  `error`.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXctohkK31s-5doASeziYlSY4o6coRdvC4CRhFfRYpd-54_zEDQB9aYdbmw9iebyFQoVnWCqvx5RC3ThrZZG3hKJFVCcEMxHZXC-pvV31gRMzFDIHr4OWCS9RQjMOgNFUMbxtKU-Z8TeGYVOUED-TEOUpAs?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.37.2. Membuat Custom Error

Selain memanfaatkan error hasil kembalian suatu fungsi internal yang tersedia, kita juga bisa membuat objek error sendiri dengan menggunakan fungsi  `errors.New()`  (harus import package  `errors`  terlebih dahulu).

Pada contoh berikut ditunjukkan bagaimana cara membuat custom error. Pertama siapkan fungsi dengan nama  `validate()`, yang nantinya digunakan untuk pengecekan input, apakah inputan kosong atau tidak. Ketika kosong, maka error baru akan dibuat.

```
package main

import (
    "errors"
    "fmt"
    "strings"
)

func validate(input string) (bool, error) {
    if strings.TrimSpace(input) == "" {
        return false, errors.New("cannot be empty")
    }
    return true, nil
}
```

Selanjutnya di fungsi main, buat proses sederhana untuk capture inputan user. Manfaatkan fungsi  `validate()`  untuk mengecek inputannya.

```
func main() {
    var name string
    fmt.Print("Type your name: ")
    fmt.Scanln(&name)

    if valid, err := validate(name); valid {
        fmt.Println("halo", name)
    } else {
        fmt.Println(err.Error())
    }
}

```

Fungsi  `validate()`  mengembalikan 2 data. Data pertama adalah nilai  `bool`  yang menandakan inputan apakah valid atau tidak. Data ke-2 adalah pesan error-nya (jika inputan tidak valid).

Fungsi  `strings.TrimSpace()`  digunakan untuk menghilangkan karakter spasi sebelum dan sesudah string. Ini dibutuhkan karena user bisa saja menginputkan spasi lalu enter.

Ketika inputan tidak valid, maka error baru dibuat dengan memanfaatkan fungsi `errors.New()`.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdUo0SosApvY4DK1t-a96dQaHh4VpcM0yBzY_RtVdvA0ETLkKAqnsnanI_C6F2tKmOySs-x8TkAsteZqV9YltGKcy3s-G7N_5_kSKcM-E76BAAY7uj0ANR4r_SNbjhaZlAhnr6k-QmuPS1F6oJkcMPkHEo?key=d3s-vJLBsYtwvRvGfZhdnw)**

Selain menggunakan `errors.New()`, objek error bisa dibuat via fungsi `fmt.Errorf()`. Pengaplikasiannya mirip, perbedaannya fungsi `fmt.Errorf()` mendukung format string.

## A.37.3. Penggunaan  `panic`

Panic digunakan untuk menampilkan  _stack trace_  error sekaligus menghentikan flow goroutine. Setelah ada panic, proses akan terhenti, apapun setelah tidak di-eksekusi kecuali proses yang sudah di-defer sebelumnya (akan muncul sebelum panic error).

> Perlu diingat bahwa  `main()`  juga merupakan goroutine, maka behaviour yang sama adalah berlaku.

Panic menampilkan pesan error di console, sama seperti  `fmt.Println()`. Informasi error yang ditampilkan adalah stack trace error, isinya sangat detail dan heboh.

Kembali ke praktek, pada program yang telah kita buat tadi, ubah  `fmt.Println()`  yang berada di dalam blok kondisi  `else`  pada fungsi main menjadi  `panic()`, lalu tambahkan  `fmt.Println()`  setelahnya.

```
func main() {
    var name string
    fmt.Print("Type your name: ")
    fmt.Scanln(&name)

    if valid, err := validate(name); valid {
        fmt.Println("halo", name)
    } else {
        panic(err.Error())
        fmt.Println("end")
    }
}
```

Jalankan program lalu langsung tekan enter, maka panic error muncul dan baris kode setelahnya tidak dijalankan.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf-vBPhgysFEkS-4iQnkYTsZp2punaSO6blKWvXUnhFHid51tYqjuKsnXwPI6dcR2Qo5zczh8PRqTEh6WXQILwlHdO9aMVlAdXDQDjOD6koHEOkBRvLO6I2yhv3gStW7sR3Yct_W0rXKoFwU9cg8PpmNwS3?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.37.4. Penggunaan  `recover`

Recover berguna untuk meng-handle panic error. Pada saat panic error muncul, recover men-take-over goroutine yang sedang panic dan efek sampingnya pesan panic tidak muncul dan eksekusi program adalah tidak error.

Ok, mari kita modifikasi sedikit fungsi di-atas untuk mempraktekkan bagaimana cara penggunaan recover. Tambahkan fungsi  `catch()`, dalam fungsi ini terdapat statement  `recover()`  yang dia akan mengembalikan pesan panic error yang seharusnya muncul.

Untuk menggunakan recover, fungsi/closure/IIFE di mana  `recover()`  berada harus dieksekusi dengan cara di-defer.

```
func catch() {
    if r := recover(); r != nil {
        fmt.Println("Error occured", r)
    } else {
        fmt.Println("Application running perfectly")
    }
}

func main() {
    defer catch()

    var name string
    fmt.Print("Type your name: ")
    fmt.Scanln(&name)

    if valid, err := validate(name); valid {
        fmt.Println("halo", name)
    } else {
        panic(err.Error())
        fmt.Println("end")
    }
}
```
Output program:

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe81aUs44rHZrBv23doEyWs61X887uZ0AbslVsEtAYHVynjWEXBEVhwa26bHbU-RatfGkJRQlyCJNepwiRnkqZ_KQtqTb_kxIJv-K6mHiUPAjKfwbY74t5fD8Ky5v2HmwX4Tc5DuIqX5A6fku0fuR3eyZil?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.37.5. Pemanfaatan  `recover`  pada IIFE

Contoh penerapan recover pada IIFE:

```
func main() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Panic occured", r)
        } else {
            fmt.Println("Application running perfectly")
        }
    }()

    panic("some error happen")
}
```

Dalam real-world development, ada kalanya recover dibutuhkan tidak dalam blok fungsi terluar, tetapi dalam blok fungsi yg lebih spesifik.

Silakan perhatikan contoh kode recover perulangan berikut. Umumnya, jika terjadi panic error, maka proses proses dalam scope blok fungsi akan terhenti, mengakibatkan perulangan juga akan terhenti secara paksa. Pada contoh berikut kita coba terapkan cara handle panic error tanpa menghentikan perulangan itu sendiri.

```
func main() {
    data := []string{"superman", "aquaman", "wonder woman"}

    for _, each := range data {

        func() {

            // recover untuk IIFE dalam perulangan
            defer func() {
                if r := recover(); r != nil {
                    fmt.Println("Panic occured on looping", each, "| message:", r)
                } else {
                    fmt.Println("Application running perfectly")
                }
            }()

            panic("some error happen")
        }()

    }
}

```

Bisa dilihat di dalam perulangan terdapat sebuah IIFE untuk recover panic dan juga ada kode untuk men-trigger panic error secara paksa. Ketika panic error terjadi, maka idealnya perulangan terhenti, tetapi pada contoh di atas tidak, dikarenakan operasi dalam perulangan sudah di bungkus dalam IIFE dan seperti yang kita tau sifat panic error adalah menghentikan proses secara paksa dalam scope blok fungsi.