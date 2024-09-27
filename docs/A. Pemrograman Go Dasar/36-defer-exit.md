---
sidebar_position: 36
---

# A.36. Defer & Exit


**Defer** digunakan untuk mengakhirkan eksekusi sebuah statement tepat sebelum blok fungsi selesai. Sedangkan **Exit** digunakan untuk menghentikan program secara paksa (ingat, menghentikan program, tidak seperti `return` yang hanya menghentikan blok kode).

## A.36.1. Penerapan keyword  `defer`

Seperti yang sudah dijelaskan singkat di atas, bahwa defer digunakan untuk mengakhirkan eksekusi baris kode  **dalam skope blok fungsi**. Ketika eksekusi blok sudah hampir selesai, statement yang di-defer dijalankan.

Defer bisa ditempatkan di mana saja, awal maupun akhir blok. Tetapi tidak mempengaruhi kapan waktu dieksekusinya, akan selalu dieksekusi di akhir.

```
package main

import "fmt"

func main() {
    defer fmt.Println("halo")
    fmt.Println("selamat datang")
}
```

Output program:

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcY_ndGUiDlGZuw2WnNsyLA4t8zpMnKLcLUF1_PykZ4uwhMyAyW2sh1vYlBPtF3-fbLujL3XnlGYHYfX2BosMP4G8dpdOTO97CmeiGXXT7NPEDmaJkGC29KpEmxksnq4oJw3B1A9_EUB-OTT6d95PpMroUB?key=d3s-vJLBsYtwvRvGfZhdnw)**

Keyword  `defer`  di atas akan mengakhirkan ekseusi  `fmt.Println("halo")`, efeknya pesan  `"halo"`  akan muncul setelah  `"selamat datang"`.

Statement yang di-defer akan tetap muncul meskipun blok kode diberhentikan ditengah jalan menggunakan  `return`. Contohnya seperti pada kode berikut.

```
func main() {
    orderSomeFood("pizza")
    orderSomeFood("burger")
}

func orderSomeFood(menu string) {
    defer fmt.Println("Terimakasih, silakan tunggu")
    if menu == "pizza" {
        fmt.Print("Pilihan tepat!", " ")
        fmt.Print("Pizza ditempat kami paling enak!", "\n")
        return
    }

    fmt.Println("Pesanan anda:", menu)
}
```

Output program:

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe_LTtlEPI8Z32IsN8dW3nz2XEO8QFl40FNT6IWrmuM-1TCazAO8h3dS0VSTkQdLckcO5QQEfQP6HsCTyFVWQmJCAWgEjkWLf7gXR4y1SVCIm4Ly44zl0pgE7y1bi9UyE3sZ4HZu-NK5C7b8lEqvzRQbyE?key=d3s-vJLBsYtwvRvGfZhdnw)**

Info tambahan, ketika ada banyak statement yang di-defer, maka seluruhnya akan dieksekusi di akhir secara berurutan.

## A.36.2. Kombinasi  `defer`  dan IIFE

Penulis ingatkan lagi bahwa eksekusi defer adalah di akhir blok fungsi, bukan blok lainnya seperti blok seleksi kondisi.

```
func main() {
    number := 3

    if number == 3 {
        fmt.Println("halo 1")
        defer fmt.Println("halo 3")
    }

    fmt.Println("halo 2")
}
```

Output program:

```
halo 1
halo 2
halo 3
```

Pada contoh di atas  `halo 3`  akan tetap di print setelah  `halo 2`  meskipun statement defer dipergunakan dalam blok seleksi kondisi  `if`. Hal ini karena defer eksekusinya terjadi pada akhir blok fungsi (dalam contoh di atas  `main()`), bukan pada akhir blok  `if`.

Agar  `halo 3`  bisa dimunculkan di akhir blok  `if`, maka harus dibungkus dengan IIFE. Contoh:

```
func main() {
    number := 3

    if number == 3 {
        fmt.Println("halo 1")
        func() {
            defer fmt.Println("halo 3")
        }()
    }

    fmt.Println("halo 2")
}
```

Output program:

```
halo 1
halo 3
halo 2
```

Bisa dilihat  `halo 3`  muncul sebelum  `halo 2`, karena dalam blok seleksi kondisi  `if`  eksekusi defer terjadi dalam blok fungsi anonymous (IIFE).

## A.36.3. Penerapan Fungsi  `os.Exit()`

Exit digunakan untuk menghentikan program secara paksa pada saat itu juga. Semua statement setelah exit tidak akan dieksekusi, termasuk juga defer.

Fungsi  `os.Exit()`  berada dalam package  `os`. Fungsi ini memiliki sebuah parameter bertipe numerik yang wajib diisi. Angka yang dimasukkan akan muncul sebagai  **exit status**  ketika program berhenti.

```
package main

import "fmt"
import "os"

func main() {
    defer fmt.Println("halo")
    os.Exit(1)
    fmt.Println("selamat datang")
}
```

Meskipun  `defer fmt.Println("halo")`  ditempatkan sebelum  `os.Exit()`, statement tersebut tidak akan dieksekusi, karena di-tengah fungsi program dihentikan secara paksa.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeSZWfcH8hSmfQjggHJ1fzcnnlyV35KDKfhXL_kT2-CtDZKMpUvWnuwnChJtyg1epYJBGSrxnvhggVna7kH9Ff8t6zzZUynEFg5iT2YztKUPc-5xIJSKzik2xzHyyzxEvWgKjXPTIX_3o3JKtBkIHde6XH3?key=d3s-vJLBsYtwvRvGfZhdnw)**