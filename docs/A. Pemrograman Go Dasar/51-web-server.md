---
sidebar_position: 51
---

# A.51. Web Server


Go menyediakan package  `net/http`, berisi berbagai macam fitur untuk keperluan pembuatan aplikasi berbasis web. Termasuk di dalamnya mencakup web server, routing, templating, dan lainnya.

Go memiliki web server sendiri, tersedia dalam package Go yang bisa kita import dengan mudah. Jadi berbeda dibanding beberapa bahasa lain yang servernya terpisah yang perlu diinstal sendiri (seperti PHP yang memerlukan Apache, .NET yang memerlukan IIS).

Pada chapter ini kita akan belajar cara pembuatan aplikasi web sederhana dan pemanfaatan template untuk mendesain view.

## A.51.1. Membuat Aplikasi Web Sederhana

Package  `net/http`  memiliki banyak sekali fungsi yang bisa dimanfaatkan. Di bagian ini kita akan mempelajari beberapa fungsi penting seperti  _routing_  dan  _start server_.

Program di bawah ini merupakan contoh sederhana untuk memunculkan text di web ketika url tertentu diakses.

```
package main

import "fmt"
import "net/http"

func index(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "apa kabar!")
}

func main() {
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintln(w, "halo!")
    })

    http.HandleFunc("/index", index)

    fmt.Println("starting web server at http://localhost:8080/")
    http.ListenAndServe(":8080", nil)
}
```
Jalankan program tersebut.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXft_A535KQEgYSEdTOO-c6lRsQeu-L2jixBMR9dnaOwSWRc5Iv87w73HVru94gg0H-1CHgrYsHRehCJgC_SUbGxr0MyWB0MdfgImvDUwauW9SrMs_GgbEA1dM0zKSxyS1gPN8o3HrMr_ad9fMM_07r4quty?key=d3s-vJLBsYtwvRvGfZhdnw)**

Jika muncul dialog  **Do you want the application “bab48” to accept incoming network connections?**  atau sejenis, pilih allow. Setelah itu, buka url  [http://localhost/](http://localhost/)  dan  [http://localhost/index](http://localhost/index)  di browser.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeyVSsyWyapICJkuN3DTi8ibtDto2b3o6lXiOjqW077Atlklblkgt0r_Dtunjkrl8ugUaEAFGQwg1j9bhArZqSAgnlrk4Y1iY2YMJHJSfPxxMV_NRBXSXZWIxYIUFFXFsCPw4lT1FxypY1b3uNWGZjoDjvM?key=d3s-vJLBsYtwvRvGfZhdnw)**

Fungsi  `http.HandleFunc()`  digunakan untuk routing aplikasi web. Maksud dari routing adalah penentuan aksi ketika url tertentu diakses oleh user.

Pada kode di atas 2 rute didaftarkan, yaitu  `/`  dan  `/index`. Aksi dari rute  `/`  adalah menampilkan text  `"halo"`  di halaman website. Sedangkan  `/index`  menampilkan text  `"apa kabar!"`.

Fungsi  `http.HandleFunc()`  memiliki 2 buah parameter yang harus diisi. Parameter pertama adalah rute yang diinginkan. Parameter kedua adalah  _callback_  atau aksi ketika rute tersebut diakses. Callback tersebut bertipe fungsi  `func(w http.ResponseWriter, r *http.Request)`.

Pada pendaftaran rute  `/index`, callback-nya adalah fungsi  `index()`, hal seperti ini diperbolehkan asalkan tipe dari fungsi tersebut sesuai.

Fungsi  `http.listenAndServe()`  digunakan untuk menghidupkan server sekaligus menjalankan aplikasi menggunakan server tersebut. Di Go, 1 web aplikasi adalah 1 buah server berbeda.

Pada contoh di atas, server dijalankan pada port  `8080`.

Perlu diingat, setiap ada perubahan pada file  `.go`,  `go run`  harus dipanggil lagi.

Untuk menghentikan web server, tekan  **CTRL+C**  pada terminal atau CMD, di mana pengeksekusian aplikasi berlangsung.

## A.51.2. Penggunaan Template Web

Template engine memberikan kemudahan dalam mendesain tampilan view aplikasi website. Dan kabar baiknya Go menyediakan engine template sendiri, dengan banyak fitur yang tersedia di dalamnya.

Di sini kita akan belajar contoh sederhana penggunaan template untuk menampilkan data. Pertama siapkan dahulu template-nya. Buat file  `template.html`  lalu isi dengan kode berikut.

```
<html>
    <head>
        <title>Go learn net/http</title>
    </head>
    <body>
        <p>Hello {{.Name}} !</p>
        <p>{{.Message}}</p>
    </body>
</html>
```

Kode  `{{.Name}}`  artinya memunculkan isi data property  `Name`  yang dikirim dari router. Kode tersebut nantinya di-replace dengan isi variabel  `Name`.

Selanjutnya ubah isi file  `.go`  dengan kode berikut.

```
package main

import "fmt"
import "html/template"
import "net/http"

func main() {
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        var data = map[string]string{
            "Name":    "john wick",
            "Message": "have a nice day",
        }

        var t, err = template.ParseFiles("template.html")
        if err != nil {
            fmt.Println(err.Error())
            return
        }

        t.Execute(w, data)
    })

    fmt.Println("starting web server at http://localhost:8080/")
    http.ListenAndServe(":8080", nil)
}
```

Jalankan, lalu buka  [http://localhost:8080](http://localhost:8080/), maka data  `Nama`  dan  `Message`  akan muncul di view.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcuZ2MZ6hnymiGdR-Qo1hmuN8jOdOYQHNwvQ8yZJ9Ex0HJz6u7RuutnOff7PUT9hFHsodPM5FUSgUH9oGQ47zP6xaxzpl-rtk__cp3LJYy-orNfd18Oja2FAe2PcAEmlmyI8itHhSh2tM0NQZ6Gev1A6NM?key=d3s-vJLBsYtwvRvGfZhdnw)**

Fungsi  `template.ParseFiles()`  digunakan untuk parsing template, mengembalikan 2 data yaitu instance template-nya dan error (jika ada). Pemanggilan method  `Execute()`  akan membuat hasil parsing template ditampilkan ke layar web browser.

Pada kode di atas, variabel  `data`  disisipkan sebagai parameter ke-2 method  `Execute()`. Isi dari variabel tersebut bisa diakses di-view dengan menggunakan notasi  `{{.NAMA_PROPERTY}}`  (nama variabel sendiri tidak perlu dituliskan, langsung nama property di dalamnya).

Pada contoh di atas, statement di view  `{{.Name}}`  akan menampilkan isi dari  `data.Name`.


## A.51.3. Advanced Web Programming

Sampai chapter ini yang kita pelajari adalah yang sifatnya fundamental atau dasar di pemrograman Go. Nantinya di chapter  [B.1. Golang Web App: Hello World](https://dasarpemrogramangolang.novalagung.com/B-golang-web-hello-world.html)  hingga seterusnya akan lebih banyak membahas mengenai pemrograman web. Jadi untuk sekarang sabar dulu ya. Mari kita selesaikan pembelajaran fundamental secara runtun, sebelum masuk ke bagian pengembangan web.