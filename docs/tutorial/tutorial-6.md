# Tutorial 6: Pengantar Tentang Flutter

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer Universitas Indonesia, Semester Genap 2022/2023

---

## Tujuan Pembelajaran

Setelah menyelesaikan tutorial ini, mahasiswa diharapkan untuk:

- Mengerti proses instalasi Flutter.
- Mengerti dan menggunakan perintah-perintah dasar Flutter yang perlu diketahui untuk mengerjakan proyek aplikasi.
- Memahami alur dasar pembuatan dan eksekusi aplikasi Flutter.
- Memahami elemen-elemen dasar pada Flutter.

---

## Pengenalan Flutter

Flutter adalah sebuah _framework_ aplikasi _mobile_ sumber terbuka (_open source_) yang diciptakan oleh Google pada 2017. Flutter digunakan dalam pengembangan aplikasi untuk sistem operasi Android dan iOS. Flutter juga mendukung untuk pengembangan aplikasi berbasis web, Windows, Linux, dan MacOS secara _native_.

Keuntungan dari Flutter sendiri adalah kemampuannya untuk menciptakan aplikasi untuk berbagai _platform_ dengan hanya satu _codebase_. Selain itu, fitur JIT (_just in time_) memungkinkan pengembang aplikasi untuk melihat perubahan yang dilakukan pada _codebase_ secara langsung tanpa harus mengulang proses kompilasi kode aplikasi dari awal.

---

## Instalasi Flutter

1. Akses tautan berikut sesuai dengan sistem operasi yang kamu gunakan.

    a. [Mac OS](https://docs.flutter.dev/get-started/install/macos)
  
    Khusus pengguna Mac OS yang menggunakan Homebrew, kamu dapat menggunakan perintah `brew install --cask flutter` untuk menginstal Flutter.
  
    b. [Windows](https://docs.flutter.dev/get-started/install/windows)

    c. [Linux](https://docs.flutter.dev/get-started/install/linux)

2. Instal Flutter versi terkini (_latest version_) dengan mengikuti panduan pada tautan di atas.
  
    Untuk pengguna Mac, dapat melewati tahap `iOS Setup` dan langsung ke tahap `Android Setup`.

3. Instal IDE pilihan kamu yang akan digunakan untuk mengembangkan aplikasi Flutter.

    a. [Android Studio (Recommended)](https://developer.android.com/studio)

    b. [Visual Studio Code](https://code.visualstudio.com/)

    Kamu dapat menggunakan Visual Studio Code untuk Flutter dengan menginstall ekstensi [Dart](https://marketplace.visualstudio.com/items?itemName=Dart-Code.dart-code) dan [Flutter](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter).

    Kamu juga dapat membaca fungsionalitas IDE yang disediakan oleh ekstensi Flutter pada tautan yang tersedia.

---

## Tutorial: _Getting Started with Flutter_

1. Buka Terminal atau Command Prompt.

2. Masuk ke direktori sesuai keinginan masing-masing.

3. _Generate_ proyek Flutter dan masuk ke dalam direktori proyek (`APP_NAME` pada proyek ini adalah money_tracker).

    ```bash
    flutter create <APP_NAME>
    cd <APP_NAME>
    ```

4. Jalankan proyek melalui Terminal atau Command Prompt.

    ```bash
    flutter run
    ```

5. Akan muncul tampilan seperti di bawah ini.

    ![First App](https://i.ibb.co/GTq5p70/693e69f5108186abc024710adf4387bb.jpg)

6. Lakukan `git init` pada _root folder_ dan `add`-`commit`-`push` proyek ke sebuah repositori baru di GitHub. Kamu dapat menamai repositori barumu dengan nama `pbp-flutter-tutorial`.

---

## Tutorial: Merapikan Struktur Proyek

Sebelum kita bermain dengan Flutter lebih lanjut, kita akan merapikan struktur file pada proyek kita terlebih dahulu agar kode proyek dapat dipahami lebih baik.

1. Buatlah file baru bernama `menu.dart` pada folder `lib`.

2. Potong (_cut_) isi file `main.dart` dari baris 32 (`class MyHomePage extends StatefulWidget`) sampai akhir file dan tempelkan kodenya pada file `menu.dart`. Jika kamu melihat tulisan peringatan berwarna merah, jangan khawatir; kita akan menyelesaikannya setelah ini.

3. Pada file `menu.dart`, salin dan tempel `import 'package:flutter/material.dart';` pada baris paling awal pada file.

    ![Photo](https://i.ibb.co/ZWmbt8q/Selection-2292.png)

4. Pada file `main.dart`, _hover_ kursor ke kode yang bermasalah dan selesaikan masalahnya dengan mengikuti petunjuk tangkapan layar berikut

    Pilihlah opsi `Quick Fix`.

    ![Langkah 1](https://i.ibb.co/nDdJMzx/Screenshot-2023-04-11-10-46-25.jpg)

    Pilihlah opsi `Import library 'package:money_tracker/menu.dart'`.

    ![Langkah 2](https://i.ibb.co/3mv5pBs/Screenshot-2023-04-11-10-46-36.jpg)

5. Coba jalankan proyek melalui Terminal atau Command Prompt untuk melihat apakah aplikasi tetap dapat berjalan.

---

## Tutorial: Membuat Widget Sederhana pada Flutter

Pada tutorial kali ini, kita akan belajar membuat widget sederhana pada Flutter. Kita akan membuat widget text sebagai judul dan button sebagai menu untuk aplikasi kita. Ketika button dipencet, akan muncul notifikasi di bawah layar berupa tombol apa yang dipencet.

Pertama-tama, kita akan mengubah tema warna aplikasi menjadi hijau.

1. Buka file `main.dart`.

2. Ubahlah isi kode `primarySwatch` menjadi `Colors.green`.

    ```dart
    primarySwatch: Colors.green,
    ```

3. Hapus `title` yang ada pada `const MyHomePage(title: 'Flutter Demo Home Page')` sehingga menjadi:

    ```dart
    const MyHomePage()
    ```

Coba jalankan proyek kamu untuk melihat apakah warna tema aplikasi sudah berubah menjadi hijau.

Setelah mengubah warna tema aplikasi, kita akan mengubah sifat widget halaman menu menjadi _stateless_.

1. Ubah sifat _widget_ halaman dari _stateful_ menjadi _stateless_ pada file `menu.dart`. Ubah `({super.key, required this.title})` menjadi `({Key? key}) : super(key: key);`. Hapus `final String title;` sampai bawah serta tambahkan Widget `build` sehingga kode terlihat seperti di bawah.

    ```dart
    class MyHomePage extends StatelessWidget {
        const MyHomePage({Key? key}) : super(key: key);

        @override
        Widget build(BuildContext context) {
            return Scaffold(
                ...
            );
        }
    }
    ```

Setelah mengubah sifat _widget_ halaman menu menjadi _stateless_, kita akan menambahkan teks dan _grid buttons_ yang akan menjadi menu aplikasi.

1. Untuk menambahkan teks dan juga _grid buttons_, tambahkan potongan kode berikut pada bagian `Widget build(BuildContext context)`.

    ```dart
    return Scaffold(
      appBar: AppBar(
        // Set title aplikasi menjadi Money Tracker
        title: const Text( 
          'Money Tracker',
        ),
      ),
      body: SingleChildScrollView( // Widget wrapper yang dapat discroll
        child: Padding( 
          padding: const EdgeInsets.all(10.0), // Set padding dari halaman
          child: Column( // Widget untuk menampilkan children secara vertikal
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                child: Text(
                  'Selamat datang!',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // Grid layout
              GridView.count(
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: <Widget>[
                  Material(
                    color: Colors.green,
                    child: InkWell( // Area responsive terhadap sentuhan
                      onTap: () {
                        // Memunculkan SnackBar ketika diklik
                        ScaffoldMessenger.of(context)
                        ..hideCurrentSnackBar()
                        ..showSnackBar(const SnackBar(
                          content: Text("Kamu telah menekan tombol Lihat Riwayat Transaksi!")));
                      },
                      child: Container( // Container untuk menyimpan Icon dan Text
                        padding: const EdgeInsets.all(8),
                        child: Center(
                          child: Column(
                            mainAxisAlignment: MainAxisAlignment.center,
                            children: const [
                              Icon(
                                Icons.list_alt,
                                color: Colors.white,
                                size: 30.0,
                              ),
                              Padding(padding: EdgeInsets.all(3)),
                              Text(
                                "Lihat Riwayat Transaksi",
                                textAlign: TextAlign.center,
                                style: TextStyle(color: Colors.white),
                              ),
                            ],
                          ),
                        ),
                      ),
                    ),
                  ),
                  Material(
                    color: Colors.green,
                    child: InkWell(
                      onTap: () {
                        ScaffoldMessenger.of(context)
                        ..hideCurrentSnackBar()
                        ..showSnackBar(const SnackBar(
                          content: Text("Kamu telah menekan tombol Tambah Transaksi!")));
                      },
                      child: Container(
                        padding: const EdgeInsets.all(8),
                        child: Center(
                          child: Column(
                            mainAxisAlignment: MainAxisAlignment.center,
                            children: const [
                              Icon(
                                Icons.add_box,
                                color: Colors.white,
                                size: 40.0,
                              ),
                              Padding(padding: EdgeInsets.all(1)),
                              Text(
                                "Tambah Transaksi",
                                textAlign: TextAlign.center,
                                style: TextStyle(color: Colors.white),
                              ),
                            ],
                          ),
                        ),
                      ),
                    ),
                  ),
                  Material(
                    color: Colors.green,
                    child: InkWell(
                      onTap: () {
                        ScaffoldMessenger.of(context)
                        ..hideCurrentSnackBar()
                        ..showSnackBar(const SnackBar(
                          content: Text("Kamu telah menekan tombol Logout!")));
                      },
                      child: Container(
                        padding: const EdgeInsets.all(8),
                        child: Center(
                          child: Column(
                            mainAxisAlignment: MainAxisAlignment.center,
                            children: const [
                              Icon(
                                // Kamu juga dapat mengggunakan icon lainnya
                                // seperti Icons.logout
                                Icons.door_back_door,
                                color: Colors.white,
                                size: 30.0,
                              ),
                              Padding(padding: EdgeInsets.all(3)),
                              Text(
                                "Logout",
                                textAlign: TextAlign.center,
                                style: TextStyle(color: Colors.white),
                              ),
                            ],
                          ),
                        ),
                      ),
                    ),
                  ),
                ],
              ),
            ],
          ),
        ),
      ),
    );
    ```

2. Coba jalankan proyek dan kamu telah berhasil membuat _widget_ sederhana pada aplikasi Flutter. Aplikasi akan tampil seperti tangkapan layar di bawah ini.

  ![Menu](https://i.ibb.co/D5s6Xyq/app-one-001.png)

  ![Menu Snackbar](https://i.ibb.co/yYL9cvh/app-one-002.png)

---

## Akhir Kata

Selamat, kamu telah membuat aplikasi Flutter pertamamu!

Setelah kamu menyelesaikan seluruh tutorial di atas, harapannya kini kamu lebih paham dan ke depannya kamu dapat lebih banyak bereksplorasi dengan _framework_ Flutter dalam membuat sebuah aplikasi _multiplatform_.

Sebagai contoh, kamu dapat mengeksplorasi _built-in icons_ pada Flutter [di sini](https://api.flutter.dev/flutter/material/Icons-class.html).

Jangan lupa untuk mengumpulkan tautan repositori kamu ke slot submisi yang ada pada Scele, ya.

**_Happy coding!_**

---

## Credits

Tutorial ini dikembangkan berdasarkan [PBP Ganjil 2023](https://github.com/pbp-fasilkom-ui/ganjil-2023) yang ditulis oleh Tim Pengajar Pemrograman Berbasis Platform 2023. Segala tutorial serta instruksi yang dicantumkan pada repositori ini dirancang sedemikian rupa sehingga mahasiswa yang sedang mengambil mata kuliah Pemrograman Berbasis Platform dapat menyelesaikan tutorial saat sesi lab berlangsung.
