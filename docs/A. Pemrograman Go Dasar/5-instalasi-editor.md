---
sidebar_position: 5
---

# A.5. Instalasi Editor


Proses pembuatan aplikasi menggunakan Go akan lebih maksimal jika didukung oleh editor atau **IDE** yang pas. Ada cukup banyak pilihan bagus yang bisa dipertimbangkan, di antaranya: JetBrains GoLand, Visual Studio Code, Netbeans, Atom, Sublime Text, dan lainnya.

Penulis sarankan untuk memilih editor yang paling nyaman digunakan, preferensi masing-masing pastinya berbeda. Penulis sendiri lebih sering menggunakan Visual Studio Code. Editor ini sangat ringan, mudah didapat, dan memiliki ekstensi yang bagus untuk bahasa Go. Jika pembaca ingin menggunakan editor yang sama, maka silakan melanjutkan panduan berikut.

## A.5.1. Instalasi Editor Visual Studio Code

1.  Download Visual Studio Code di  [https://code.visualstudio.com/Download](https://code.visualstudio.com/Download), pilih sesuai dengan sistem operasi yang digunakan.
2.  Jalankan  _installer_.
3.  Setelah selesai, jalankan editornya.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd9wIVqz-I1RWDT6vv_OW57HHDbhnxqL0tnUB6cB_a4LxZ2T0SZWA7bHJFTvz0oY8Zlhq5omD6vGCT8mCj1ze_4pVzHRD92qnZjiV5JrLcZ8DV9LHrVHN0hL6lnfd_fqVTFJ5kQK4l0UAL6f3y8ifU-EB46?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.5.2. Instalasi Extensi Go

Dengan meng-_install_ Go Extension pada VSCode, maka development akan menjadi lebih menyenangkan dan mudah. Banyak benefit yang didapat dari ekstensi ini, beberapa di antaranya adalah integrasi dengan kompiler Go, auto lint on save, testing with coverage, fasilitas debugging with breakpoints, dan lainnya.

Cara instalasi ekstensi sendiri cukup mudah, klik `View -> Extension` atau klik ikon _Extension Marketplace_ di sebelah kiri (silakan lihat gambar berikut, deretan button paling kiri yang dilingkari merah). Setelah itu ketikan **Go** pada inputan search, silakan install ekstensi Go buatan GO Team at Google, biasanya muncul paling atas sendiri.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcypLjGKrExfaFgDfLl8Ha0Rb1JJUJI6aTbPQeeEMaTtkHs6BAkRj4cxD2EKm4sfz4TUmCs-q-lWIhwNELHwApIgJfNVTAMFVfH8RM4ie0t6xCQoX5Lio3fJkIAWYh7-8-UxSdAiuvgA3Q17H1lXMsRjty7?key=d3s-vJLBsYtwvRvGfZhdnw)**
## A.5.3. Setup Editorconfig
[Editorconfig](https://editorconfig.org/) membantu kita supaya _coding style_ menjadi konsisten untuk dibaca oleh banyak developer, dan juga ketika dimuat pada berbagai macam **IDE**. Instalasinya di VSCode cukup mudah, cari saja _extension_-nya kemudian klik _install_ seperti pada gambar berikut.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXetf5CLVgviqvO95Z6lPJgRSgEwXk2z1CugcTqdurHKNPIh4onwBhh_O7miHnRcETdCjq0hpRr37NBDix5_gGdWcy2w9jejAAht8bviIrYboOWZ5ci1YCVkEFdbj3RigiSRxgpU65o7novypK4L8kAVrfwe?key=d3s-vJLBsYtwvRvGfZhdnw)**


Editorconfig pada sebuah proyek (biasanya berada di root direktori proyek tersebut) berupa konfigurasi format file `.editorconfig` yang berisi definisi style penulisan yang menyesuaikan dengan standar penulisan masing-masing bahasa pemrograman. Misalnya untuk [_style guide_  **GO**](https://golang.org/doc/effective_go.html) kita bisa mulai dengan menggunakan konfigurasi sederhana sebagai berikut:

```
root = true

[*]
insert_final_newline = true
charset = utf-8
trim_trailing_whitespace = true
indent_style = space
indent_size = 2

[{Makefile,go.mod,go.sum,*.go}]
indent_style = tab
indent_size = 8
```