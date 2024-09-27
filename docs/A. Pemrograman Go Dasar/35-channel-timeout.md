---
sidebar_position: 35
---

# A.35. Channel - Timeout


Teknik channel timeout digunakan untuk kontrol waktu penerimaan data pada channel, berapa lama channel tersebut harus menunggu hingga akhirnya suatu penerimaan data dianggap timeout.

Durasi penerimaan kita tentukan sendiri. Ketika tidak ada aktivitas penerimaan data dalam durasi tersebut, blok timeout dijalankan.

## A.35.1. Penerapan Channel Timeout

Berikut adalah program sederhana contoh pengaplikasian timeout pada channel. Sebuah goroutine dijalankan dengan tugas adalah mengirimkan data secara berulang dalam interval tertentu, dengan durasi interval-nya sendiri adalah acak/random.

```
package main

import "fmt"
import "math/rand"
import "runtime"
import "time"

func sendData(ch chan<- int) {
    randomizer := rand.New(rand.NewSource(time.Now().Unix()))

    for i := 0; true; i++ {
        ch <- i
        time.Sleep(time.Duration(randomizer.Int()%10+1) * time.Second)
    }
}
```

Selanjutnya, disiapkan perulangan tanpa henti, yang di setiap perulangan ada seleksi kondisi channel menggunakan  `select`.

```
func retreiveData(ch <-chan int) {
    loop:
    for {
        select {
        case data := <-ch:
            fmt.Print(`receive data "`, data, `"`, "\n")
        case <-time.After(time.Second * 5):
            fmt.Println("timeout. no activities under 5 seconds")
            break loop
        }
    }
}
```

Ada 2 blok kondisi pada  `select`  tersebut.

-   Kondisi  `case data := <-messages:`, akan terpenuhi ketika ada serah terima data pada channel  `messages`.
-   Kondisi  `case <-time.After(time.Second * 5):`, akan terpenuhi ketika tidak ada aktivitas penerimaan data dari channel dalam durasi 5 detik. Blok inilah yang kita sebut sebagai blok timeout.

Terakhir, kedua fungsi tersebut dipanggil di  `main()`.
```
func main() {
    runtime.GOMAXPROCS(2)

    var messages = make(chan int)

    go sendData(messages)
    retreiveData(messages)
}
```
Muncul output setiap kali ada penerimaan data dengan delay waktu acak. Ketika dalam durasi 5 detik tidak ada aktivitas penerimaan sama sekali, maka dianggap timeout dan perulangan pengecekkan channel dihentikan.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcmdRX2KjTp3qfSuoENBDl8zRzebE58J2Tj0_i1nsbg35LHV4jlZw9jRrv5jFwfcFS5STpBiGlgYB_x61Jv3Fv2HE31PBY17C4AN8cSaOEZ5ImgfUoM5omjZnTeCFRlZByXt8n50G-zgOE-nfYfDcR2Ljwk?key=d3s-vJLBsYtwvRvGfZhdnw)**