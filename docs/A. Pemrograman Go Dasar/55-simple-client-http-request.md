---
sidebar_position: 55
---

# A.55. Simple Client HTTP Request


Pada chapter sebelumnya telah dibahas bagaimana cara membuat Web Service API yang response data-nya berbentuk JSON. Pada chapter ini kita akan belajar mengenai cara untuk mengkonsumsi data tersebut.

Pastikan anda sudah mempraktekkan apa-apa yang ada pada chapter sebelumnya (A.54. Web Service API Server), karena web service yang telah dibuat di situ juga dipergunakan pada chapter ini.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfR0ltueiGHjrX54wy_lq-dHB27wcFvxhGmcVY8E_KAFz3LcOlC53gzz1hQ1Po8iE8ePPNCBQ4xf5-CWgGdGFSYaKHYfhyYkG8MKiEoFT7n99O5hvxhJbY2PK4VyqQrUNypx6FAMCUnikxO1PRN7ibtDQg?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.55.1. Penggunaan HTTP Request

Package  `net/http`, selain berisikan tools untuk keperluan pembuatan web, juga berisikan fungsi-fungsi untuk melakukan http request. Salah satunya adalah  `http.NewRequest()`  yang akan kita bahas di sini. Untuk menggunakannya pastikan import package-nya terlebih dahulu.

Kemudian siapkan struct  `student`  yang nantinya akan dipakai sebagai tipe data reponse dari web API. Struk tersebut skema nya sama dengan yang ada pada chapter ([A.54. Web Service API Server](https://dasarpemrogramangolang.novalagung.com/A-web-service-api.html)).

```
package main

import "fmt"
import "net/http"
import "encoding/json"

var baseURL = "http://localhost:8080"

type student struct {
    ID    string
    Name  string
    Grade int
}
```

Setelah itu buat fungsi  `fetchUsers()`. Fungsi ini bertugas melakukan request ke  [http://localhost:8080/users](http://localhost:8080/users), menerima response dari request tersebut, lalu menampilkannya.
```
func fetchUsers() ([]student, error) {
    var err error
    var client = &http.Client{}
    var data []student

    request, err := http.NewRequest("GET", baseURL+"/users", nil)
    if err != nil {
        return nil, err
    }

    response, err := client.Do(request)
    if err != nil {
        return nil, err
    }
    defer response.Body.Close()

    err = json.NewDecoder(response.Body).Decode(&data)
    if err != nil {
        return nil, err
    }

    return data,nil
}
```
Statement  `&http.Client{}`  menghasilkan instance  `http.Client`. Objek ini nantinya diperlukan untuk eksekusi request.

Fungsi  `http.NewRequest()`  digunakan untuk membuat request baru. Fungsi tersebut memiliki 3 parameter yang wajib diisi.

1.  Parameter pertama, berisikan tipe request  **POST**  atau  **GET**  atau lainnya
2.  Parameter kedua, adalah URL tujuan request
3.  Parameter ketiga, form data request (jika ada)

Fungsi tersebut menghasilkan instance bertipe  `http.Request`  yang nantinya digunakan saat eksekusi request.

Cara eksekusi request sendiri adalah dengan memanggil method  `Do()`  pada variabel  `client`  yang sudah dibuat. Fungsi  `Do()`  dipanggil dengan disisipkan argument fungsi yaitu object  `request`. Penulisannya:  `client.Do(request)`.

Method tersebut mengembalikan instance bertipe  `http.Response`  yang di contoh ditampung oleh variabel  `response`. Dari data response tersebut kita bisa mengakses informasi yang berhubungan dengan HTTP response, termasuk response body.

Data response body tersedia via property  `Body`  dalam tipe  `[]byte`. Gunakan JSON Decoder untuk mengkonversinya menjadi bentuk JSON. Contohnya bisa dilihat di kode di atas,  `json.NewDecoder(response.Body).Decode(&data)`.

Perlu diketahui, data response perlu di-**close**  setelah tidak dipakai. Caranya dengan memanggil method  `Close()`  milik property  `Body`  yang dalam penerapannya umumnya di-defer. Contohnya:  `defer response.Body.Close()`.

Selanjutnya, eksekusi fungsi  `fetchUsers()`  dalam fungsi  `main()`.

```
func main() {
    var users, err = fetchUsers()
    if err != nil {
        fmt.Println("Error!", err.Error())
        return
    }

    for _, each := range users {
        fmt.Printf("ID: %s\t Name: %s\t Grade: %d\n", each.ID, each.Name, each.Grade)
    }
}
```

Ok, terakhir sebelum memulai testing, pastikan telah run aplikasi pada chapter sebelumya (A.54. Web Service API Server). Setelah itu start prompt cmd/terminal baru dan jalankan program yang telah dibuat di chapter ini.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdRKIP8A1k5l7Euf8-kQ2bfS4SoLx45c63AZyYB1Kr7BQqAFVHEuf5ur0w_9YvoyG4o_eS3jns3I7Uk48Wg7NEBxUwsYVe8PSaqKvJoIyHnXvL_jhK0TgNRUVBwMjtTAgC_IQ23hp32Gb-WTUv85Ejd4eHw?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.55.2. HTTP Request Dengan Form Data

Untuk menyisipkan data pada sebuah request, ada beberapa hal yang perlu ditambahkan. Pertama, import package  `bytes`  dan  `net/url`.

```
import "bytes"
import "net/url"
```

Kemudian buat fungsi baru, isinya request ke  [http://localhost:8080/user](http://localhost:8080/user)  dengan data yang disisipkan adalah  `ID`.
```
func fetchUser(ID string) (student, error) {
    var err error
    var client = &http.Client{}
    var data student

    var param = url.Values{}
    param.Set("id", ID)
    var payload = bytes.NewBufferString(param.Encode())

    request, err := http.NewRequest("POST", baseURL+"/user", payload)
    if err != nil {
        return data, err
    }
    request.Header.Set("Content-Type", "application/x-www-form-urlencoded")

    response, err := client.Do(request)
    if err != nil {
        return data, err
    }
    defer response.Body.Close()

    err = json.NewDecoder(response.Body).Decode(&data)
    if err != nil {
        return data, err
    }

    return data, nil
}
```
Isi fungsi  `fetchUser()`  memiliki beberapa kemiripan dengan fungsi  `fetchUsers()`  sebelumnya.

Statement  `url.Values{}`  akan menghasilkan objek yang nantinya digunakan sebagai form data request. Pada objek tersebut perlu di set data apa saja yang ingin dikirimkan menggunakan fungsi  `Set()`  seperti pada  `param.Set("id", ID)`.

Statement  `bytes.NewBufferString(param.Encode())`  melakukan proses encoding pada data param untuk kemudian diubah menjadi bentuk  `bytes.Buffer`. Nantinya data buffer tersebut disisipkan pada parameter ketiga pemanggilan fungsi  `http.NewRequest()`.

Karena data yang akan dikirim adalah  _encoded_, maka pada header perlu dituliskan juga tipe encoding-nya. Kode  `request.Header.Set("Content-Type", "application/x-www-form-urlencoded")`  menandai bahwa HTTP request berisi body yang ter-encode sesuai spesifikasi  `application/x-www-form-urlencoded`.

> Pada konteks HTML, HTTP Request yang di trigger dari tag  `<form></form>`  secara default tipe konten-nya sudah di set  `application/x-www-form-urlencoded`. Lebih detailnya bisa merujuk ke spesifikasi HTML form  [http://www.w3.org/TR/html401/interact/forms.html#h-17.13.4.1](http://www.w3.org/TR/html401/interact/forms.html#h-17.13.4.1)

Response dari endpoint  `/user`  bukanlah slice, tetapi berupa objek. Maka pada saat decode perlu pastikan tipe variabel penampung hasil decode data response adalah  `student`  (bukan  `[]student`).

Lanjut ke perkodingan, terakhir, implementasikan  `fetchUser()`  pada fungsi  `main()`.

```
func main() {
    var user1, err = fetchUser("E001")
    if err != nil {
        fmt.Println("Error!", err.Error())
        return
    }

    fmt.Printf("ID: %s\t Name: %s\t Grade: %d\n", user1.ID, user1.Name, user1.Grade)
}
```
Untuk keperluan testing, kita hardcode `ID` nilainya `"E001"`. Jalankan program untuk test apakah data yang dikembalikan sesuai.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcUdlwTVn7DQvJg6qxMnlhCC3nr9R0I1H164-Ng89xzu-TbyHottekWIda9hwdCjHEuwxdbAo4GEQdPwRvUMTaj53sUB586hx7nCRU_fflRKiVMzX3QcjX0Ohu5h1t5ihb3oH0AR6FdMWCKh7Rt8fjMgOY?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.55.3. Secure & Insecure HTTP Request

Sampai sini kita telah belajar bagaimana cara membuat http request sederhana untuk kirim data dan juga ambil data. Nantinya pada chapter  [C.27. Secure & Insecure Client HTTP Request](https://dasarpemrogramangolang.novalagung.com/C-secure-insecure-client-http-request.html)  pembelajaran topik HTTP request dilanjutkan kembali, kita akan bahas tentang aspek keamanan/security suatu HTTP request.