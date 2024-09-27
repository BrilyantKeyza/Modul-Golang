---
sidebar_position: 7
---

# A.7. Program Pertama: Hello World


Semua persiapan sudah selesai, saatnya masuk pada sesi programming. Program pertama yang akan kita buat adalah cukup terkenal di kalangan programmer, yaitu program untuk memunculkan text  **Hello world**.

Proses pembelajaran di chapter ini akan disampaikan secara runtun dan komprehensif,  _step-by-step_  mulai dari awal. Mulai dari pembuatan project, pembuatan file program, sesi penulisan kode (coding), hingga eksekusi program.

## A.7.1. Inisialisasi Project

Buat direktori bernama  `hello-world`  bebas ditempatkan di mana. Lalu via CLI, masuk ke direktori tersebut dan jalankan  _command_  untuk inisialisasi project.

```
mkdir hello-world
cd hello-world
go mod init hello-world
```
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeZz1u-xC6aTT15WYCyjBTXynOe4miBtu9uRlSvl6aaaiyTVpVx9JY4JCFL9F8xt_mxwyP1vHQ8NL8PlGPecqhlMeVWwM8EnVUVfqm_Wv8U7XRMfptVMB1pFUgewcOaPpPa6t1k3scgKRam48TAiYxG-Kyd?key=d3s-vJLBsYtwvRvGfZhdnw)**
## A.7.2. Load Project Folder ke Editor

Buka editor, di sini penulis menggunakan VSCode. Cari menu untuk menambahkan project, lalu pilih project folder  `hello-world`. Untuk beberapa jenis editor, cara load project bisa cukup dengan klik-drag folder tersebut ke editor.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf-eubt87-a67HLAnkhpBSrpTI-0pPDsokLoX1nHF7_HcdkXMgc6rBKoWbq-GfSZRDapTRirLaJkSjx8AU52j7xdOA2c4cV4JNGdWaSFUOnDmwNXTiqRPmRrJ8YMhORDbSJHEBG7uo1i8erC7scMVOli8Mb?key=d3s-vJLBsYtwvRvGfZhdnw)**
## A.7.3. Menyiapkan File Program
File program di sini maksudnya adalah file yang isinya  _source code_  Go. Ciri khas file program adalah memiliki ekstensi  `.go`.

Di dalam project yang telah dibuat, siapkan sebuah file dengan nama bebas, yang jelas harus ber-ekstensi  `.go`. Pada contoh ini saya menggunakan nama file  `main.go`.

Pembuatan file program bisa dilakukan lewat CLI atau browser, atau juga lewat editor. Pastikan file dibuat dalam project folder ya.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeOICS121KfGsBeV79_PErn5JGoTK9eHPXdqwHLD_i4iWPmHbcJtzTSx3DYzxQbnfegr3Z-WhulgyB3oNZjfpRpwB0mPtI1jKqASZiXp3S-jDRl82WlyXAOh1jshHhuzNrOwG-sr28xXB-4gaHKdAEODPBW?key=d3s-vJLBsYtwvRvGfZhdnw)**
## A.7.4. Program Pertama: Hello Word

Setelah project folder dan file program sudah siap, saatnya untuk  _coding_.

Silakan salin kode berikut ke file program yang telah dibuat. Sebisa mungkin jangan copy paste. Biasakan untuk menulis dari awal, agar cepat terbiasa dan familiar dengan Go.

```
package main

import "fmt"

func main() {
    fmt.Println("Hello world")
}
```
Setelah kode disalin, buka terminal (atau CMD bagi pengguna Windows), lalu masuk ke direktori proyek, kemudian jalankan program menggunakan perintah `go run`.

```
cd hello-world
go run main.go
```
Hasilnya, muncul tulisan **hello world** di layar console.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXephazpzDdkkHup6tmDpmEf3VFdiKb6dSkhxvPDhKeaJGpmWEARgnmGTiqhTFuL2IrDTWvXmObB0oRYQaZJcYrb6UaFE7Bc4fyEZxesYR4nz5pMKT7bLvaMWYYBTogBs9yEcsXVWZ8l4lx12KmnVaD7zqWC?key=d3s-vJLBsYtwvRvGfZhdnw)**
Selamat! Anda telah berhasil membuat program Go!

Berikut merupakan pembahasan untuk tiap baris kode yang sudah ditulis di atas.

## A.7.5. Penggunaan Keyword  `package`

Setiap file program harus memiliki  **package**. Setiap project harus ada minimal satu file dengan nama  _package_  `main`. File yang ber-_package_  `main`, akan dieksekusi pertama kali ketika program di jalankan.

Cara menentukan  _package_  dengan menggunakan keyword  `package`, berikut adalah contoh penulisannya.

```
package <nama-package>
package main
```

## A.7.6. Penggunaan Keyword  `import`

Keyword  `import`  digunakan untuk meng-_import_  atau memasukan  _package_  lain ke dalam file program, agar isi dari package yang di-_import_  bisa dimanfaatkan.

_Package_  `fmt`  merupakan salah satu  _package_  bawaan yang disediakan oleh Go, isinya banyak fungsi untuk keperluan  **I/O**  yang berhubungan dengan text.

Berikut adalah skema penulisan keyword  `import`:

```
import "<nama-package>"
import "fmt"
```

## A.7.7. Penggunaan Fungsi  `main()`

Dalam sebuah proyek harus ada file program yang di dalamnya berisi sebuah fungsi bernama  `main()`. Fungsi tersebut harus berada di file yang package-nya bernama  `main`.

Fungsi  `main()`  adalah yang dipanggil pertama kali pada saat eksekusi program. Contoh penulisan fungsi  `main`:

```
func main() {

}
```

## A.7.8. Penggunaan Fungsi  `fmt.Println()`

Fungsi  `fmt.Println()`  digunakan untuk memunculkan text ke layar (pada konteks ini, terminal atau CMD). Di program pertama yang telah kita buat, fungsi ini memunculkan tulisan  **Hello world**.

Skema penulisan keyword  `fmt.Println()`  bisa dilihat pada contoh berikut.

```
fmt.Println("<isi-pesan>")
fmt.Println("Hello world")
```
Fungsi  `fmt.Println()`  berada dalam package  `fmt`, maka untuk menggunakannya perlu package tersebut untuk di-import terlebih dahulu.

Fungsi  `fmt.Println()`  dapat menampung parameter yang tidak terbatas jumlahnya. Semua data parameter akan dimunculkan dengan pemisah tanda spasi.

```
fmt.Println("Hello", "world!", "how", "are", "you")

```

Contoh statement di atas akan menghasilkan output:  **Hello world! how are you**.