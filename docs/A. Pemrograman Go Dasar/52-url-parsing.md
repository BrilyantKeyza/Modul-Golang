---
sidebar_position: 52
---

# A.52. URL Parsing


Data string berisi informasi URL bisa dikonversi ke tipe data  `url.URL`. Dengan menggunakan tipe  `url.URL`, akan ada banyak informasi yang bisa kita dapatkan dengan mudah, di antaranya seperti jenis protokol yang digunakan, path yang diakses, query, dan lainnya.

Berikut adalah contoh sederhana konversi string ke  `url.URL`.
```
package main

import "fmt"
import "net/url"

func main() {
    var urlString = "http://kalipare.com:80/hello?name=john wick&age=27"
    var u, e = url.Parse(urlString)
    if e != nil {
        fmt.Println(e.Error())
        return
    }

    fmt.Printf("url: %s\n", urlString)

    fmt.Printf("protocol: %s\n", u.Scheme) // http
    fmt.Printf("host: %s\n", u.Host)       // kalipare.com:80
    fmt.Printf("path: %s\n", u.Path)       // /hello

    var name = u.Query()["name"][0] // john wick
    var age = u.Query()["age"][0]   // 27
    fmt.Printf("name: %s, age: %s\n", name, age)
}
```
Fungsi  `url.Parse()`  digunakan untuk parsing string ke bentuk url. Fungsi ini mengembalikan 2 data, variabel objek bertipe  `url.URL`  dan error (jika ada). Lewat variabel objek tersebut pengaksesan informasi url akan menjadi lebih mudah, contohnya seperti nama host bisa didapatkan lewat  `u.Host`, protokol lewat  `u.Scheme`, dan lainnya.

Selain itu, query yang ada pada url akan otomatis diparsing juga, menjadi bentuk  `map[string][]string`, dengan key adalah nama elemen query, dan value array string yang berisikan value elemen query.

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfgpHDHcqZ_qrU5oTbTFjW2x-kHliPzmHuwHw3s7xy7Xb8xEfNlPgx3wjLInsia_gmffumlvgQHW19j-gh9fRaRiK0LZkZskzDVYgIkmPsPCP6HVYv3PjyvWM926np8uvALLvGPAnN9yFhkR4ypTcHw0-GN?key=d3s-vJLBsYtwvRvGfZhdnw)**