---
sidebar_position: 2
---

# A.2. Instalasi Golang (Stable & Unstable)


Hal pertama yang perlu dilakukan sebelum bisa menggunakan Go adalah meng-_install_-nya terlebih dahulu. Panduan instalasi sebenarnya sudah disediakan di situs resmi Go [http://golang.org/doc/install#install](http://golang.org/doc/install#install).


Di sini penulis mencoba meringkas petunjuk instalasi pada  _link_  di atas, agar lebih mudah untuk diikuti terutama untuk pembaca yang baru belajar.

> Go yang digunakan adalah versi  **1.22**, direkomendasikan menggunakan versi tersebut.

URL untuk mengunduh  _installer_  Go:  [https://golang.org/dl/](https://golang.org/dl/). Silakan langsung unduh dari  _link_  tersebut lalu lakukan proses instalasi, atau bisa mengikuti petunjuk pada chapter ini.

## A.2.1. Instalasi Go  _Stable_

#### ◉ Instalasi Go di Windows

1.  Download terlebih dahulu  _installer_-nya di  [https://golang.org/dl/](https://golang.org/dl/). Pilih  _installer_  untuk sistem operasi Windows sesuai jenis bit yang digunakan.
    
2.  Setelah ter-_download_, jalankan  _installer_, klik  _next_  hingga proses instalasi selesai.  _By default_  jika anda tidak merubah path pada saat instalasi, Go akan ter-_install_  di  `C:\go`.  _Path_  tersebut secara otomatis akan didaftarkan dalam  `PATH`  _environment variable_.
    
3.  Buka  _Command Prompt_  /  _CMD_, eksekusi perintah berikut untuk mengecek versi Go.
	```
	go version
	```
4.   Jika output adalah sama dengan versi Go yang ter-_install_, menandakan proses instalasi berhasil.


>Sering terjadi, command `go version` tidak bisa dijalankan meskipun instalasi sukses. Solusinya bisa dengan restart CMD (tutup CMD, kemudian buka lagi). Setelah itu coba jalankan ulang command di atas.

#### ◉ Instalasi Go di MacOS

Cara termudah instalasi Go di MacOS adalah menggunakan  [Homebrew](http://brew.sh/).

1.  _Install_  terlebih dahulu Homebrew (jika belum ada), caranya jalankan perintah berikut di  **terminal**.
	```
	$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
	```
2.  _Install_  Go menggunakan command  `brew`.
    
    ```
    $ brew install go
    ```
3.  Tambahkan path binary Go ke  `PATH`  _environment variable_.
    
    ```
    $ echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.bash_profile
    $ source ~/.bash_profile
    ```
4.  Jalankan perintah berikut mengecek versi Go.
    
    ```
    go version
    ```
5.  Jika output adalah sama dengan versi Go yang ter-_install_, menandakan proses instalasi berhasil.


#### ◉ Instalasi Go di Linux

1.  Unduh arsip  _installer_  dari  [https://golang.org/dl/](https://golang.org/dl/), pilih installer untuk Linux yang sesuai dengan jenis bit komputer anda. Proses download bisa dilakukan lewat CLI, menggunakan  `wget`  atau  `curl`.
    
    ```
    $ wget https://storage.googleapis.com/golang/go1...
    
    ```
    
2.  Buka terminal,  _extract_  arsip tersebut ke  `/usr/local`.
    
    ```
    $ tar -C /usr/local -xzf go1...
    
    ```
    
3.  Tambahkan path binary Go ke  `PATH`  _environment variable_.
    
    ```
    $ echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.bashrc
    $ source ~/.bashrc
    ```
    
4.  Selanjutnya, eksekusi perintah berikut untuk mengetes apakah Go sudah terinstal dengan benar.
    
    ```
    go version
    ```
    
5.  Jika output adalah sama dengan versi Go yang ter-_install_, menandakan proses instalasi berhasil.

## A.2.2. Variabel  `GOROOT`

_By default_, setelah proses instalasi Go selesai, secara otomatis akan muncul  _environment variable_  `GOROOT`. Isi dari variabel ini adalah lokasi di mana Go ter-_install_.

Sebagai contoh di Windows, ketika Go di-_install_  di  `C:\go`, maka path tersebut akan menjadi isi dari  `GOROOT`.

Silakan gunakan command  `go env`  untuk melihat informasi konfigurasi  _environment_  yang ada.

## A.2.3. Instalasi Go  _Unstable_/_Development_
    

Jika pembaca tertarik untuk mencoba versi development Go, ingin mencoba fitur yang belum dirilis secara official, ada beberapa cara:

-   Instalasi dengan  _build from source_  [https://go.dev/doc/install/source](https://go.dev/doc/install/source)
-   Gunakan command  `go install`, contohnya seperti  `go install  [golang.org/dl/go1.18beta1@latest](http://golang.org/dl/go1.18beta1@latest)`. Untuk melihat versi unstable yang bisa di-install silakan merujuk ke  [https://go.dev/dl/#unstable](https://go.dev/dl/#unstable)