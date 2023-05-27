# Tutorial 7: Flutter Navigation, Input, dan Form

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer, Universitas Indonesia, Semester Genap 2022/2023

---

## Tujuan Pembelajaran

Setelah menyelesaikan tutorial ini, mahasiswa diharapkan untuk:

- Memahami elemen input dan form pada Flutter.
- Memahami navigasi dan _routing_ dasar pada Flutter.
- Memahami alur pembuatan form dan data pada Flutter.
- Memahami _clean architecture_ pada kode Flutter.

---

## Navigasi Halaman pada Flutter

Pada saat belajar pengembangan _web_, kalian pasti sudah belajar bahwa dalam sebuah _website_ kita dapat berpindah-pindah halaman sesuai dengan _url_ yang diakses. Begitu juga pada sebuah aplikasi, kita dapat melakukan perpindahan dari satu halaman ke halaman lain. Bedanya, pada sebuah aplikasi, yang kita gunakan untuk berpindah bukanlah dengan mengakses _url_.

Flutter menyediakan sistem yang cukup lengkap untuk melakukan navigasi antar halaman. Salah satu cara yang dapat kita gunakan untuk berpindah-pindah halaman adalah dengan menggunakan _widget_ `Navigator`. _Widget_ `Navigator` menampilkan layar seakan sebagai sebuah tumpukan (_stack_). Untuk menavigasi sebuah halaman baru, kita dapat mengakses `Navigator` melalui `BuildContext` dan memanggil fungsi `push()` atau `pop()`. Berikut contoh penggunaan `Navigator`.

```dart
...
onPressed: () {
    Navigator.of(context).push(
        MaterialPageRoute(
          builder: (context) => const MyNewScreen(myProp: prop),
        ),
    );
},
child: Text(myProp.someValue),
...
```

Untuk mengetahui lebih dalam terkait `Navigator`, dapat dibaca pada tautan berikut: [https://api.flutter.dev/flutter/widgets/Navigator-class.html](https://api.flutter.dev/flutter/widgets/Navigator-class.html)

---

## Input dan Form pada Flutter

Sama halnya dengan sebuah _web_, sebuah aplikasi juga dapat berinteraksi dengan pengguna melalui _input_ dan _form_. Flutter memiliki _widget_ `Form` yang dapat kita manfaatkan untuk menjadi wadah bagi beberapa _input field widget_ yang kita buat. Sama hal nya dengan _input field_ pada _web_, Flutter juga memiliki banyak tipe _input field_, salah satunya _widget_ `TextField`.

Untuk mencoba sampel dari _widget_ `Form`, jalankan perintah berikut:

```bash
flutter create --sample=widgets.Form.1 formSample
```

Untuk mengetahui lebih lanjut terkait _widget_ `Form`, dapat dibaca pada tautan berikut: <https://api.flutter.dev/flutter/widgets/Form-class.html>.

---

## Tutorial: Melakukan _Refactoring_ pada Halaman Menu

Sebelum kita terjun ke dalam bagian kode program, kita akan melakukan _refactoring_ struktur proyek kita terlebih dahulu. Hal ini dilakukan agar kode program lebih terstruktur. Dalam dunia nyata, praktik ini disebut dengan _clean architecture_.

Ikuti langkah-langkah berikut untuk menerapkan prinsip _clean architecture_ pada proyekmu.

1. Buka proyek yang sebelumnya telah dibuat pada tutorial 6 dengan menggunakan IDE favoritmu.

2. Buatlah sebuah folder baru dengan nama `pages` pada folder `lib`. Folder ini akan digunakan untuk menyimpan halaman-halaman dari aplikasimu.

3. Pindahkan halaman menu (`menu.dart`) yang sudah dibuat pada tutorial 6 ke dalam folder `lib/pages`.

4. Ubah bagian `import 'package:money_tracker/menu.dart';` menjadi `import 'package:money_tracker/pages/menu.dart';`.

5. Coba jalankan aplikasimu; jika tidak ada _error_, maka kamu telah berhasil melakukan _simple refactoring_.

---

## Tutorial: Membuat dan Menambahkan Drawer

Setelah melakukan _refactoring_, kita akan menambahkan _drawer/hamburger menu_. Menu ini berguna bagi para pengguna aplikasi untuk mengakses fitur-fitur yang ada pada aplikasi tanpa harus kembali ke _homepage_ untuk mengakses menu.

1. Buatlah sebuah folder baru dengan nama `widgets` pada folder `lib`. Folder ini akan digunakan untuk menyimpan _widgets_ pada aplikasimu.

2. Buatlah sebuah file baru dengan nama `drawer.dart` pada folder `lib/widgets`.

3. _Import_ beberapa file yang akan digunakan ke dalam `drawer.dart`.

    ```dart
    import 'package:money_tracker/pages/menu.dart';
    import 'package:flutter/material.dart';
    ```

4. Tambahkan kode berikut pada `drawer.dart`.

    ```dart
    class DrawerMenu extends StatelessWidget {

      const DrawerMenu({Key? key}) : super(key: key);

      @override
      Widget build(BuildContext context) {
        return Drawer(
          child: Column(
            children: [          
            ],
          ),
        );
      }
    }
    ```

5. Tambahkan halaman menu yang akan dimunculkan pada _drawer/hamburger_ menu dalam bentuk `ListTile`.

    ```dart
    ...
    child: Column(
          children: [
            // Menambahkan clickable menu
            ListTile(
              title: const Text('Menu'),
              onTap: () {
                // Route menu ke halaman utama
                Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(builder: (context) => const MyHomePage()),
                );
              },
            ),
    ...
    ```

6. Buka `pages/menu.dart` dan tambahkan _drawer_ ke halaman tersebut dengan menambahkan potongan kode berikut.

    ```dart
    ...
    appBar: AppBar(
      title: const Text(
        'Money Tracker',
      ),
    ),
    drawer: const DrawerMenu(), // Menambahkan drawer pada halaman
    body: SingleChildScrollView(
    ...
    ```

7. Jalankan aplikasimu dan _drawer/hamburger_ menu sudah muncul pada bagian kiri atas halaman menu.

---

## Tutorial: Membuat Halaman Form

Setelah membuat menu, kita akan membuat halaman form yang akan menerima input data dari pengguna. Untuk sekarang, kita hanya akan membuat halaman form dan menampilkan datanya secara lokal. Integrasi aplikasi Flutter dengan layanan Django akan dibahas pada lab berikutnya.

1. Buatlah file baru pada folder `lib/pages` dengan nama `form.dart`.

2. Tambahkan _boilerplate_ berikut ke dalam file tersebut.

    ```dart
    class MyFormPage extends StatefulWidget {
        const MyFormPage({super.key});

        @override
        State<MyFormPage> createState() => _MyFormPageState();
    }

    class _MyFormPageState extends State<MyFormPage> {
        @override
        Widget build(BuildContext context) {
            return Scaffold(
                appBar: AppBar(
                    title: Text('Form'),
                ),
                drawer: const DrawerMenu(),
                body: Center(
                    child: Column(
                        mainAxisAlignment: MainAxisAlignment.center,
                        children: <Widget>[
                            Text('Hello World!'),
                        ],
                    ),
                ),
            );
        }
    }
    ```

3. Tambahkan impor pada kode berikut.

    `/lib/pages/form.dart`

    ```dart
    import 'package:money_tracker/widgets/drawer.dart';
    import 'package:flutter/material.dart';
    import 'package:flutter/services.dart';
    ...
    ```

    `/lib/pages/menu.dart`

    ```dart
    import 'package:money_tracker/pages/form.dart';
    ...
    ```

    `lib/widgets/drawer.dart`

    ```dart
    import 'package:money_tracker/pages/form.dart';
    ```

4. Ubah fungsi tombol `Tambah Transaksi` pada `lib/pages/menu.dart` agar mengarahkan ke halaman `MyFormPage`. Kamu dapat melakukan _redirection_ dengan menambahkan kode berikut pada bagian `onTap: () { }` yang ada pada `Container` tombol `Tambah Transaksi` pada `MyHomePage`.

    ```dart
    ...
    Container(
    ...
      onTap: () {
        Navigator.pushReplacement(
          context,
          MaterialPageRoute(
              builder: (context) => const MyFormPage()),
        );
      }
    ),
    ...
    ```

5. Coba jalankan aplikasi untuk melihat perubahan yang baru saja kamu buat. Seharusnya terdapat drawer atau _hamburger menu_ pada pojok kiri atas dan halaman form berisi teks “Hello World!”.

---

## Tutorial: Menambahkan Form dan Elemen Input

Kita akan mencoba untuk menambahkan dua tipe input form yang ada di Flutter, yaitu `TextFormField` dan `DropdownButton`.

1. Ubah _widget_ `Center` menjadi `Form`.

    ```dart
    body: Form(),
    ```

2. Tambahkan _form key_ sebagai _handle_ dari _state_, validasi, dan penyimpanan form.

    ```dart
    ...
    class _MyFormPageState extends State<MyFormPage> {
    final _formKey = GlobalKey<FormState>();

    @override
    ...
        body: Form(
            key: _formKey,
        ),
    ...
    ```

3. Buatlah _widget_ `SingleChildScrollView` sebagai _child_ dari _widget_ `Form`.

    ```dart
    ...
    body: Form(
      key: _formKey,
      child: SingleChildScrollView(),
    ),
    ...
    ```

4. Buatlah _widget_ `Container` sebagai _child_ dari _widget_ `SingleChildScrollView`.

    ```dart
    ...
    child: SingleChildScrollView(
      child: Container(),
    ),
    ...
    ```

5. Tambahkan _padding_ pada _widget_ `Container` agar tampilan _widget_ menjadi rapi. Sebagai contoh, kita akan memakai _padding_ sebesar 20 _pixels_.

    ```dart
    ...
    child: Container(
      padding: const EdgeInsets.all(20.0),
    ),
    ...
    ```

6. Buatlah _widget_ `Column` sebagai _child_ dari _widget_ `Container`.

    ```dart
    ...
    child: Container(
      padding: const EdgeInsets.all(20.0),
      child: Column(),
    ),
    ...
    ```

7. Buatlah _widget_ `TextFormField` yang dibungkus oleh `Padding` sebagai salah satu _children_ dari _widget_ `Column`. Selain itu, tambahkan variabel baru sebagai _placeholder_ dari nilai yang diketik pada `TextFormField` nantinya. Buatlah `TextFormField` sebagai penampung variabel nama transaksi. Berikut adalah contohnya.

    ```dart
    ...
    class _MyFormPageState extends State<MyFormPage> {
    final _formKey = GlobalKey<FormState>();
    String _namaTransaksi = "";
    
    @override
    ...
              child: Column(
                children: [
                  Padding(
                    // Menggunakan padding sebesar 8 pixels
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Contoh: Bayar UKT",
                        labelText: "Nama Transaksi",
                        // Menambahkan icon agar lebih intuitif
                        icon: const Icon(Icons.edit_note),
                        // Menambahkan circular border agar lebih rapi
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      // Menambahkan behavior saat nama diketik
                      onChanged: (String? value) {
                        setState(() {
                          _namaTransaksi = value!;
                        });
                      },
                      // Menambahkan behavior saat data disimpan
                      onSaved: (String? value) {
                        setState(() {
                          _namaTransaksi = value!;
                        });
                      },
                      // Validator sebagai validasi form
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return 'Nama transaksi tidak boleh kosong!';
                        }
                        return null;
                      },
                    ),
                  ),
    ...
    ```

8. Buatlah _widget_ `DropdownButton` sebagai salah satu _children_ dari _widget_ `Column`. Tambahkan variabel baru sebagai _placeholder_ dari nilai _dropdown_ nantinya. Selain itu, tambahkan pula `List` of `String` yang menampung opsi yang akan ditampilkan pada _dropdown_. Berikut adalah contohnya.

    ```dart
    ...
    String tipeTransaksi = 'Pengeluaran';
    List<String> listTipeTransaksi = ['Pengeluaran', 'Pemasukan'];
    
    @override
    ...
                    ListTile(
                    leading: const Icon(Icons.class_),
                    title: const Text(
                      'Tipe Transaksi:',
                    ),
                    trailing: DropdownButton(
                      value: tipeTransaksi,
                      icon: const Icon(Icons.keyboard_arrow_down),
                      items: listTipeTransaksi.map((String items) {
                        return DropdownMenuItem(
                          value: items,
                          child: Text(items),
                        );
                      }).toList(),
                      onChanged: (String? newValue) {
                        setState(() {
                          tipeTransaksi = newValue!;
                        });
                      },
                    ),
                  ),
    ...
    ```

9. Buatlah _widget_ T`extFormField` yang dibungkus oleh `Padding` sebagai salah satu _children_ dari _widget_ `Column`. Selain itu, tambahkan variabel baru sebagai _placeholder_ dari nilai yang diketik pada `TextFormField` nantinya. Buatlah `TextFormField` sebagai penampung variabel jumlah transaksi. Berikut adalah contohnya.

    ```dart
    ...
    int jumlahTransaksi = 0;

    @override
    ...
                    Padding(
                    // Menggunakan padding sebesar 8 pixels
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      keyboardType: TextInputType.number,
                      inputFormatters: <TextInputFormatter>[
                        FilteringTextInputFormatter.digitsOnly
                      ],
                      decoration: InputDecoration(
                        hintText: "Contoh: 1000000",
                        labelText: "Jumlah Transaksi",
                        // Menambahkan icon agar lebih intuitif
                        icon: const Icon(Icons.edit_note),
                        // Menambahkan circular border agar lebih rapi
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      // Menambahkan behavior saat jumlah diketik
                      onChanged: (String? value) {
                        setState(() {
                          jumlahTransaksi = int.parse(value!);
                        });
                      },
                      // Menambahkan behavior saat data disimpan
                      onSaved: (String? value) {
                        setState(() {
                          jumlahTransaksi = int.parse(value!);
                        });
                      },
                      // Validator sebagai validasi form
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return 'Jumlah transaksi tidak boleh kosong!';
                        }
                        return null;
                      },
                    ),
                  ),
    ...
    ```

10. Buatlah _widget_ `TextFormField` yang dibungkus oleh `Padding` sebagai salah satu _children_ dari _widget_ `Column`. Selain itu, tambahkan variabel baru sebagai _placeholder_ dari nilai yang diketik pada `TextFormField` nantinya. Buatlah `TextFormField` sebagai penampung variabel deskripsi transaksi. Berikut adalah contohnya.

    ```dart
    ...
    String _deskripsiTransaksi = "";

    @override
    ...
                    Padding(
                    // Menggunakan padding sebesar 8 pixels
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Contoh: Sebelum masuk semester!",
                        labelText: "Deskripsi Transaksi",
                        // Menambahkan icon agar lebih intuitif
                        icon: const Icon(Icons.notes),
                        // Menambahkan circular border agar lebih rapi
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      // Menambahkan behavior saat nama diketik
                      onChanged: (String? value) {
                        setState(() {
                          _deskripsiTransaksi = value!;
                        });
                      },
                      // Menambahkan behavior saat data disimpan
                      onSaved: (String? value) {
                        setState(() {
                          _deskripsiTransaksi = value!;
                        });
                      },
                      // Validator sebagai validasi form
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return 'Deskripsi transaksi tidak boleh kosong!';
                        }
                        return null;
                      },
                    ),
                  ),
    ...
    ```

11. Buatlah tombol yang akan menyimpan data yang ada di setiap elemen input. Kali ini kita tidak akan menyimpan data ke dalam _database_, namun kita akan memunculkannya pada _popup_ yang akan muncul setelah tombol ditekan.

    ```dart
              ...
              TextButton(
                child: const Text(
                  "Tambah",
                  style: TextStyle(color: Colors.white),
                ),
                style: ButtonStyle(
                  backgroundColor: MaterialStateProperty.all(Colors.blue),
                ),
                onPressed: () {
                  if (_formKey.currentState!.validate()) {}
                },
              ),
              ...
    ```

Setelah semua input dan logika form dibuat, maka kita akan membuat _popup_ yang akan memunculkan data yang ada pada input form saat tombol `Tambah` ditekan.

---

## Tutorial: Memunculkan Data

1. Tambahkan fungsi `showDialog()` pada bagian `onPressed()` dan munculkan _widget_ `Dialog` pada fungsi tersebut. Berikut adalah contoh potongan kodenya.

    ```dart
    ...
    onPressed: () {
      if (_formKey.currentState!.validate()) {
        showDialog(
          context: context,
          builder: (context) {
            return Dialog(
              shape: RoundedRectangleBorder(
                borderRadius: BorderRadius.circular(10),
              ),
              elevation: 15,
              child: Container(
                child: ListView(
                  padding: const EdgeInsets.only(top: 20, bottom: 20),
                  shrinkWrap: true,
                  children: <Widget>[
                    Center(child: const Text('Informasi Data')),
                    SizedBox(height: 20),
                    // TODO: Munculkan informasi yang didapat dari form
                    TextButton(
                      onPressed: () {
                        Navigator.pop(context);
                      },
                      child: Text('Kembali'),
                    ),
                  ],
                ),
              ),
            );
          },
        );
      }
    },
    ...
    ```

2. Silakan tambahkan informasi yang didapat dari form secara mandiri. Kamu dapat menggunakan widget `Text` dan melakukan _string interpolation_ agar keterangan data dan isi data dapat disajikan dalam satu widget. Contohnya adalah `Text('Nama Transaksi: $_namaTransaksi')`.

3. Coba jalankan program kamu, gunakan form yang telah dibuat, dan lihat hasilnya.

---

## Akhir Kata

Selamat, kamu telah mempelajari navigasi dasar dan pembuatan form dasar pada Flutter!

Setelah kamu menyelesaikan seluruh tutorial di atas, kamu dapat mencoba widget input lainnya yang ada di Flutter. Kamu juga dapat mencoba untuk membuat halaman baru dengan opsi navigasi yang berbeda, seperti `Navigator.push()` dan `Navigator.pop()`.

Jika kamu ingin mencoba tantangan, maka cobalah untuk menerapkan hal berikut pada tutorial ini.

- Modifikasi navigasi pada Drawer agar melakukan `Navigator.pop()` apabila halaman yang ingin dibuka adalah halaman yang sedang dibuka, alih-alih mengunakan `Navigator.pushReplacement()` untuk semua navigasi.
- Kustomisasi widget-widget yang telah kamu buat sebelumnya (_styling_), seperti warna, ikon, dll.

---

## Referensi Tambahan

- [Build a form with validation](https://docs.flutter.dev/cookbook/forms/validation)
- [Input widgets](https://docs.flutter.dev/development/ui/widgets/input)
- [Navigation and routing](https://docs.flutter.dev/development/ui/navigation)

---

## Credits

Tutorial ini dikembangkan berdasarkan [PBP Ganjil 2023](https://github.com/pbp-fasilkom-ui/ganjil-2023) yang ditulis oleh Tim Pengajar Pemrograman Berbasis Platform 2023. Segala tutorial serta instruksi yang dicantumkan pada repositori ini dirancang sedemikian rupa sehingga mahasiswa yang sedang mengambil mata kuliah Pemrograman Berbasis Platform dapat menyelesaikan tutorial saat sesi lab berlangsung.
