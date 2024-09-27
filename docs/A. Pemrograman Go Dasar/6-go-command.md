---
sidebar_position: 6
---

# A.6. Go Command


Pengembangan aplikasi Go pastinya tak akan jauh dari hal-hal yang berbau CLI atau  _Command Line Interface_. Di Go, proses inisialisasi project, kompilasi, testing, eksekusi program, semuanya dilakukan lewat command line.

Go menyediakan command  `go`, dan pada chapter ini kita akan mempelajari beberapa di antaranya.

>Pada pembelajaran chapter ini, pembaca tidak harus menghafal dan mempraktekan semuanya, cukup ikuti saja pembelajaran agar mulai familiar. Perihal prakteknya sendiri akan dimulai pada chapter selanjutnya, yaitu A.7. Program Pertama: Hello World.

## A.6.1. Command  `go mod init`

_Command_  `go mod init`  digunakan untuk inisialisasi project pada Go yang menggunakan Go Modules. Untuk nama project bisa menggunakan apapun, tapi umumnya disamakan dengan nama direktori/folder.

Nama project ini penting karena nantinya berpengaruh pada  _import path sub packages_  yang ada dalam project tersebut.

```
mkdir <nama-project>
cd <nama-project>
go mod init <nama-project>
```
## A.6.2. Command  `go run`

_Command_  `go run`  digunakan untuk eksekusi file program, yaitu file yang ber-ekstensi  `.go`. Cara penggunaannya dengan menuliskan  _command_  tersebut diikuti argumen nama file.

Berikut adalah contoh penerapan  `go run`  untuk eksekusi file program  `main.go`  yang tersimpan di path  `project-pertama`  yang path tersebut sudah diinisialisasi menggunakan  `go mod init`.

```
cd project-pertama
go run main.go
```


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc8aYK9AFvxcDDSsQtS6bSg5NXqA1weNInnt9BlUbRY5JZ5q8hNNYXJ7IY-BmGaSqRQ_fbsCY46YwVX9t7qMRAsi9kBj433yZKhEZ76_109tTjpisqj4DZq9c97VtZLt7Kf9zndxkoIlbRfAX4FpDk0sKC1?key=d3s-vJLBsYtwvRvGfZhdnw)**


_Command_  `go run`  hanya bisa digunakan pada file yang nama package-nya adalah  `main`. Lebih jelasnya dibahas pada chapter selanjutnya, yaitu (A.7. Program Pertama: Hello World).

Jika ada banyak file yang package-nya  `main`  dan file-file tersebut berada pada satu direktori level dengan file utama, maka eksekusinya adalah dengan menuliskan semua file sebagai argument  _command_  `go run`. Contohnya bisa dilihat pada kode berikut.

```
go run main.go library.go
```
## A.6.3. Command  `go test`

Go menyediakan package  `testing`, berguna untuk keperluan pembuatan file test. Pada penerapannya, ada aturan yang wajib diikuti yaitu nama file test harus berakhiran  `_test.go`.

Berikut adalah contoh penggunaan  _command_  `go test`  untuk testing file  `main_test.go`.

```
go test main_test.go
```
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdqowQqhOuwxDuINnf4CTW8KFdIKrEaNyvjYu53RYgvpCjyWlmRMGHSBsmq69yzn9sSs5APA9xn6ErNuOaUibb0GviXiAfOtS0NWnTydKwhP2GWvb6STl8d-Bdtvstg8DX-gVR7gQTnz5Q_owzvGxn_jpU?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.6.4. Command  `go build`
_Command_  ini digunakan untuk mengkompilasi file program.

Sebenarnya ketika eksekusi program menggunakan  `go run`  didalamnya terjadi proses kompilasi juga. File hasil kompilasi kemudian disimpan pada folder temporary untuk selanjutnya langsung dieksekusi.

Berbeda dengan  `go build`,  _command_  ini menghasilkan file  _executable_  atau  _binary_  pada folder yang sedang aktif. Contoh praktiknya bisa dilihat di bawah ini.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc0qT1HENihLM8x42u9JyshYp5v2FVL9zwtyER9z2ErZPd1tVaKEEcV_DTudqazHpX9TwLasio5h66DhPLn_hTZ98YO6I5-FLIF0mF9TkBMGKB1GjPte2GO_3_dJxdQ-ghyukA4Tg3_uUS6m7a3Q6Ruj5nh?key=d3s-vJLBsYtwvRvGfZhdnw)**

Di contoh, project  `project-pertama`  di-build, hasilnya adalah file baru bernama  `project-pertama.exe`  berada di folder yang sama. File  _executable_  tersebut kemudian dieksekusi.

_Default_  nama file binary atau executable adalah sesuai dengan nama project. Untuk mengubah nama file executable, gunakan flag  `-o`. Contoh:
```
go build -o <nama-executable>
go build -o program.exe
```
>Khusus untuk sistem operasi non-windows, tidak perlu menambahkan akhiran .exe pada nama binary

## A.6.5. Command  `go get`

_Command_  `go get`  digunakan untuk men-download package atau  _dependency_. Sebagai contoh, penulis ingin men-download package Kafka driver untuk Go pada project  `project-pertama`, maka command-nya kurang lebih seperti berikut:

```
cd project-pertama
go get github.com/segmentio/kafka-go
```
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe-yLO7Zt1tIRKSrO-lvlFhpXstKBpCYSiOINMo13lZ8gSQIXe--tJmXrSfKUXrTNvXmbirdCc-edafpbtcWnJFqqzRGVxkKw9ET6bKsBUPjH9ok31jAOG_XLnlOVv1XHmq8T7sHySivdzrwdpp0RZ8g90?key=d3s-vJLBsYtwvRvGfZhdnw)**

Pada contoh di atas, bisa dilihat bahwa URL  [github.com/segmentio/kafka-go](http://github.com/segmentio/kafka-go)  merupakan URL package kafka-go. Package yang sudah terunduh tersimpan dalam temporary folder yang ter-link dengan project folder di mana  _command_  `go get`  dieksekusi, menjadikan project tersebut bisa meng-_import_  package yang telah di-download.

Untuk mengunduh package/dependency versi terbaru, gunakan flag  `-u`  pada command  `go get`, contohnya:

```
go get -u github.com/segmentio/kafka-go
```
Command `go get`  **harus dijalankan dalam folder project**. Jika dijalankan di-luar path project maka dependency yang ter-unduh akan ter-link dengan GOPATH, bukan dengan project.

## A.6.6. Command  `go mod download`

_Command_  `go mod download`  digunakan untuk men-download dependency.

## A.6.7. Command  `go mod tidy`

_Command_  `go mod tidy`  digunakan untuk memvalidasi dependency sekaligus men-download-nya jika memang belum ter-download.

## A.6.8. Command  `go mod vendor`

Command ini digunakan untuk vendoring. Lebih detailnya akan dibahas di akhir serial chapter A, pada chapter A.61. Go Vendoring.