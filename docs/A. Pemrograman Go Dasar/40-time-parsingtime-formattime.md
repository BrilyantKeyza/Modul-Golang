---
sidebar_position: 40
---

# A.40. Time, Parsing Time, & Format Time


Pada chapter ini kita akan belajar tentang pemanfaatan data bertipe datetime serta method-method-nya, juga tentang  **format**  &  **parsing**  data  `string`  ke tipe  `time.Time`  dan sebaliknya.

Go menyediakan package  `time`  yang berisikan banyak sekali komponen yang bisa digunakan untuk keperluan pemanfaatan date dan time. Salah satunya adalah  `time.Time`, yang merupakan tipe untuk data tanggal dan waktu di Go.

> Meskipun nama package-nya adalah  `time`, yang dicakup adalah  **date**  dan  **time**, jadi bukan hanya waktu saja.


## A.40.1. Penggunaan  `time.Time`

Tipe  `time.Time`  merupakan representasi untuk objek date-time. Ada 2 cara yang bisa dipilih untuk membuat data bertipe ini.

1.  Menjadikan informasi waktu sekarang sebagai objek  `time.Time`, menggunakan  `time.Now()`.
2.  Atau, membuat objek baru bertipe  `time.Time`  dengan informasi ditentukan sendiri, menggunakan  `time.Date()`.

Berikut merupakan contoh penggunannya.

```
package main

import "fmt"
import "time"

func main() {
    var time1 = time.Now()
    fmt.Printf("time1 %v\n", time1)
    // time1 2015-09-01 17:59:31.73600891 +0700 WIB

    var time2 = time.Date(2011, 12, 24, 10, 20, 0, 0, time.UTC)
    fmt.Printf("time2 %v\n", time2)
    // time2 2011-12-24 10:20:00 +0000 UTC
}
```
Fungsi `time.Now()` mengembalikan objek `time.Time` dengan nilai adalah informasi date-time tepat ketika statement tersebut dijalankan. Bisa dilihat pada saat di-print muncul informasi date-time sesuai dengan tanggal program tersebut dieksekusi.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdhQz_rZCtCLqYdYMgGPjJr7MedWJnjcdDObUfYBvdYiZaiWLJD8OsQLaOSKvJKX9Kuql6Dfw2r1DSDpexWjonSUlpM-F7-1HLXpjSNlwxwdwwjkei5xOAfvi8vB0zR-NgAtIInRidHdgMilIZxLPZDPiuU?key=d3s-vJLBsYtwvRvGfZhdnw)**

Fungsi  `time.Date()`  digunakan untuk membuat objek  `time.Time`  baru yang informasi date-time-nya kita tentukan sendiri. Fungsi ini memiliki 8 buah parameter  _mandatory_  dengan skema bisa dilihat di kode berikut:

```
time.Date(tahun, bulan, tanggal, jam, menit, detik, nanodetik, timezone)
```

Objek cetakan fungsi  `time.Now()`  memiliki timezone yang relatif terhadap lokasi kita. Karena kebetulan penulis berlokasi di Jawa Timur, maka akan terdeteksi masuk dalam  **GMT+7**  atau  **WIB**. Berbeda dengan variabel  `time2`  yang lokasinya sudah kita tentukan secara eksplisit yaitu  **UTC**.

Selain menggunakan  `time.UTC`  untuk penentuan lokasi, tersedia juga  `time.Local`  yang nilainya adalah relatif terhadap date-time lokal kita.

## A.40.2. Method Milik  `time.Time`

Tipe data  `time.Time`  merupakan struct, memiliki beberapa method yang bisa dipakai.

```
var now = time.Now()
fmt.Println("year:", now.Year(), "month:", now.Month())
// year: 2015 month: 8
```
Kode di atas adalah contoh penggunaan beberapa method milik objek bertipe  `time.Time`. Method  `Year()`  mengembalikan informasi tahun, dan  `Month()`  mengembalikan informasi angka bulan.

Selain kedua method di atas, ada banyak lagi yang bisa dimanfaatkan. Tabel berikut merupakan list method yang berhubungan dengan  _date_,  _time_, dan  _location_  yang dimiliki tipe  `time.Time`.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdhKCw_9fJzM3nGgbVEsNLZAtV6aaniVRSWwBWckQZZktddqDmfuYUMgJHLhZEBi18x_X-djD9AzZYI54BbE4w7xDoviiKSG07tvW3a7zJ7ZwyKV3ciwbyuUh35DtBccDGpU1lbrY7pBN2KqcsY3MZ-R9ay?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.40.3. Parsing dari  `string`  ke  `time.Time`

Data  `string`  bisa dikonversi menjadi  `time.Time`  dengan memanfaatkan  `time.Parse`. Fungsi ini membutuhkan 2 parameter:

-   Parameter ke-1 adalah layout format dari data waktu yang akan diparsing.
-   Parameter ke-2 adalah data string yang ingin diparsing.

Contoh penerapannya bisa dilihat di kode berikut.

```
var layoutFormat, value string
var date time.Time

layoutFormat = "2006-01-02 15:04:05"
value = "2015-09-02 08:04:00"
date, _ = time.Parse(layoutFormat, value)
fmt.Println(value, "\t->", date.String())
// 2015-09-02 08:04:00 +0000 UTC

layoutFormat = "02/01/2006 MST"
value = "02/09/2015 WIB"
date, _ = time.Parse(layoutFormat, value)
fmt.Println(value, "\t\t->", date.String())
// 2015-09-02 00:00:00 +0700 WIB
```

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdTzE69fEsBxOo8oiO-qW0INad-VvveelOlhoSUcOjLs0eRHOas2t85e2kEuWgo700D5JF5ooNuY3mVhfWFF-FwWRyyBCgh6mvS-CFwb_VZgXSZPnC-cR-A8wdV0SyTesgphzf_yReFTiOIqfE7Z2qMnQHB?key=d3s-vJLBsYtwvRvGfZhdnw)**

Layout format date-time di Go berbeda dibanding bahasa lain. Umumnya layout format yang digunakan adalah seperti  `"DD/MM/YYYY"`, di Go tidak.

Go memiliki standar layout format yang cukup unik, contohnya seperti pada kode di atas  `"2006-01-02 15:04:05"`. Go menggunakan  `2006`  untuk parsing tahun, bukan  `YYYY`;  `01`  untuk parsing bulan;  `02`  untuk parsing hari; dan seterusnya. Detailnya bisa dilihat di tabel berikut.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfIsqUg-akh6KOT50gQtvpnhOfEhvulTeyhCII8SNm2L7nZ-w7VW3TdJlKXE_Eil9S6pVISMSRkzRYbTQyUN62AIlEMtbM62Brz0NfUtfYeSlZ_fcR2E0SN30KVQy1Os5BPXoY3fbhVHwn-YNib3VsupkIX?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.40.4. Predefined Layout Format Untuk Keperluan Parsing Time

Go juga menyediakan beberapa predefined layout format umum yang bisa dimanfaatkan. Jadi tidak perlu menuliskan kombinasi komponen-komponen layout format.

Salah satu predefined layout yang bisa digunakan adalah  `time.RFC822`, ekuivalen dengan layout format  `02 Jan 06 15:04 MST`. Berikut adalah contoh penerapannya.

```
var date, _ = time.Parse(time.RFC822, "02 Sep 15 08:00 WIB")
fmt.Println(date.String())
// 2015-09-02 08:00:00 +0700 WIB
```
Ada beberapa layout format lain yang tersedia, silakan lihat tabel berikut.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXddLhcb-JNG1jynzPjWj9qDT-G6aED9_Dx3O4KH81paH1N55pv2Ui-C6_kazvCLo9n5BoON_RB4XnMP3LtSMK-XWs7F6gJiwBCeWeg1e0Z17ArVfRF5YRu1Mkn1wzUqcKbR0SoTqOuYSeUCuJXpcr1fGlqc?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.40.5. Format dari  `time.Time`  ke  `string`

Setelah sebelumnya kita belajar tentang cara konversi data dengan tipe  `string`  ke  `time.Time`. Kali ini kita akan belajar kebalikannya, konversi  `time.Time`  ke  `string`.

Method  `Format()`  milik tipe  `time.Time`  digunakan untuk membentuk output  `string`  sesuai dengan layout format yang diinginkan. Contoh bisa dilihat pada kode berikut.

```
var date, _ = time.Parse(time.RFC822, "02 Sep 15 08:00 WIB")

var dateS1 = date.Format("Monday 02, January 2006 15:04 MST")
fmt.Println("dateS1", dateS1)
// Wednesday 02, September 2015 08:00 WIB

var dateS2 = date.Format(time.RFC3339)
fmt.Println("dateS2", dateS2)
// 2015-09-02T08:00:00+07:00
```

Variabel  `date`  di atas berisikan hasil parsing data dengan format  `time.RFC822`. Data tersebut kemudian diformat sebagai string 2 kali dengan layout format berbeda.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcf8R0A13yYBaOAScEwwqVgBbOnK1FK-jNddfjVR1on4sysargxDbVDuXPuMPGMPsqfljDFbdFHNEV1AfXxt_nIbUUoMUD8YHu9m9VdTc0kiUsgQjW3W3_-YEi_yqfMP4nPVH3zfRqH4I8QMPCFZMUKhgJx?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.40.6. Handle Error Parsing  `time.Time`

Parsing  `string`  ke  `time.Time`  memungkinkan terjadinya error, misalnya karena struktur data yang akan di-parse tidak sesuai layout format yang digunakan. Error-tidaknya parsing bisa diketahui lewat nilai kembalian ke-2 fungsi  `time.Parse()`. Contoh:

```
var date, err = time.Parse("06 Jan 15", "02 Sep 15 08:00 WIB")

if err != nil {
    fmt.Println("error", err.Error())
    return
}

fmt.Println(date)

```

Kode di atas menghasilkan error karena format tidak sesuai dengan skema data yang akan diparsing. Layout format yang seharusnya digunakan adalah  `06 Jan 15 03:04 MST`.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfcqr6ppzm59tT2hJF8MYlQKNSn-C25VhQ7pEkiTkMhuN2B2fXmL0n-ADG4oN2QdY5V8EM_64b-5EiSrVATObcnr8ZElMFtSgfGGRuhl898rxoN8EQUY41-_CzHTLBvUc0p32Bnw2vdZKgBcKakwudKsGQa?key=d3s-vJLBsYtwvRvGfZhdnw)**