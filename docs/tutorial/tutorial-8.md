# Tutorial 8: Flutter Model, State Management Dasar, dan Pengintegrasian dengan Web Service

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer, Universitas Indonesia, Semester Genap 2022/2023

---

## Tujuan Pembelajaran

Setelah menyelesaikan tutorial ini, mahasiswa diharapkan untuk:

- Memahami struktur dan pembuatan model pada Flutter.
- Memahami *package* `provider` untuk melakukan *state management* dasar.
- Dapat melakukan autentikasi dengan *web service* Django dengan aplikasi Flutter.
- Memahami cara mengambil, mengolah, dan menampilkan data dari *web service* yang sudah ada.

---

## Model pada Flutter

Pada tutorial kali ini, kita akan membuat sebuah pemanggilan *web service* hingga menampilkannya ke halaman Flutter yang kita buat. Akan tetapi sebelum melakukan pemanggilan *web service*, kita perlu mendefinisikan model yang kita gunakan ketika melakukan pemanggilan *web service*. Model pada Flutter menggunakan prinsip *class* seperti layaknya yang sudah dipelajari pada DDP2 bagian OOP.

> Kode di bawah ini adalah contoh, tidak wajib diikuti, tetapi sangat disarankan dibaca karena konsepnya akan digunakan pada bagian-bagian selanjutnya.

Berikut merupakan contoh *class* pada Flutter.

```dart
class Mobil {
    Mobil({
        this.id,
        this.brand,
        this.model
        this.color
    });

    int id;
    String brand;
    String model;
    String color;
}
```

Catatan: Jika kamu mengalami *error* saat membuat *class*, tambahkan *keyword* `required` pada setiap parameter *class* pada bagian konstruktor.

Sampai saat ini, kita telah berhasil membuat *class*. Selanjutnya, kita akan menambahkan beberapa kode sehingga terbentuk sebuah model `Mobil`. `Mobil` ini merupakan suatu model yang merepresentasikan response dari pemanggilan *web service*.

Imporlah `dart:convert` pada bagian paling atas file.

```dart
import 'dart:convert';
...
```

Pada *class* `Mobil`, tambahkan kode berikut.

```dart
factory Mobil.fromJson(Map<String, dynamic> json) => Mobil(
    id: json["id"],
    brand: json["brand"],
    model: json["model"],
    color: json["color"],
);

Map<String, dynamic> toJson() => {
    "id": id,
    "brand": brand,
    "model": model,
    "color": color,
};
```

Tambahkan kode berikut di luar *class* `Mobil`.

```dart
Mobil mobilFromJson(String str) => Mobil.fromJson(json.decode(str));
String mobilToJson(Mobil data) => json.encode(data.toJson());
```

Sehingga kode akhirnya akan seperti berikut untuk menampilkan satu objek `Mobil` dari *web service*.

```dart
import 'dart:convert';

Mobil mobilFromJson(String str) => Mobil.fromJson(json.decode(str));
String mobilToJson(Mobil data) => json.encode(data.toJson());

class Mobil {
    Mobil({
        this.id,
        this.brand,
        this.model,
        this.color,
    });

    int id;
    String brand;
    String model;
    String color;

    factory Mobil.fromJson(Map<String, dynamic> json) => Mobil(
        id: json["id"],
        brand: json["brand"],
        model: json["model"],
        color: json["color"],
    );

    Map<String, dynamic> toJson() => {
        "id": id,
        "brand": brand,
        "model": model,
        "color": color,
    };
}
```

Penjelasan kode di atas adalah sebagai berikut.

Terdapat beberapa kode-kode tambahan seperti *method* `toJson` dan `fromJson` di dalam *class* `Mobil`. Hal tersebut disebabkan ketika kita me-*request* suatu *web service* dengan *method* **GET**, umumnya kita mendapatkan hasil pemanggilan berupa JSON. Oleh karena itu, kita perlu melakukan konversi data dengan *method* `fromJson` agar Flutter mengenali JSON tersebut sebagai objek *class* `Mobil`. Selain itu, terdapat juga *method* `toJson` yang akan digunakan ketika kita melakukan pengiriman data ke *web service* (seperti **POST** atau **PUT**).

Berikut adalah contoh respons dari *web service* dengan *method* **GET** yang dapat dikonversi ke *class* model **Mobil** tersebut.

```json
{
   "id": 1,
   "brand": "Honda",
   "model": "Civic",
   "color": "Yellow"
}
```

Lalu, bagaimana jika respons dari *web service* berupa kumpulan objek JSON? Sebenarnya sama saja dengan kode di atas, hanya saja terdapat pengubahan pada *method* `mobilFromJson` dan `mobilToJson`.

Kodenya adalah sebagai berikut.

```dart
List<Mobil> mobilFromJson(String str) => List<Mobil>.from(json.decode(str).map((mobil) => Mobil.fromJson(mobil)));

String mobilToJson(List<Mobil> data) => json.encode(List<dynamic>.from(data.map((mobil) => mobil.toJson())));
```

Berikut adalah contoh respons dari *web service* dengan *method* **GET** yang dapat dikonversi ke model `Mobil` tersebut.

```json
[
  {
    "id": 1,
    "brand": "Honda",
    "model": "Civic",
    "color": "Yellow"
  },
  {
    "id": 2,
    "brand": "Toyota",
    "model": "Supra",
    "color": "Red"
  }
]
```

---

## *Fetch Data* dari *Web Service* pada Flutter

Sebagai seorang *developer*, tentunya kita membutuhkan data untuk ditampilkan ke klien. Hal ini mengharuskan kalian untuk mengetahui bagaimana cara untuk melakukan *fetching data* dari *web service* kemudian menampilkannya ke aplikasi yang telah kita buat sebelumnya.

Secara umum terdapat beberapa langkah ketika ingin menampilkan data dari *web service* lain ke aplikasi Flutter, yaitu:

1. Menambahkan *dependency* `http` ke proyek, *dependency* ini digunakan untuk bertukar data melalui *HTTP request*, seperti **GET**, **POST**, **PUT**, dan lain-lain.

2. Membuat model sesuai dengan respons dari data yang berasal dari *web service* tersebut.

3. Membuat *http request* ke *web service* menggunakan *dependency* `http`.

4. Mengkonversikan objek yang didapatkan dari *web service* ke model yang telah kita buat di langkah kedua.

5. Menampilkan data yang telah dikonversi ke aplikasi dengan `FutureBuilder`.

Penjelasan lebih lanjut dapat dibaca pada tautan berikut: <https://docs.flutter.dev/cookbook/networking/fetch-data#5-display-the-data>.

---

## *State Management* Dasar dengan Provider

`Provider` adalah sebuah pembungkus di sekitar `InheritedWidget` agar `InheritedWidget` lebih mudah digunakan dan lebih dapat digunakan kembali. `InheritedWidget` sendiri adalah kelas dasar untuk widget Flutter yang secara efisien menyebarkan informasi ke widget lainnya yang berada pada satu *tree*.

Manfaat menggunakan `provider` adalah sebagai berikut.

- Mengalokasikan *resource* menjadi lebih sederhana.
- *Lazy-loading*.
- Mengurangi *boilerplate* tiap kali membuat *class* baru.
- Didukung oleh Flutter Devtool sehingga `provider` dapat di-*track* dari Devtool.
- Peningkatan skalabilitas untuk *class* yang memanfaatkan mekanisme *listen* yang dibangun secara kompleks.

Untuk mengetahui `provider` secara lebih lanjut, silakan buka halaman *package* Provider: <https://pub.dev/packages/provider>

---

## Tutorial: Migrasi Server ke PaaS Lain

Tim asisten dosen telah menemukan dua PaaS (*Platform as a Service*) alternatif yang lebih baik. Silakan baca informasi lebih lanjut dan ikuti langkah-langkah yang dituliskan pada blog berikut: [Bahas Hosting (Lagi) - Cecoret](https://determinedguy.github.io/cecoret/hosting-alternatives/)

> **Pastikan kamu telah memindahkan server tutorial kamu ke salah satu PaaS yang disebutkan sebelum kamu mengerjakan tutorial ini.**

---

## Tutorial: Integrasi Sistem Autentikasi *Web Service* Django dengan Aplikasi Flutter

Untuk memudahkan pembuatan sistem autentikasi, tim asisten dosen telah membuatkan *package* Flutter yang dapat dipakai untuk melakukan kontak dengan *web service* Django (termasuk operasi `GET` dan `POST`).

*Package* dapat diakses melalui tautan berikut: [pbp_django_auth](https://pub.dev/packages/pbp_django_auth)

Untuk menginstal _package_ tersebut, jalankan perintah berikut.

```bash
flutter pub add pbp_django_auth
flutter pub add provider
```

Ikuti langkah-langkah berikut untuk melakukan integrasi sistem autentikasi pada **Django**.

1. Buatlah `django-app` bernama `authentication` dengan perintah `python manage.py startapp authentication` pada aplikasi Django yang telah kamu buat sebelumnya.

2. Tambahkan `authentication` ke `INSTALLED_APPS` pada `django_tutorial/settings.py` aplikasimu.

3. Jalankan perintah `pip install django-cors-headers` untuk menginstal _library_ yang dibutuhkan.

4. Tambahkan `corsheaders` ke `INSTALLED_APPS` pada `django_tutorial/settings.py` aplikasi.

5. Tambahkan `corsheaders.middleware.CorsMiddleware` ke `MIDDLEWARE` pada `django_tutorial/settings.py` aplikasi.

6. Buatlah sebuah variabel baru di `django_tutorial/settings.py` dengan  ama `CORS_ALLOW_ALL_ORIGINS` dan berikan nilai `True`, (`CORS_ALLOW_ALL_ORIGINS=True`).

7. Buatlah sebuah variabel baru di `django_tutorial/settings.py` dengan nama `CORS_ALLOW_CREDENTIALS` dan berikan nilai `True`, (`CORS_ALLOW_CREDENTIALS=True`).

8. Tambahkan beberapa variabel berikut ini pada `django_tutorial/settings.py` aplikasi.

    ```python
    CSRF_COOKIE_SECURE = True
    SESSION_COOKIE_SECURE = True
    CSRF_COOKIE_SAMESITE = 'None'
    SESSION_COOKIE_SAMESITE = 'None'
    ```

9. Buatlah sebuah metode _view_ untuk login pada `authentication/views.py`.

    ```python
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
                "message": "Login gagal, periksa kembali email/password."
            }, status=401)
    ```

10. Buat _file_ `urls.py` pada folder `authentication` dan tambahkan kode berikut.

    ```python
    from django.urls import path
    from authentication.views import *

    app_name = 'authentication'

    urlpatterns = [
        path('login/', login, name='login'),
    ]
    ```

11. Terakhir, tambahkan `path('auth/', include('authentication.urls')),` pada file `django_tutorial/urls.py`.

12. Lakukan `add`-`commit`-`push` dan lakukan _redeploy_ aplikasi PaaS pilihan kamu.

Fungsi _view_ ini akan mengatur _cookies_ ke pengguna dan membolehkan _requests_ yang terautentikasi dengan `@login_required` _decorator_.

Ikuti langkah-langkah berikut untuk melakukan integrasi sistem autentikasi pada **Flutter**.

1. Untuk menggunakan _package_ nya, kamu perlu memodifikasi _root widget_ untuk menyediakan `CookieRequest` _library_ ke semua _child widgets_ dengan menggunakan `Provider`.

    Sebagai contoh, jika aplikasimu sebelumnya seperti ini:

    ```dart
    class MyApp extends StatelessWidget {
        const MyApp({Key? key}) : super(key: key);
        
        @override
        Widget build(BuildContext context) {
            return MaterialApp(
                title: 'Flutter App',
                theme: ThemeData(
                    primarySwatch: Colors.blue,
                ),
                home: const LoginPage(),
            );
        }
    }
    ```

    Ubahlah menjadi:

    ```dart
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
                        primarySwatch: Colors.blue,
                    ),
                    home: const LoginPage(),
                ),
            );
        }
    }
    ```

    Hal ini akan membuat objek `Provider` baru yang akan membagikan _instance_ `CookieRequest` dengan semua komponen yang ada di aplikasi.

2. Buatlah _file_ baru pada folder `pages` dengan nama `login.dart`.

3. Impor _library_ `Provider` dan package `pbp_django_auth` ke komponen pada `main.dart` dan `pages/login.dart`.

    ```dart
    import 'package:provider/provider.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    ...
    ```

4. Isilah _file_ `login.dart` dengan kode berikut.

    ```dart
    import 'package:app_one/pages/menu.dart';
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
                                    final response = await request.login("https://<APP_URL_KAMU>/auth/login/", {
                                    'username': username,
                                    'password': password,
                                    });
                        
                                    if (request.loggedIn) {
                                        String message = response['message'];
                                        String uname = response['username'];
                                        Navigator.pushReplacement(
                                            context,
                                            MaterialPageRoute(builder: (context) => const MyHomePage()),
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

5. Pastikan kamu sudah memiliki akun pada situs web yang sudah di-_deploy_ di PaaS alternatif pilihan kamu.

6. Jalankan aplikasi Flutter kamu dan cobalah untuk login.

---

## Tutorial: Membuat Model Kustom

Dalam membuat model yang menyesuaikan dengan data JSON, kita dapat memanfaatkan website [Quicktype](https://app.quicktype.io/) dengan tahapan sebagai berikut.

1. Bukalah _endpoint_ `JSON` yang sudah kamu buat sebelumnya pada tutorial 2.

2. Salinlah data `JSON` dan buka situs web [Quicktype](https://app.quicktype.io/).

3. Pada situs web Quicktype, ubahlah _setup name_ menjadi `TransactionRecord`, _source type_ menjadi `JSON`, dan _language_ menjadi `Dart`.

4. Tempel data JSON yang telah disalin sebelumnya ke dalam _textbox_ yang tersedia pada Quicktype.

    Berikut adalah contoh hasilnya.

    ![Quicktype Example](https://i.ibb.co/8jFbD27/Contoh-Model.png)

5. Klik pilihan `Copy Code` pada Quicktype.

Setelah mendapatkan kode model melalui Quicktype, buka kembali proyek Flutter dan lakukan langkah-langkah berikut.

1. Buatlah file baru pada folder `lib/model` dengan nama `transaction_record.dart`.

2. Tempel kode yang telah disalin sebelumnya ke file `transaction_record.dart`.

---

## Tutorial: Menambahkan Dependensi HTTP

Untuk melakukan perintah _HTTP request_, kita membutuhkan _package_ tambahan yakni _package_ [http](https://pub.dev/packages/http).

1. Lakukan `flutter pub add http` pada terminal proyek Flutter untuk menambahkan _package_ `http`.

2. Pada file `android/app/src/main/AndroidManifest.xml`, tambahkan kode berikut untuk memperbolehkan akses Internet pada aplikasi Flutter yang sedang dibuat.

    ```xml
    ...
        <application>
        ...
        </application>
        <!-- Required to fetch data from the Internet. -->
        <uses-permission android:name="android.permission.INTERNET" />
    ...
    ```

---

## Tutorial: Mengambil, Mengolah, dan Menampilkan Data dari *Web Service*

1. Buatlah file baru pada folder `lib/pages` dengan nama `transaction.dart`.

2. Pada file `transaction.dart`, impor *library* yang dibutuhkan. Ubahlah <APP_NAME> sesuai dengan nama proyek Flutter yang kalian buat.

    ```dart
    import 'package:http/http.dart' as http;
    import 'dart:convert' as convert;
    import 'package:<APP_NAME>/model/transaction_record.dart';
    ...
    ```

3. Salinlah potongan kode berikut pada `pages/transaction.dart`.

    ```dart
    ...
    import 'package:<APP_NAME>/widgets/drawer.dart';

    class TransactionPage extends StatefulWidget {
    const TransactionPage({Key? key}) : super(key: key);

    @override
    _TransactionPageState createState() => _TransactionPageState();
    }

    class _TransactionPageState extends State<TransactionPage> {
    Future<List<TransactionRecord>> fetchTransactionRecord() async {
        // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
        var url = Uri.parse(
            'https://<URL_APP_KAMU>/tracker/json/');
        var response = await http.get(
            url,
            headers: {"Content-Type": "application/json"},
        );

        // melakukan decode response menjadi bentuk json
        var data = jsonDecode(utf8.decode(response.bodyBytes));

        // melakukan konversi data json menjadi object TransactionRecord
        List<TransactionRecord> listTransactionRecord = [];
        for (var d in data) {
            if (d != null) {
                listTransactionRecord.add(TransactionRecord.fromJson(d));
            }
        }
        return listTransactionRecord;
    }

    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
            title: const Text('Transaksi'),
            ),
            drawer: const DrawerMenu(),
            body: FutureBuilder(
                future: fetchTransactionRecord(),
                builder: (context, AsyncSnapshot snapshot) {
                    if (snapshot.data == null) {
                        return const Center(child: CircularProgressIndicator());
                    } else {
                        if (!snapshot.hasData) {
                        return Column(
                            children: const [
                            Text(
                                "Tidak ada data transaksi.",
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
                                    decoration: BoxDecoration(
                                        color: Colors.white,
                                        borderRadius: BorderRadius.circular(15.0),
                                        boxShadow: [
                                        BoxShadow(
                                            color:
                                                snapshot.data![index].fields.type ==
                                                        "Pemasukan"
                                                    ? Colors.blueAccent
                                                    : Colors.red,
                                            blurRadius: 2.0)
                                        ]),
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
                                        Text("${snapshot.data![index].fields.amount}"),
                                    ],
                                    ),
                                ));
                        }
                    }
                }));
        }
    }

    ```

4. Tambahkan halaman `transaction.dart` ke `widget/drawer.dart` dengan menambahkan kode berikut.

    ```dart
    // Kode ListTile Menu
    ...
    ListTile(
        title: const Text('Riwayat Transaksi'),
        onTap: () {
            // Route menu ke halaman transaksi
            Navigator.pushReplacement(
            context,
            MaterialPageRoute(builder: (context) => const TransactionPage()),
            );
        },
    ),
    ...
    ```

5. Ubah fungsi tombol `Riwayat Transaksi` pada `lib/pages/menu.dart` agar mengarahkan ke halaman `TransactionPage`. Kamu dapat melakukan _redirection_ dengan menambahkan kode berikut pada bagian `onTap: () { }` yang ada pada `Container` tombol `Riwayat Transaksi`.

    ```dart
    onTap: () {
        Navigator.pushReplacement(
            context,
            MaterialPageRoute(
                builder: (context) => const TransactionPage()),
        );
    },
    ```

6. Impor _file_ yang dibutuhkan saat menambahkan `TransactionPage` ke `drawer.dart` dan `menu.dart`.

7. Jalankan aplikasi dan cobalah untuk menambahkan beberapa transaksi di situs web kamu. Kemudian, coba lihat riwayat transaksi yang sudah kamu buat sebelumnya di situs web pada halaman Riwayat Transaksi di aplikasi Flutter.

---

## Tutorial: Integrasi Layanan Form Django dengan Aplikasi Flutter

Langkah-langkah berikut akan dilakukan pada kode proyek Django.

1. Buatlah sebuah fungsi _view_ baru pada `money_tracker/views.py` aplikasi Django kamu dengan potongan kode berikut.

    ```python
    @csrf_exempt
    def create_transaction_flutter(request):
        if request.method == 'POST':
            
            data = json.loads(request.body)

            new_transaction = TransactionRecord.objects.create(
                name = data["name"],
                type = data["type"],
                amount = int(data["amount"]),
                description = data["description"]
            )

            new_transaction.save()

            return JsonResponse({"status": "success"}, status=200)
        else:
            return JsonResponse({"status": "error"}, status=401)
    ```

2. Tambahkan _path_ baru pada `money_tracker/urls.py` dengan kode berikut.

    ```python
    path('create-flutter/', create_transaction_flutter, name='create_transaction_flutter'),
    ```

3. _Deploy_ ulang aplikasi kamu.

    > Catatan: Data akun dan transaksi akan hilang setelah di-_redeploy_.

Langkah-langkah berikut akan dilakukan pada kode proyek Flutter.

1. Bukalah `lib/pages/form.dart` dan ubahlah tipe data variabel `jumlahTransaksi` dari `double` menjadi `int`.

    ```dart
    ...
    int jumlahTransaksi = 0;
    ...
    ```

    > Catatan: Lakukan _quick fix_ pada baris-baris yang bermasalah.

2. Hubungkan halaman `form.dart` dengan `CookieRequest` dengan menambahkan baris kode berikut.

    ```dart
    ...
    @override
    Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();

        return Scaffold(
    ...
    ```

3. Ubahlah perintah pada `onPressed: ()` _button_ tambah menjadi kode berikut.

    ```dart
    ...
    onPressed: () async {
        if (_formKey.currentState!.validate()) {
            // Kirim ke Django dan tunggu respons
            // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
            final response = await request.postJson(
            "https://<URL_APP_KAMU>/tracker/create-flutter/",
            convert.jsonEncode(<String, String>{
                'name': _namaTransaksi,
                'type': tipeTransaksi,
                'amount': jumlahTransaksi.toString(),
                'description': _deskripsiTransaksi
            }));
            if (response['status'] == 'success') {
                ScaffoldMessenger.of(context)
                    .showSnackBar(const SnackBar(
                content: Text("Transaksi baru berhasil disimpan!"),
                ));
                Navigator.pushReplacement(
                    context,
                    MaterialPageRoute(builder: (context) => const TransactionPage()),
                );
            } else {
                ScaffoldMessenger.of(context)
                    .showSnackBar(const SnackBar(
                    content:
                        Text("Terdapat kesalahan, silakan coba lagi."),
                ));
            }
        }
    },
    ...
    ```

4. Lakukan _quick fix_ pada baris-baris yang bermasalah untuk mengimpor _file_ yang dibutuhkan.

5. Jalankan ulang aplikasi dan coba untuk menambahkan transaksi baru dari aplikasi Flutter kamu.

---

## Tutorial: Integrasi Fitur *Logout* Django dengan Aplikasi Flutter

Langkah-langkah berikut akan dilakukan pada kode proyek Django.

1. Buatlah sebuah metode _view_ untuk logout pada `authentication/views.py`.

    ```python
    @csrf_exempt
    def logout(request):
        username = request.user.username

        try:
            auth_logout(request)
            return JsonResponse({
                "username": username,
                "status": True,
                "message": "Logout berhasil!"
            }, status=200)
        except:
            return JsonResponse({
            "status": False,
            "message": "Logout gagal."
            }, status=401)
    ```

2. Tambahkan _path_ baru pada `authentication/urls.py` dengan kode berikut.

    ```python
    path('logout/', logout, name='logout'),
    ```

3. _Deploy_ ulang aplikasi kamu.

    > Catatan: Data akun dan transaksi akan hilang setelah di-_redeploy_.

Langkah-langkah berikut akan dilakukan pada kode proyek Flutter.

1. Ubahlah perintah `onTap: ()` pada `Container` logout di `pages/menu.dart` menjadi kode berikut.

    ```dart
    ...
    onTap: () async {
        final response = await request.logout(
            // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
            "https://<URL_APP_KAMU>/auth/logout/");
            String message = response["message"];
            if (response['status']) {
                String uname = response["username"];
                ScaffoldMessenger.of(context).showSnackBar( SnackBar(
                    content: Text("$message Sampai jumpa, $uname."),
                ));
                Navigator.pushReplacement(
                    context,
                    MaterialPageRoute(builder: (context) => const LoginPage()),
                );
            } else {
                ScaffoldMessenger.of(context).showSnackBar( SnackBar(
                content: Text("$message"),
            ));
        }
    },
    ...
    ```

2. Jalankan ulang aplikasi dan coba untuk lakukan logout.

---

## Akhir Kata

Pertama-tama, tim pengajar ingin mengucapkan apresiasi kepada semua mahasiswa yang telah berpartisipasi dan berkontribusi dalam mata kuliah ini. Tim pengajar melihat usaha dan dedikasi yang telah kalian tunjukkan dalam menghadapi tantangan pengembangan aplikasi multiplatform pada mata kuliah ini.

Selama proses lab dan tugas, kita telah menggali konsep dan prinsip dasar yang mendasari pengembangan aplikasi web dan *mobile* menggunakan Django dan Flutter. Kalian telah mempelajari tentang arsitektur, fitur, dan alat yang dapat membantu dalam membangun aplikasi yang tangguh dan responsif di kedua platform ini.

Tim pengajar berharap lab dan tugas yang diberikan dapat memberikan pemahaman yang lebih mendalam tentang potensi dan tantangan dalam pengembangan aplikasi multiplatform serta memberikan kalian keterampilan yang berguna dan dapat diterapkan dalam karir kalian sebagai pengembang perangkat lunak.

Namun, pembelajaran tidak berhenti di sini. Dunia pengembangan terus berkembang dengan cepat, dan penting untuk tetap mengikuti perkembangan terbaru dalam industri ini. Tim pengajar mendorong kalian untuk terus belajar dan menjaga keterampilan kalian tetap relevan dengan membaca referensi lainnya, mengikuti kursus lanjutan, dan mengambil bagian dalam proyek-proyek nyata.

Akhir kata, ingatlah bahwa pengembangan aplikasi multiplatform adalah bidang yang menarik dan penuh potensi. Teruslah eksplorasi dan berinovasi, dan tim pengajar yakin kalian memiliki masa depan yang cerah sebagai pengembang perangkat lunak. Terima kasih dan semoga sukses dalam perjalanan kalian!

<h2 align="center">
  <b>Buona fortuna!</b>
</h2>

---

## Referensi Tambahan

- [Fetch Data From the Internet](https://docs.flutter.dev/cookbook/networking/fetch-data)
- [How to create models in Flutter Dart](https://thegrowingdeveloper.org/coding-blog/how-to-create-models-in-flutter-dart)
- [Simple app state management | Flutter](https://docs.flutter.dev/development/data-and-backend/state-mgmt/simple)
- [Flutter State Management with Provider](https://blog.devgenius.io/flutter-state-management-with-provider-5a57eca108f1)
- [Pengenalan State Management Flutter dan Jenis-jenisnya](https://caraguna.com/pengenalan-state-management-flutter/)

---

## Credits

Tutorial ini dikembangkan berdasarkan [PBP Ganjil 2023](https://github.com/pbp-fasilkom-ui/ganjil-2023) yang ditulis oleh Tim Pengajar Pemrograman Berbasis Platform 2023. Segala tutorial serta instruksi yang dicantumkan pada repositori ini dirancang sedemikian rupa sehingga mahasiswa yang sedang mengambil mata kuliah Pemrograman Berbasis Platform dapat menyelesaikan tutorial saat sesi lab berlangsung.
