---
sidebar_position: 17
---

# A.17. Map


**Map**  adalah tipe data asosiatif yang ada di Go yang berbentuk  _key-value pair_. Data/value yang disimpan di map selalu disertai dengan key. Key sendiri harus unik, karena digunakan sebagai penanda (atau identifier) untuk pengaksesan value yang disimpan di map.

Kalau dilihat,  `map`  mirip seperti slice, hanya saja identifier yang digunakan untuk pengaksesan bukanlah index numerik, melainkan bisa dalam tipe data apapun sesuai dengan yang diinginkan.

## A.17.1. Penggunaan Map

Cara pengaplikasian map cukup mudah, dengan menuliskan keyword  `map`  diikuti tipe data key dan value-nya. Silakan perhatikan contoh di bawah ini agar lebih jelas.

```
var chicken map[string]int
chicken = map[string]int{}

chicken["januari"] = 50
chicken["februari"] = 40

fmt.Println("januari", chicken["januari"]) // januari 50
fmt.Println("mei",     chicken["mei"])     // mei 0
```

Variabel  `chicken`  dideklarasikan bertipe data map, dengan key ditentukan tipenya adalah  `string`  dan tipe value-nya  `int`. Dari kode tersebut bisa dilihat bagaimana cara penerapan keyword  `map`  untuk pembuatan variabel.

Kode  `map[string]int`  merepresentasikan tipe data  `map`  dengan key bertipe  `string`  dan value bertipe  `int`.

Zero value atau nilai default variabel  `map`  adalah  `nil`. Dari sini maka penting untuk menginisialisasi nilai awal map agar tidak  `nil`. Jika dibiarkan  `nil`, ketika map digunakan untuk menampung data pasti memunculkan error.

Cara untuk inisialisasi map dengan menambahkan kurung kurawal buka tutup di akhir penulisan map, contoh:  `map[string]int{}`.

Cara menambahkan item pada map adalah dengan menuliskan variabel-nya, kemudian diikuti dengan  `key`  pada kurung siku variabel (mirip seperti cara pengaksesan elemen slice), lalu operator  `=`, kemudian nilai/data yang ingin disimpan. Contohnya seperti  `chicken["februari"] = 40`. Sedangkan cara mengakses item map dengan cukup dengan menuliskan nama variabel diikuti kurung siku dan  `key`.

Pengisian data pada map bersifat  **overwrite**, artinya variabel sudah memiliki item dengan key yang sama, maka value item yang lama (dengan key sama) akan ditimpa dengan value baru.


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeZSYrBF6RBSLy0FR_wWMndQK0q1ssu90VGKFXhnGqYK08dFyZFrPUdWI-vCvaKhhlE25Ub1XDoLhyd6PTL-OQR2I9UOEOfRojDp2LXKE60C5vG9sqjgi6N8S62z_sBJgblKIoJkn8Z8Q40QFyXJP3qxDHF?key=d3s-vJLBsYtwvRvGfZhdnw)**

Pengaksesan item menggunakan key yang belum tersimpan di map, menghasilkan data berupa nilai default sesuai tipe data value. Contohnya kode `chicken["mei"]` menghasilkan nilai 0 (nilai default tipe `int`), hal ini karena variabel map `chicken` tidak memiliki item dengan key `"mei"`.

## A.17.2. Inisialisasi Nilai Map

Zero value dari map adalah  `nil`. Disarankan untuk menginisialisasi secara explisit nilai awalnya agar tidak  `nil`.

```
var data map[string]int
data["one"] = 1
// akan muncul error!

data = map[string]int{}
data["one"] = 1
// tidak ada error
```

Nilai variabel bertipe map bisa didefinisikan di awal, caranya dengan menambahkan kurung kurawal setelah tipe data, kemudian menuliskan key dan value di dalam kurung kurawal tersebut. Cara ini sekilas mirip dengan definisi nilai array/slice namun dalam bentuk key-value.
```
// cara horizontal
var chicken1 = map[string]int{"januari": 50, "februari": 40}

// cara vertical
var chicken2 = map[string]int{
    "januari":  50,
    "februari": 40,
}
```

Key dan value dituliskan dengan pembatas tanda titik dua (`:`). Sedangkan tiap itemnya dituliskan dengan pembatas tanda koma (`,`). Khusus deklarasi dengan gaya vertikal, tanda koma perlu dituliskan setelah item terakhir.

Variabel  `map`  bisa di-inisialisasi dengan tanpa nilai awal, caranya menggunakan tanda kurung kurawal, contoh:  `map[string]int{}`. Atau bisa juga dengan menggunakan keyword  `make`  dan  `new`. Contohnya bisa dilihat pada kode berikut. Ketiga cara di bawah ini intinya adalah sama.
```
var chicken3 = map[string]int{}
var chicken4 = make(map[string]int)
var chicken5 = *new(map[string]int)
```
Khusus inisialisasi data menggunakan keyword `new`, yang dihasilkan adalah data pointer. Untuk mengambil nilai aslinya bisa dengan menggunakan tanda asterisk (`*`). Topik pointer nantinya dibahas lebih detail pada chapter A.23. Pointer.

## A.17.3. Iterasi Item Map Menggunakan  `for`  -  `range`

Item variabel  `map`  bisa di iterasi menggunakan  `for`  -  `range`. Cara penerapannya masih sama seperti pada slice, dengan perbedaan pada map data yang dikembalikan di tiap perulangan adalah key dan value (bukan indeks dan elemen). Contohnya bisa dilihat pada kode berikut.

```
var chicken = map[string]int{
    "januari":  50,
    "februari": 40,
    "maret":    34,
    "april":    67,
}

for key, val := range chicken {
    fmt.Println(key, "  \t:", val)
}
```
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfUiFU6BZL_3CpYatv-GPQ70LUFllkXanSuoi1RDbDi4ri08A0_g0dqWCbimBNntrjyiFBvzvcAgHXvR1omuagzwDrW6uGT3elD0K1xRL0ZRHwt1F4jDajGFEHwgpE3W1OCCuWOz7Yn6CNwKRvxgEjNAnc?key=d3s-vJLBsYtwvRvGfZhdnw)**

## A.17.4. Menghapus Item Map

Fungsi  `delete()`  digunakan untuk menghapus item dengan key tertentu pada variabel map. Cara penggunaannya, dengan memasukan objek map dan key item yang ingin dihapus sebagai argument pemanggilan fungsi  `delete()`.

```
var chicken = map[string]int{"januari": 50, "februari": 40}

fmt.Println(len(chicken)) // 2
fmt.Println(chicken)

delete(chicken, "januari")

fmt.Println(len(chicken)) // 1
fmt.Println(chicken)
```

Operasi di atas membuat item dengan key  `"januari"`  dalam variabel map  `chicken`  dihapus.


**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd8m4J2QFWVjILYgyxRXQzfnV0buZQVix1bX9M8psBttAdnhPZc9OPwz7Onqw4xPRllq3SQ0Cl9jJRdlQ45Rv2GirnC11dXZsLWqTE0WD5dP-N8r-A7Vic042zUjKYq7Bujky-bxo4e7PCJb0C3xjxa9yA?key=d3s-vJLBsYtwvRvGfZhdnw)**


Penggunaan fungsi `len()` pada map mengembalikan informasi jumlah item.

## A.17.5. Deteksi Keberadaan Item Dengan Key Tertentu

Ada cara untuk mengetahui apakah dalam variabel map terdapat item dengan key tertentu atau tidak, yaitu dengan memanfaatkan 2 variabel sebagai penampung nilai kembalian pengaksesan item. Return value ke-2 sifatnya opsional, boleh ditulis boleh juga tidak. Isinya nilai  `bool`, jika berisi  `true`  menandakan bahwa item yang dicari ada di map, jika  `false`  maka tidak ada.

```
var chicken = map[string]int{"januari": 50, "februari": 40}
var value, isExist = chicken["mei"]

if isExist {
    fmt.Println(value)
} else {
    fmt.Println("item is not exists")
}
```

## A.17.6. Kombinasi Slice & Map

Slice dan  `map`  bisa dikombinasikan, dan pada praktiknya cukup sering digunakan, contohnya untuk keperluan penyimpanan data array yang berisikan informasi siswa, dan banyak lainnya.

Cara penerapannya cukup mudah, contohnya  `[]map[string]int`, tipe tersebut artinya adalah sebuah slice yang tipe setiap elemen-nya adalah  `map[string]int`. Agar lebih jelas, silakan praktekan contoh berikut.

```
var chickens = []map[string]string{
    map[string]string{"name": "chicken blue",   "gender": "male"},
    map[string]string{"name": "chicken red",    "gender": "male"},
    map[string]string{"name": "chicken yellow", "gender": "female"},
}

for _, chicken := range chickens {
    fmt.Println(chicken["gender"], chicken["name"])
}
```
Variabel  `chickens`  di atas berisikan 3 buah item bertipe  `map[string]string`. Ketiga item tersebut dideklarasikan memiliki 2 key yang sama, yaitu  `name`  dan  `gender`.

Penulisan tipe data tiap item adalah opsional. Boleh ditulis atau tidak. Contoh alternatif penulisan:

```
var chickens = []map[string]string{
    {"name": "chicken blue",   "gender": "male"},
    {"name": "chicken red",    "gender": "male"},
    {"name": "chicken yellow", "gender": "female"},
}
```

Dalam  `[]map[string]string`, tiap elemen bisa saja memiliki key yang berbeda-beda, contohnya seperti kode berikut.

```
var data = []map[string]string{
    {"name": "chicken blue", "gender": "male", "color": "brown"},
    {"address": "mangga street", "id": "k001"},
    {"community": "chicken lovers"},
}
```