---
sidebar_position: 12
---

# A.12. Operator


Chapter ini membahas mengenai macam operator yang bisa digunakan di Go. Secara umum terdapat 3 kategori operator: aritmatika, perbandingan, dan logika.

## A.12.1. Operator Aritmatika

Operator aritmatika adalah operator yang digunakan untuk operasi yang sifatnya perhitungan. Go mendukung beberapa operator aritmatika standar, list-nya bisa dilihat di tabel berikut.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfwJhwHBBc_8OCrcFnuTL6b-pJj7suENUuSWnCUA1SwkuXqJBIQ_IErf0Ai2ocXz3mVEadfhGcNv7rDoFA77weNTC2KTa6qEffNfcISP1exe08q7v7YNzfcIrxFRH0IpDVkzl5yBksSJ_gqGH5qB-dSmy4?key=d3s-vJLBsYtwvRvGfZhdnw)**
Contoh penggunaan:

```
var value = (((2 + 6) % 3) * 4 - 2) / 3
```

## A.12.2. Operator Perbandingan

Operator perbandingan digunakan untuk menentukan kebenaran suatu kondisi. Hasilnya berupa nilai boolean,  `true`  atau  `false`.

Tabel di bawah ini berisikan operator perbandingan yang bisa digunakan di Go.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdcFd-QBU2DzpqETrJtgngyI_EjJXTbXx1dyWGg791fSPhRcV4KUuzceYWwesWVSSGUtgnMWnmjSmBlVGlbPDSdekOR9NrYKFuPY0Z0dTsouyFl_YY8QM7-_SPytv9yM05KAdKpoQ2YRedk_wOqPccaGLkQ?key=d3s-vJLBsYtwvRvGfZhdnw)**
Contoh penggunaan:

```
var value = (((2 + 6) % 3) * 4 - 2) / 3
var isEqual = (value == 2)

fmt.Printf("nilai %d (%t) \n", value, isEqual)
```

Pada kode di atas, terdapat statement operasi aritmatika yang hasilnya ditampung oleh variabel  `value`. Selanjutnya, variabel tersebut dibandingkan dengan angka  **2**  untuk dicek apakah nilainya sama. Jika iya, maka hasilnya adalah  `true`, jika tidak maka  `false`. Nilai hasil operasi perbandingan tersebut kemudian disimpan dalam variabel  `isEqual`.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcBgfLXCBYb1fF6FwL4LRWzCNNjZUa4rfLKyLybAmKUmZTJNdgbmQxLAOVIvhp2T-7kxFR5QD6Z6tQeBCJEq_Xyh2kS4glNuFzii373da0AHecA7AJGmyHuZ7QvYYUCFxTB-GAQTpk3TaUVkXWEi4YvY233?key=d3s-vJLBsYtwvRvGfZhdnw)**
Untuk memunculkan nilai `bool` menggunakan `fmt.Printf()`, bisa gunakan layout format `%t`.

## A.12.3. Operator Logika

Operator ini digunakan untuk mencari benar tidaknya kombinasi data bertipe  `bool`  (bisa berupa variabel bertipe  `bool`, atau hasil dari operator perbandingan).

Beberapa operator logika standar yang bisa digunakan:
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfh4K_GzZQrXOhwDg6cbUMxUJfKSTWdcI_cQkYJujktncV9MNrfBWxesphYI7Fsm72S_hu277augkqWQWIcef3f9i5cuMMAfvuTHdby2Ne-IRyWqNEhxSGaCH8jrOpuOcs4Ia1sm2SNl5dZarOcraOLEKw?key=d3s-vJLBsYtwvRvGfZhdnw)**
Contoh penggunaan:

```
var left = false
var right = true

var leftAndRight = left && right
fmt.Printf("left && right \t(%t) \n", leftAndRight)

var leftOrRight = left || right
fmt.Printf("left || right \t(%t) \n", leftOrRight)

var leftReverse = !left
fmt.Printf("!left \t\t(%t) \n", leftReverse)
```

Hasil dari operator logika sama dengan hasil dari operator perbandingan, yaitu berupa boolean.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcRtqDYKu8p2Ah3ycPD2TBIwo_7_Xzd9GhmTnbpTk4kY9xmTPIoML-Ig5AYMTsIoMf66zGjRfe37XFx-D_FoKjB3XMevjaAoU49PW3ZKzeT1IyFoZ8mpRpbZIkna9u09sE2FCj4mIEYM5lK-NjmxPZVjs7l?key=d3s-vJLBsYtwvRvGfZhdnw)**
Berikut penjelasan statemen operator logika pada kode di atas.

-   `leftAndRight`  bernilai  `false`, karena hasil dari  `false`  **dan**  `true`  adalah  `false`.
-   `leftOrRight`  bernilai  `true`, karena hasil dari  `false`  **atau**  `true`  adalah  `true`.
-   `leftReverse`  bernilai  `true`, karena  **negasi**  (atau lawan dari)  `false`  adalah  `true`.

Template  `\t`  digunakan untuk menambahkan indent tabulasi. Biasa dimanfaatkan untuk merapikan tampilan output pada console.