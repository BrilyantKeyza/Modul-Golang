---
sidebar_position: 54
---

# A.54. Web Service API Server


Pada chapter ini kita akan mencoba mengkombinasikan hasl pembelajaran di 2 chapter sebelumnya (yaitu web programming dan JSON), untuk membuat sebuah web service API yang memilikki endpoint dengan reponse data mengadopsi format JSON.

> Web Service API adalah sebuah web yang menerima request dari client dan menghasilkan response, biasa berupa JSON/XML atau format lainnya.

## A.54.1. Pembuatan Web API

Pertama siapkan terlebih dahulu struct dan beberapa data sample.

```
package main

import "encoding/json"
import "net/http"
import "fmt"

type student struct {
    ID    string
    Name  string
    Grade int
}

var data = []student{
    student{"E001", "ethan", 21},
    student{"W001", "wick", 22},
    student{"B001", "bourne", 23},
    student{"B002", "bond", 23},
}
```

Struct  `student`  di atas digunakan sebagai tipe elemen slice sample data, ditampung variabel  `data`.

Selanjutnya buat fungsi  `users()`  untuk handle endpoint  `/users`. Di dalam fungsi tersebut ada proses deteksi jenis request lewat property  `r.Method()`, untuk mencari tahu apakah jenis request adalah  **POST**  atau  **GET**  atau lainnya.
```
func users(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "application/json")

    if r.Method == "GET" {
        var result, err = json.Marshal(data)

        if err != nil {
            http.Error(w, err.Error(), http.StatusInternalServerError)
            return
        }

        w.Write(result)
        return
    }

    http.Error(w, "", http.StatusBadRequest)
}
```

Jika request adalah GET (mengambil data), maka data yang di-encode ke JSON dijadikan sebagai response.

Statement  `w.Header().Set("Content-Type", "application/json")`  digunakan untuk menentukan tipe response, yaitu sebagai JSON. Sedangkan  `r.Write()`  digunakan untuk mendaftarkan data sebagai response.

Selebihnya, jika request tidak valid, response di set sebagai error menggunakan fungsi  `http.Error()`.

Siapkan juga handler untuk endpoint  `/user`. Perbedaan endpoint ini dengan  `/users`  di atas adalah:

-   Endpoint  `/users`  mengembalikan semua sample data yang ada (array).
-   Endpoint  `/user`  mengembalikan satu buah data saja, diambel dari data sample berdasarkan  `ID`-nya. Pada endpoint ini, client harus mengirimkan juga informasi  `ID`  data yang dicari.

```
func user(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "application/json")

    if r.Method == "GET" {
        var id = r.FormValue("id")
        var result []byte
        var err error

        for _, each := range data {
            if each.ID == id {
                result, err = json.Marshal(each)

                if err != nil {
                    http.Error(w, err.Error(), http.StatusInternalServerError)
                    return
                }

                w.Write(result)
                return
            }
        }

        http.Error(w, "User not found", http.StatusNotFound)
        return
    }

    http.Error(w, "", http.StatusBadRequest)
}
```
Method  `r.FormValue()`  digunakan untuk mengambil data form yang dikirim dari client, pada konteks ini data yang dimaksud adalah  `ID`.

Dengan menggunakan  `ID`  tersebut dicarilah data yang relevan. Jika ada, maka dikembalikan sebagai response. Jika tidak ada maka error  **400, Bad Request**  dikembalikan dengan pesan  **User Not Found**.

Terakhir, implementasikan kedua handler di atas.

```
func main() {
    http.HandleFunc("/users", users)
    http.HandleFunc("/user", user)

    fmt.Println("starting web server at http://localhost:8080/")
    http.ListenAndServe(":8080", nil)
}
```

Jalankan program, sekarang web server sudah live dan bisa dikonsumsi datanya.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfwbBLh8Mzoq9JUeEsqe8gYYzJd_OCs9BCazzUuCc7kGRZd0q4GGGPC6Su5GIk_STgG0LfYXnQd8gtvrTXeH7s2xpXUCK5rYr9I4I1fpWKQBqZdKUW36FhVprkHSJY1g3KEcJVvU4BIm_nAtoYv55_9f-U?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.54.2. Test Web Service API via Postman

Setelah web server sudah berjalan, web service yang telah dibuat perlu untuk di-tes. Di sini saya menggunakan Google Chrome plugin bernama  [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en)  untuk mengetes API yang sudah dibuat.

-   Test endpoint  `/users`, apakah data yang dikembalikan sudah benar.

	**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeIs0aYgV11o_P4nGrbev0-fkSVcDBey6JuZ6-Yi8WPwcytiQ8bBk71hYHIWyc-txvdPc4ZlzpWYAIqX2ahtxmNGjuRhdmeb9G0p0X1vv0uWTpL6mmH8tQIFma64mxEsxpUWTjstJxdGLzlk3eq9Tk0Zow9?key=d3s-vJLBsYtwvRvGfZhdnw)**
- Test endpoint `/user`, isi form data `id` dengan nilai `E001`.

	**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeHDlCusm7OBQBlZF9yql2hULiqNgTRFW3xdKMs7o2wQ_1UCXTOQ6O4vgzVPS8yWOZNFRLmRsROA3GZmPfNwMPwb7IM7tDTb9Xs-8QxdqE8dYlSzh3drd8do1P5YWcM8dCtCg_abPVIe2HfSoDeCZEm3flG?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.54.3. Test Web Service API via  `cURL`

Testing bisa juga dilakukan via cURL. Pastikan untuk menginstall cURL terlebih dahulu agar bisa menggunakan command berikut.

```
curl -X GET http://localhost:8080/users
curl -X GET http://localhost:8080/user?id=B002
```

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcMUXYH5S-YqHcMDSbX9N4w8FyBlYj8DewghII6e3T1-t_eCtwVne9i8OmRIcX0P0P9I00i5jj4jdkEY0lN69m6vS2CScTg2XcsaAHMxyBZ-vrtUm4Vk5ycqZkE599LEc-AgFwpXf7YH6R08UFWPttOWeKZ?key=d3s-vJLBsYtwvRvGfZhdnw)**

Data user ID pada endpoint `/user` ditulis dalam format query parameters, yaitu `?id=B002`. 