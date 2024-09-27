---
sidebar_position: 34
---

# A.34. Channel - Range dan Close


Proses penerimaan/_retrieving_  data dari banyak channel bisa lebih mudah dilakukan dengan memanfaatkan kombinasi keyword  `for`  -  `range`. Penerapannnya cukup mudah, yaitu dengan menuliskan keyword  `for`  -  `range`  pada variabel channel.

Cara kerjanya:

-   Transaksi data via channel men-trigger perulangan  `for`  -  `range`. Perulangan akan berlangsung seiring terjadinya pengiriman data ke channel yang di-iterasi.
-   Perulangan tersebut hanya akan berhenti jika channel di-**close**  atau di non-aktifkan via fungsi  `close()`. Channel yang sudah di-close tidak bisa digunakan lagi baik untuk menerima data ataupun untuk mengirim data.
## A.34.1. Penerapan  `for`  -  `range`  -  `close`

Berikut adalah contoh program pengaplikasian  `for`,  `range`, dan  `close`  untuk penerimaan data dari channel.

Pertama siapkan fungsi  `sendMessage()`  yang tugasnya mengirim data via channel. Di dalam fungsi ini dijalankan perulangan sebanyak 20 kali, ditiap perulangannya data dikirim ke channel. Channel di-close setelah semua data selesai dikirim.

```
func sendMessage(ch chan<- string) {
    for i := 0; i < 20; i++ {
        ch <- fmt.Sprintf("data %d", i)
    }
    close(ch)
}
```

Siapkan juga fungsi  `printMessage()`  untuk handle penerimaan data. Di dalam fungsi tersebut, channel di-looping menggunakan  `for`  -  `range`. Di setiap iterasi, data yang diterima dari channel ditampilkan.

```
func printMessage(ch <-chan string) {
    for message := range ch {
        fmt.Println(message)
    }
}
```

Selanjutnya, buat channel baru dalam fungsi  `main()`, jalankan  `sendMessage()`  sebagai goroutine. Dengan ini 20 data yang berada dalam fungsi tersebut dikirimkan via goroutine baru. Tak lupa jalankan juga fungsi  `printMessage()`.

```
func main() {
    runtime.GOMAXPROCS(2)

    var messages = make(chan string)
    go sendMessage(messages)
    printMessage(messages)
}

```

Setelah 20 data yang dikirim sukses diterima, channel  `ch`  di-non-aktifkan dengan adanya statement  `close(ch)`. Statement tersebut menghentikan perulangan channel dalam  `printMessage()`.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeof1qsKKtCDD9Yy19rVDAr37tXhu6vUZn4NTkMVHEd0L7hJlY4GhQ8CpAJLIGw6co5sgwOqmWQDRw9YFve-kVWV3722X-vPxuXZwLdx_SVRVgGg4_Ukt1o-jyfUITXc8JVLERDx27KDJLAe7LSA9JW8beu?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.34.2. Penjelasan tambahan

Berikut merupakan penjelasan tambahan untuk beberapa hal dari kode yang sudah dipraktekan:

#### ◉ Channel Direction

Go mendesain API channel untuk mendukung level akses channel, apakah hanya sebagai penerima, pengirim, atau penerima sekaligus pengirim. Konsep ini disebut dengan  **channel direction**.

Cara pemberian level akses adalah dengan menambahkan tanda  `<-`  sebelum atau setelah keyword  `chan`. Untuk lebih jelasnya bisa dilihat di list berikut.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdQ2rLC6DzkZf265m1-TXAYRNm9Qg-5sxzc0LdN9u-PTUEsQF6DwgyoQhJO5C3dHEW73hArrw30YDJaOlyXV9cAejHzx3omfZmTfLKayWT2GTREbipcY1tptqmlVT4BDXxbYMDSgiQZRmdMLGacCcEGGzpR?key=d3s-vJLBsYtwvRvGfZhdnw)**

Pada kode di atas bisa dilihat bahwa secara default channel akan memiliki kemampuan untuk mengirim dan menerima data. Untuk mengubah channel tersebut agar hanya bisa mengirim atau menerima saja, dengan memanfaatkan simbol  `<-`.

Sebagai contoh fungsi  `sendMessage(ch chan<- string)`  yang parameter  `ch`  dideklarasikan dengan level akses untuk pengiriman data saja. Channel tersebut hanya bisa digunakan untuk mengirim, contohnya:  `ch <- fmt.Sprintf("data %d", i)`.

Dan sebaliknya pada fungsi  `printMessage(ch <-chan string)`, channel  `ch`  hanya bisa digunakan untuk menerima data saja.