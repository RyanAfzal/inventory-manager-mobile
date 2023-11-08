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
6. Buat file baru bernama menu.dart pada shopping_list/lib dan ```import 'package:flutter/material.dart';```
7. Isi menu.dart dengan kode yang dipindahkan dari main.dart dari baris ke 39 hingga akhir
8. Pada main.dart tambahkan ```import 'package:shopping_list/menu.dart';```
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
