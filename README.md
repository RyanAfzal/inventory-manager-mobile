# Tugas 7 PBP

# Perbedaan stateless widget dan stateful widget

Stateless widget adalah widget statis dimana seluruh konfigurasi yang dimuat didalamnya telah diinisiasi sejak awal, statless widget tidak bisa diubah state nya saat aplikasi sedang berjalan, hanya memiliki properti final, seperti namanya widget ini tidak memiliki state, dan widget ini masih bisa diubah dengan mengubah events eksternal pada parent widget di widget tree.
Contoh : Text, Icon, RaisedButton.

Sedangkan Stateful widget berlaku sebaliknya dimana sifatnya adalah dinamis, sehingga widget ini dapat diperbaharui kapanpun dibutuhkan termasuk saat aplikasi sedang berjalan berdasarkan user actions atau ketika terjadinya perubahan data dan widget ini memiliki state internal.
Contoh : Checkbox, Radio Button, Slider

# Widget yang digunakan untuk tugas ini
| Nama Widget | Fungsi |
| --- | --- |
|MyHomePage|untuk mengatur tampilan halama home aplikasi|
|ShopCard|untuk menampilkan tombol lihat produk, tambah produk, dan logout|
|Scaffold|untuk struktur tata letak visual Desain Material dasar, termasuk drawers, snack bars, AppBar, and bottom sheets|
|AppBar|untuk menampilkan konten dan action pada bagian paling atas layar|
|SingleChildScrollView| Untuk membuat area konten yang dapat di scroll jika konten melebihi ukuran layar|
|Padding|untuk memberi jarak di sekitar widget child|
|Column|Membuat tata letak daftar widget child dalam arah vertikal|
|Text|untuk menampilkan teks dengan 1 style|
|GridView.count|Untuk membuat tata letak grid dengan jumlah kolom yang tetap|
|Material|Untuk mengatur bahan dasar card dengan warna latar belakang yang sesuai|
|InkWell|Untuk membuat area responsif terhadap sentuhan (*tap*)|
|Container|untuk mengatur posisi, painting, dan ukuran, serta pada tugas ini untuk menyimpan|
|Icon|untuk desain material icon|
|SnackBar|untuk pesan singkat tentang proses aplikasi yang ditampilkan di bagian bawah layar|
|ColorScheme|Untuk mengatur palet warna dalam aplikasi|

# Cara mengimplementasi checklist step-by-step
1. Install flutter
2. Buat direktori untuk app saya buat nama direktori inventory_manager_mobile
3. Create direktori proyek dengan nama inventory_manager
4. Lalu run dan enable web support dengan ```flutter config --enable-web```
5. Hubungkan direktori dengan git dan lakukan git add,commit,push
6. Buat file baru bernama menu.dart pada inventory_manager/lib dan ```import 'package:flutter/material.dart';```
7. Isi menu.dart dengan kode yang dipindahkan dari main.dart dari baris ke 39 hingga akhir
8. Pada main.dart tambahkan ```import 'package:inventory_manager/menu.dart';```
9. Ubah warna tema aplikasi dengan mengubah kode di main.dart pada class MyApp di bagian colorScheme
10. Hapus const dan parameter MyHomePage()
11. Membuat widget sederhana dan mengubah dari stateful menjadi stateless 
```
class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Scaffold(
        appBar: AppBar(
          title: const Text(
            'Inventory Manager',
            style: TextStyle(
              color: Colors.white,
            ),
          ),
          backgroundColor: Colors.indigo,
        ),
        body: SingleChildScrollView(
          // Widget wrapper yang dapat discroll
          child: Padding(
            padding: const EdgeInsets.all(10.0), // Set padding dari halaman
            child: Column(
              // Widget untuk menampilkan children secara vertikal
              children: <Widget>[
                const Padding(
                  padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                  // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                  child: Text(
                    'Whole Mart', // Text yang menandakan toko
                    textAlign: TextAlign.center,
                    style: TextStyle(
                      fontSize: 30,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                ),
                // Grid layout
                GridView.count(
                  // Container pada card kita.
                  primary: true,
                  padding: const EdgeInsets.all(20),
                  crossAxisSpacing: 10,
                  mainAxisSpacing: 10,
                  crossAxisCount: 3,
                  shrinkWrap: true,
                  children: items.map((ShopItem item) {
                    // Iterasi untuk setiap item
                    return ShopCard(item);
                  }).toList(),
                ),
              ],
            ),
          ),
        ),
      );
    }
}
```
12. Lalu saya menambahkan barang-barang dijual dan define pada tipe list
```
class ShopItem {
  final String name;
  final IconData icon;

  ShopItem(this.name, this.icon);
}
```

13. Lalu dibawah kode MyHomePage({Key? key}) : super(key: key); saya menambahkan kode 
```
final List<ShopItem> items = [
    ShopItem("Lihat Produk", Icons.checklist),
    ShopItem("Tambah Produk", Icons.add_shopping_cart),
    ShopItem("Logout", Icons.logout),
];
```

14. Untuk handle error menambahkan widget stateless untuk menampilkan card
```
class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: Colors.indigo,
      child: InkWell(
        // Area responsive terhadap sentuhan
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
        },
        child: Container(
          // Container untuk menyimpan Icon dan Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

15. Untuk bonus pada class tambahkan field color ShopItem dan pada List<ShopItem> setiap items nya tambahkan argumen untuk warna nya
16. Pada class ShopCard, di widget bagian Material ubah color menjadi ```color: item.color,```
<br>
https://github.com/RyanAfzal/inventory-manager-mobile/assets/137851158/d85dc4fd-fed2-40e4-9ba9-def39af53471

# Tugas 8 PBP

# Perbedaan antara Navigator.push() dan Navigator.pushReplacement()
Navigaotr.push() akan menambahkan route baru diatas route yang sudah ada pada atas stack, sedangkan Navigator.pushReplacement() menggantikan route yang sudah ada pada atas stack dengan route baru tersebut. Sehingga dengan push bisa kembali ke route sebelumnya dengan Navigator.pop, sedangkan dengan Navigator.pushReplacement route lama pada atas stack akan digantikan secara langsung oleh route baru yang diberikan tanpa mengubah kondisi elemen stack yang berada di bawahnya. Contoh Navigator push : untuk pergantian halaman misalnya pada tugas ini adalah dari home pindah ke halaman tambah produk. Contoh Navigator pushReplacement : login, setelah pengguna berhasil login, halaman login akan digantikan dengan halaman home dan mencegah pengguna untuk kembali ke halaman login dengan tombol back.

# Layout widget di flutter dan kegunaannya
1. Single child widget seperti namanya widget ini hanya dapat memiliki 1 child widget yang memiliki fungsi spesial untuk membuat tampilan lebih menarik. Contohnya:
- container : untuk mengatur posisi, warna, dan ukuran widget di dalamnya (sebagai wadah widget). Container Widget merupakan “Single Child Widget” yang berarti hanya dapat memiliki satu buah child widget saja. Akan tetapi dalam sebuah container kita dapat menempatkan row, column, text atau bahkan container lain.
- align : untuk mengatur posisi atau align child di dalamnya
- Padding: Memberikan jarak dari dalam widget menuju widget lainnya
- dan lain-lain

2. Multiple child widget adalah widget yang dapat memiliki lebih dari satu child widget dan layout dari widget ini unik.Contohnya :
- Column : untuk mengatur child widget secara vertikal
- Row : untuk mengatur child widget secara horizontal
- ListView : untuk mengatur child widget linear yang dapat di scroll
- Stack: Menempatkan widget di atas satu sama lain (bertumpuk)
- dan lain-lain

3. Silver widget adalah widget yang digunakan untuk membuat widget yang dapat di scroll.Contohnya:
- CupertinoSliverNavigationBar
- CustomScrollView
- SliverAppBar
- dan lain-lain

# Elemen input pada form pada tugas ini dan alasan penggunaan
1. Hanya 1 yaitu TextFormField, elemen input dipilih karena fungsinya yang digunakan untuk memasukkan data dan data yang dimasukkan dapat divalidasi sesuai format yang diinginkan dan di integrasi dengan `Form`.

# Penerapan clean architecture pada Flutter
Clean architecture adalah salah satu cara untuk membuat aplikasi Flutter yang bersih, rapi, mudah dipelihara, dan dapat diuji. Contoh penerapan pada tugas ini adalah dengan mengelompokkan file berdasarkan fungsinya yaitu screens untuk tampilan layar yang berisi menu.dart dan shoplist_form.dart dan widgets untuk widget-widget yang digunakan yaitu left_drawer.dart dan shop_card.dart serta dengan refactoring.

# Cara mengimplementasi checklist step-by-step
1. Membuat halaman baru untuk tambah item baru dengan membuat file baru shoplist_form.dart di dalam direktori screen di direktori lib. Dengan tiga elemen input, yaitu name, amount, description, tombol save, dan validasi tidak boleh kosong dan sesuai dengan tipe nya jika angka harus angka dengan if dan snackbar. Berikut untuk implementasi kodenya

```
import 'package:flutter/material.dart';
// TODO: Impor drawer yang sudah dibuat sebelumnya
import 'package:inventory_manager/widgets/left_drawer.dart';

class ShopFormPage extends StatefulWidget {
    const ShopFormPage({super.key});

    @override
    State<ShopFormPage> createState() => _ShopFormPageState();
}

class _ShopFormPageState extends State<ShopFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _amount = 0;
  String _description = "";

    @override
    Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: const Center(
              child: Text(
                'Form Tambah Produk',
              ),
            ),
            backgroundColor: Colors.indigo,
            foregroundColor: Colors.white,
          ),
          // TODO: Tambahkan drawer yang sudah dibuat di sini
          body: Form(
            key: _formKey,
            child: SingleChildScrollView(
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Nama Produk",
                        labelText: "Nama Produk",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      onChanged: (String? value) {
                        setState(() {
                          _name = value!;
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          ScaffoldMessenger.of(context)
                          ..hideCurrentSnackBar()
                          ..showSnackBar(SnackBar(
                          content: Text("Nama tidak boleh kosong!")));
                          return "Nama tidak boleh kosong!";
                        }
                        return null;
                      },
                    ),
                  ),
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Jumlah",
                        labelText: "Jumlah",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      // TODO: Tambahkan variabel yang sesuai
                      onChanged: (String? value) {
                        setState(() {
                          _amount = int.parse(value!);
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          ScaffoldMessenger.of(context)
                          ..hideCurrentSnackBar()
                          ..showSnackBar(SnackBar(
                          content: Text("Jumlah tidak boleh kosong!")));
                          return "Jumlah tidak boleh kosong!";
                        }
                        if (int.tryParse(value) == null) {
                          ScaffoldMessenger.of(context)
                          ..hideCurrentSnackBar()
                          ..showSnackBar(SnackBar(
                          content: Text("Jumlah harus berupa angka!")));
                          return "Jumlah harus berupa angka!";
                        }
                        return null;
                      },
                    ),
                  ),
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Deskripsi",
                        labelText: "Deskripsi",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      onChanged: (String? value) {
                        setState(() {
                          // TODO: Tambahkan variabel yang sesuai
                          _description = value!;
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          ScaffoldMessenger.of(context)
                          ..hideCurrentSnackBar()
                          ..showSnackBar(SnackBar(
                          content: Text("Deskripsi tidak boleh kosong!")));
                          return "Deskripsi tidak boleh kosong!";
                        }
                        return null;
                      },
                    ),
                  ),

                  //untuk pop up
                  Align(
                    alignment: Alignment.bottomCenter,
                    child: Padding(
                      padding: const EdgeInsets.all(8.0),
                      child: ElevatedButton(
                        style: ButtonStyle(
                          backgroundColor:
                              MaterialStateProperty.all(Colors.indigo),
                        ),
                        onPressed: () {
                          if (_formKey.currentState!.validate()) {
                            showDialog(
                              context: context,
                              builder: (context) {
                                return AlertDialog(
                                  title: const Text('Produk berhasil tersimpan'),
                                  content: SingleChildScrollView(
                                    child: Column(
                                      crossAxisAlignment:
                                          CrossAxisAlignment.start,
                                      children: [
                                        Text('Nama: $_name'),
                                        // TODO: Munculkan value-value lainnya
                                      ],
                                    ),
                                  ),
                                  actions: [
                                    TextButton(
                                      child: const Text('OK'),
                                      onPressed: () {
                                        Navigator.pop(context);
                                      },
                                    ),
                                  ],
                                );
                              },
                            );
                          _formKey.currentState!.reset();
                          } // if _formKey.currentState!.validate()
                        }, //onPressed
                        child: const Text(
                          "Save",
                          style: TextStyle(color: Colors.white),
                        ),
                      ),
                    ),
                  ), 
                ]
              )
            ),
          ),
        );
    }
}
```

2. Mengarahkan pengguna ke halaman form tambah item baru ketika menekan tombol Tambah Item pada halaman utama, dengan menggunakan Navigator push pada halaman utama sebenarnya pada menu.dart tetapi karena menerapkan clean architecture jadi pada shop_card.dart dengan import shop_card.dart di menu.dart. Berikut implementasi kode nya

```
if (item.name == "Tambah Produk") {
  // TODO: Gunakan Navigator.push untuk melakukan navigasi ke MaterialPageRoute yang mencakup ShopFormPage.
  Navigator.push(context,MaterialPageRoute(builder: (context) => const ShopFormPage()));
}
```

3. Memunculkan data sesuai isi dari formulir yang diisi dalam sebuah pop-up setelah menekan tombol Save pada halaman formulir tambah item baru, dengan menambahkan fungsi showDialog() pada bagian onPressed() dan munculkan widget AlertDialog, berikut implementasi kode nya

```
...
child: ElevatedButton(
          style: ButtonStyle(
            backgroundColor:
                MaterialStateProperty.all(Colors.indigo),
          ),
          onPressed: () {
            if (_formKey.currentState!.validate()) {
              showDialog(
                context: context,
                builder: (context) {
                  return AlertDialog(
                    title: const Text('Produk berhasil tersimpan'),
                    content: SingleChildScrollView(
                      child: Column(
                        crossAxisAlignment:
                            CrossAxisAlignment.start,
                        children: [
                          Text('Nama: $_name'),
                          // TODO: Munculkan value-value lainnya
                        ],
                      ),
                    ),
                    actions: [
                      TextButton(
                        child: const Text('OK'),
                        onPressed: () {
                          Navigator.pop(context);
                        },
                      ),
                    ],
                  );
                },
              );
            _formKey.currentState!.reset();
            }
          },
          child: const Text(
            "Save",
            style: TextStyle(color: Colors.white),
          ),
        ),
...
```

4. Membuat drawer yang akan mengarahkan pengguna ke Halaman utama atau tambah item dengan cara menggunakan Navigator pushReplacement pada ListTile. Berikut implementasi kode nya

```
import 'package:flutter/material.dart';
import 'package:inventory_manager/screens/menu.dart';
import 'package:inventory_manager/screens/shoplist_form.dart';

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          const DrawerHeader(
            // TODO: Bagian drawer header
            decoration: BoxDecoration(
              color: Colors.indigo,
            ),
            child: Column(
              children: [
                Text(
                  'Inventory Manager',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                Padding(padding: EdgeInsets.all(10)),
                Text("Catat seluruh keperluan belanjamu di sini!",
                    // TODO: Tambahkan gaya teks dengan center alignment, font ukuran 15, warna putih, dan weight biasa
                    textAlign: TextAlign.center,
                    style: TextStyle(
                      fontSize: 15,
                      color: Colors.white,
                      fontWeight: FontWeight.normal,
                    ),
                ),
              ],
            ),
          ),
          // TODO: Bagian routing
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Halaman Utama'),
            // Bagian redirection ke MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MyHomePage(),
                  ));
            },
          ),
          ListTile(
            leading: const Icon(Icons.add_shopping_cart),
            title: const Text('Tambah Produk'),
            // Bagian redirection ke ShopFormPage
            onTap: () {
              /*
              TODO: Buatlah routing ke ShopFormPage di sini,
              setelah halaman ShopFormPage sudah dibuat.
              */

              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => const ShopFormPage(),
                  ));
            },
          ),
        ],
      ),
    );
  }
}
```

dan pada menu.dart buat widget nya dengan cara `drawer: const LeftDrawer(),`.

# References
1. https://docs.flutter.dev/ui/widgets/layout?gclid=CjwKCAiA0syqBhBxEiwAeNx9N9K7XJzi0OCmH9SaYolNYKiLKKXJLNupSreivl-Yocg41_G8Rd9OfBoCAS0QAvD_BwE&gclsrc=aw.ds#Multi-child%20layout%20widgets


# Tugas 9 PBP

# Pengambilan data JSON tanpa membuat model itu dapat dilakukan. 
Pada Flutter, kita dapat menggunakan metode json.decode untuk mengurai string JSON menjadi objek Map<String, dynamic> dan mengakses value dengan menggunakan keys.

Namun, jika kita mengambil data JSON dengan membuat modelnya terlebih dahulu itu akan lebih unggul dan praktis. Kelas model dapat menyediakan berbagai tipe keamanan, validasi, dan keterbacaan untuk data JSON. Selain itu, dapat membantu terhindar dari kesalahan atau bug yang terjadi saat mengakses data JSON tanpa kelas model. 

#  fungsi dari CookieRequest dan alasan instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter
Fungsi CookieRequest adalah untuk menangani pengiriman dan penerimaan cookie dalam permintaan HTTP di Flutter.

Instance CookieRequest perlu dibagian ke semua komponen dalam Flutter karena instance tersebut menjaga objek CookieJar yang menyimpan semua cookie untuk domain dan jalur berbeda. Dengan berbagi instance CookieRequest yang sama, komponen yang berbeda dapat mengakses cookie yang sama dan menghindar pembuatan cookie konflik atau duplikat. 

# mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.
1. Pada inventory_manager versi django saya run terlebih dahulu lalu tambahkan /json pada browser yang menampilkan web app inventory_manager
2. Kemudian ambil data json dan convert menjadi code dart dengan quicktype
3. pada inventory_manager di flutter, buatlah file baru pada folder lib/models dengan nama product.dart, dan copy code dari quicktype ke product.dart
4. Kemudian buat dependensi http
5. Import yang dibutuhkan, yaitu :
```
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
import 'package:inventory_manager/models/product.dart';
```
6. Pada list_product.dart tambahkan kode berikut:
```
import 'package:<APP_NAME>/widgets/left_drawer.dart';

class ProductPage extends StatefulWidget {
    const ProductPage({Key? key}) : super(key: key);

    @override
    _ProductPageState createState() => _ProductPageState();
}

class _ProductPageState extends State<ProductPage> {
Future<List<Product>> fetchProduct() async {
    // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
    var url = Uri.parse(
        'http://<URL_APP_KAMU>/json/');
    var response = await http.get(
        url,
        headers: {"Content-Type": "application/json"},
    );

    // melakukan decode response menjadi bentuk json
    var data = jsonDecode(utf8.decode(response.bodyBytes));

    // melakukan konversi data json menjadi object Product
    List<Product> list_product = [];
    for (var d in data) {
        if (d != null) {
            list_product.add(Product.fromJson(d));
        }
    }
    return list_product;
}

@override
Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
        title: const Text('Product'),
        ),
        drawer: const LeftDrawer(),
        body: FutureBuilder(
            future: fetchProduct(),
            builder: (context, AsyncSnapshot snapshot) {
                if (snapshot.data == null) {
                    return const Center(child: CircularProgressIndicator());
                } else {
                    if (!snapshot.hasData) {
                    return const Column(
                        children: [
                        Text(
                            "Tidak ada data produk.",
                            style:
                                TextStyle(color: Color(0xff59A5D8), fontSize: 20),
                        ),
                        SizedBox(height: 8),
                        ],
                    );
                } else {
                    return ListView.builder(
                        itemCount: snapshot.data!.length,
                        itemBuilder: (_, index) => Container(
                                margin: const EdgeInsets.symmetric(
                                    horizontal: 16, vertical: 12),
                                padding: const EdgeInsets.all(20.0),
                                child: Column(
                                mainAxisAlignment: MainAxisAlignment.start,
                                crossAxisAlignment: CrossAxisAlignment.start,
                                children: [
                                    Text(
                                    "${snapshot.data![index].fields.name}",
                                    style: const TextStyle(
                                        fontSize: 18.0,
                                        fontWeight: FontWeight.bold,
                                    ),
                                    ),
                                    const SizedBox(height: 10),
                                    Text("${snapshot.data![index].fields.price}"),
                                    const SizedBox(height: 10),
                                    Text(
                                        "${snapshot.data![index].fields.description}")
                                ],
                                ),
                            ));
                    }
                }
            }));
    }
}
```
7. agar dapat ditampilkan tambahkan list_product.dart pada drawer (left_drawer.dart), dengan cara
```
// Sejajarkan dengan kode ListTile sebelumnya
ListTile(
    leading: const Icon(Icons.shopping_basket),
    title: const Text('Daftar Produk'),
    onTap: () {
        // Route menu ke halaman produk
        Navigator.push(
        context,
        MaterialPageRoute(builder: (context) => const ProductPage()),
        );
    },
),
```

8. pada shop_card.dart tambahkan handle untuk tombol yang menampilkan data pada bagian akhir onTap (){}, seperti berikut:
```
else if (item.name == "Lihat Produk") {
        Navigator.push(context,
            MaterialPageRoute(builder: (context) => const ProductPage()));
      }
```

9. Import file yang dibutuhkan saat menambahkan ProductPage ke left_drawer.dart dan shop_card.dart.

# mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
1. Buat django app authentication, kemudian tambahkan ke INSTALLED_APPS pada settings.py di direktori project inventory_manager
2. Install corsheader dengan `pip install django-cors-headers` kemudian tambahkan corsheader ke INSTALLED_APPS dan tambahkan ke middleware di settings.py di direktori project inventory_manager dengan tambahkan `corsheaders.middleware.CorsMiddleware`
3. Tambahkan variabel berikut 
```
CORS_ALLOW_ALL_ORIGINS = True
CORS_ALLOW_CREDENTIALS = True
CSRF_COOKIE_SECURE = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SAMESITE = 'None'
SESSION_COOKIE_SAMESITE = 'None'
```

4. Buat method view untuk login pada views.py di authentication
```
from django.shortcuts import render
from django.contrib.auth import authenticate, login as auth_login
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(username=username, password=password)
    if user is not None:
        if user.is_active:
            auth_login(request, user)
            # Status login sukses.
            return JsonResponse({
                "username": user.username,
                "status": True,
                "message": "Login sukses!"
                # Tambahkan data lainnya jika ingin mengirim data ke Flutter.
            }, status=200)
        else:
            return JsonResponse({
                "status": False,
                "message": "Login gagal, akun dinonaktifkan."
            }, status=401)

    else:
        return JsonResponse({
            "status": False,
            "message": "Login gagal, periksa kembali email atau kata sandi."
        }, status=401)
```

5. seperti biasa jika ada fungsi baru tambahkan ke urlpatterns pada urls.py pada authentication
6. Karena authentication app baru tambahkan `path('auth/', include('authentication.urls')),` pada urls.py di direktori project

7. untuk integrasi autentikasi install yang dibutuhkan dengan menjalankan kode berikut di terminal untuk project flutter (inventoru_manager_mobile)
```
flutter pub add provider
flutter pub add pbp_django_auth
```

8. untuk menggunakan package yang di install tersebut sediakan CookieRequest library ke semua child widgets dengan menggunakan Provider, dengan menambahkan return Provide pada myApp di inventory_manager_mobile, seperti berikut:
```
class MyApp extends StatelessWidget {
    const MyApp({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Provider(
            create: (_) {
                CookieRequest request = CookieRequest();
                return request;
            },
            child: MaterialApp(
                title: 'Flutter App',
                theme: ThemeData(
                    colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
                    useMaterial3: true,
                ),
                home: MyHomePage()),
            ),
        );
    }
}
```

9. Untuk menampilkan pada flutter buat file sebagai halaman tampilan untuk autentitasi, pada floder screens tambahkan file login.dart, dan isi dengan kode berikut:
```
import 'package:inventory_manager/screens/menu.dart';
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';

void main() {
    runApp(const LoginApp());
}

class LoginApp extends StatelessWidget {
const LoginApp({super.key});

@override
Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Login',
        theme: ThemeData(
            primarySwatch: Colors.blue,
    ),
    home: const LoginPage(),
    );
    }
}

class LoginPage extends StatefulWidget {
    const LoginPage({super.key});

    @override
    _LoginPageState createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
    final TextEditingController _usernameController = TextEditingController();
    final TextEditingController _passwordController = TextEditingController();

    @override
    Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();
        return Scaffold(
            appBar: AppBar(
                title: const Text('Login'),
            ),
            body: Container(
                padding: const EdgeInsets.all(16.0),
                child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [
                        TextField(
                            controller: _usernameController,
                            decoration: const InputDecoration(
                                labelText: 'Username',
                            ),
                        ),
                        const SizedBox(height: 12.0),
                        TextField(
                            controller: _passwordController,
                            decoration: const InputDecoration(
                                labelText: 'Password',
                            ),
                            obscureText: true,
                        ),
                        const SizedBox(height: 24.0),
                        ElevatedButton(
                            onPressed: () async {
                                String username = _usernameController.text;
                                String password = _passwordController.text;

                                // Cek kredensial
                                // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
                                // Untuk menyambungkan Android emulator dengan Django pada localhost,
                                // gunakan URL http://10.0.2.2/
                                final response = await request.login("http://<APP_URL_KAMU>/auth/login/", {
                                'username': username,
                                'password': password,
                                });
                    
                                if (request.loggedIn) {
                                    String message = response['message'];
                                    String uname = response['username'];
                                    Navigator.pushReplacement(
                                        context,
                                        MaterialPageRoute(builder: (context) => MyHomePage()),
                                    );
                                    ScaffoldMessenger.of(context)
                                        ..hideCurrentSnackBar()
                                        ..showSnackBar(
                                            SnackBar(content: Text("$message Selamat datang, $uname.")));
                                    } else {
                                    showDialog(
                                        context: context,
                                        builder: (context) => AlertDialog(
                                            title: const Text('Login Gagal'),
                                            content:
                                                Text(response['message']),
                                            actions: [
                                                TextButton(
                                                    child: const Text('OK'),
                                                    onPressed: () {
                                                        Navigator.pop(context);
                                                    },
                                                ),
                                            ],
                                        ),
                                    );
                                }
                            },
                            child: const Text('Login'),
                        ),
                    ],
                ),
            ),
        );
    }
}
```

10. Pada file main.dart, pada Widget MaterialApp(...), ubah home: MyHomePage() menjadi home: LoginPage()

# widget yang digunakan pada tugas ini dan fungsinya

Pada file login.dart
- LoginPage (Stateless Widget), untuk menampilkan halaman login
- SizedBox, untuk membuat box yang ukurannya fixed
Pada file list_item.dart
- ItemPage (Stateless Widget), untuk menampilkan halaman kumpulan item
- ItemDetailsPage (Stateless Widget), untuk menampilkan halaman detail item
- FutureBuilder, untuk menampilkan data dari operasi asinkron seperti mengambil data dari server atau melakukan perhitungan yang memerlukan waktu
- ListView.builder, untuk menampilkan daftar item secara dinamis berdasarkan sumber data yang bersifat berulang, seperti list atau array
- Expanded, widget agar mengexpand childnya sampai batasnya

# Cara mengimplementasi checklist step-by-step



