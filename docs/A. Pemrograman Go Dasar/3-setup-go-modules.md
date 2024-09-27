---
sidebar_position: 3
---

# A.3. Setup Go Modules

Pada bagian ini kita akan belajar cara pembuatan project baru menggunakan Go Modules.

## A.3.1. Penjelasan

  

Go modules merupakan tools untuk manajemen dependensi resmi milik Go. Modules digunakan untuk menginisialisasi sebuah project, sekaligus melakukan manajemen terhadap _3rd party_ atau _library_ atau _dependency_ yang digunakan dalam project.

Modules penggunaannya adalah via CLI. Jika pembaca sudah sukses meng-_install_ Go, maka otomatis bisa menggunakan operasi CLI Go Modules.

>Di Go, istilah modules (atau module) maknanya adalah sama dengan project. Jadi gak perlu bingung


## A.3.2. Inisialisasi Project Menggunakan Go Modules

Command `go mod init` digunakan untuk menginisialisasi project baru.

Mari langsung praktekan saja. Buat folder baru, bisa via CLI atau lewat browser/finder.
  
```
mkdir project-pertama
cd project-pertama
go mod init project-pertama
```

Bisa dilihat pada _command_ di atas ada direktori `project-pertama`, dibuat. Setelah masuk ke direktori tersebut, perintah `go mod init project-pertama` dijalankan. Dengan ini maka kita telah menginisialisasi direktori/folder `project-pertama` sebagai sebuah project Go dengan nama `project-pertama`.


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfSEIgMEgb3Hx61Nogf914RKNGn01X7_RWLii4Fb8nei1h_FHNHVRFeRPE_bT__bwQDk4DWBzXAJYd_49sX-HmQ7J3PW9QqD7awuXNJkRpOAKTJ0if-svV_OhJDAIU6DotpOnAVvfMYZ5wNgMWCvV2UGGxl?key=d3s-vJLBsYtwvRvGfZhdnw)**


Skema penulisan command `go mod`:

```
go mod init <nama-project>
go mod init project-pertama
```

Di sini kita tentukan nama project adalah sama dengan nama folder, ini merupakan _best practice_ di Go.

  

Eksekusi perintah `go mod init` menghasilkan satu buah file baru bernama `go.mod`. File ini digunakan oleh Go toolchain untuk menandai bahwa folder di mana file tersebut berada adalah folder project. Jadi pastikan untuk tidak menghapus file tersebut.