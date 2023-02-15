# Lab 1: Dasar-Dasar Git dan Django

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer Universitas Indonesia, Semester Genap 2022/2023

---

## Tujuan Pembelajaran

Setelah menyelesaikan tutorial ini, mahasiswa diharapkan untuk dapat:

- Mengerti perintah-perintah dasar `git` yang perlu diketahui untuk mengerjakan proyek aplikasi.
- Menggunakan perintah-perintah dasar `git` yang perlu diketahui untuk mengerjakan proyek aplikasi.
- Membuat repositori `git` lokal dan daring (GitHub).
- Menambahkan remote antara repositori `git` lokal dan pasangannya pada GitHub.
- Memahami _branching_ pada `git` dan mampu melakukan _merge request/pull request_.
- Mengerti konfigurasi _routing_ yang ada pada `urls.py`.
- Memahami kaitan _models_, _views_ dan _template_ pada Django.
- Memahami sintaks dasar untuk melakukan _mapping_ data ke templat HTML.
- Melakukan _deployment_ aplikasi Django pada Railway.

---

## Pengenalan git

Dalam kehidupanmu sebagai mahasiswa Ilmu Komputer atau Sistem Informasi, kamu mungkin pernah menggunakan sebuah **version control system**. Salah satu yang mungkin kamu pakai adalah fitur _undo_ pada _text editor_. Ketika kamu membuat suatu kesalahan, kamu bisa mengembalikan kesalahanmu ke waktu sebelum kamu membuat kesalahan dengan fitur _undo_ tersebut. Contoh lain adalah ketika kamu mengerjakan dokumen secara kolaboratif di Google Drive, kamu bisa melihat setiap perubahan yang dilakukan di dokumen tersebut dan kamu bisa mengembalikan ke perubahan sebelumnya.

Pada tutorial ini, kamu akan mempelajari sebuah _version control system_ bernama [git](https://git-scm.com). `git` merupakan sebuah _version control system_ yang umum digunakan untuk melacak perubahan pada artefak-artefak perangkat lunak seperti _source code_, halaman HTML, atau _stylesheet_. `git` akan mencatat perubahan-perubahan yang terjadi pada pekerjaan kamu sebagai sebuah rangkaian _**commit**_ yang tersusun dari _commit_ terlama hingga _commit_ yang terbaru. Perubahan tersebut seperti sebuah _graph_ yang mana node merepresentasikan sebuah _commit_ dan _directed edge(s)_ merepresentasikan hubungan antara suatu _commit_ dengan _commit_ sebelumnya.

> Jangan khawatir jika kamu masih asing dengan terminologi seperti: _node_, _edge_, dan
> _graph_. Kamu akan mempelajarinya lebih lanjut dalam mata kuliah Struktur Data &
> Algoritma dan Matematika Diskret.

Sebelum melakukan tutorial ini dan tutorial-tutorial selanjutnya, pastikan kamu telah
memasang _tools_ berikut:

- [git](https://git-scm.com/downloads)
- [Python (Latest Version)](https://www.python.org/downloads/)
- _Text editor_ atau IDE yang baik, seperti
  [Vim](http://www.vim.org/download.php),
  [Visual Studio Code](https://code.visualstudio.com/),
  [Sublime](https://www.sublimetext.com/), atau
  [PyCharm](https://www.jetbrains.com/pycharm/).

Untuk meringkas dokumen tutorial ini, cara penginstalan dan konfigurasi masing-masing
perlengkapan dapat dilihat melalui tautan diatas.

---

## Tutorial: Basic git dan GitHub

1. Bukalah _command prompt_ atau _shell_ favoritmu. Jika kamu menggunakan Windows, gunakan `git Bash` atau `cmd` (hanya berlaku jika kamu telah menambahkan path ke _folder executable_ `git` ke PATH di _environment variable_). Jika kamu menggunakan OS berbasis Unix (Linux atau Mac OS), kamu bisa menggunakan _shell_ yang tersedia pada OS-mu, seperti [bash](https://www.gnu.org/software/bash/).

    > Walaupun kamu bisa menggunakan aplikasi GUI seperti built-in GUI git,
    > [gitKraken](https://www.gitkraken.com), atau
    > [SourceTree](https://www.sourcetree.com), **kami merekomendasikan untuk
    > menggunakan perintah melalui _shell_**. _Shell_ merupakan salah satu tools
    > yang paling umum digunakan saat pengembangan Web, terutama saat kamu harus
    > men-deploy aplikasi web kamu ke _remote server_. Akan sangat berguna jika
    > kamu mengetahui perintah _shell_ dan git ketika GUI tidak dapat diakses.
    > Mengeksekusi perintah melalui _shell_ juga **lebih cepat** dibandingkan
    > menggunakan GUI.

2. Ubah direktori ke _folder_ yang akan kamu gunakan untuk menyimpan pekerjaanmu. Gunakan perintah `cd` untuk melakukan navigasi ke direktori yang kamu inginkan.

3. Buat _folder_ baru untuk menyimpan file yang berhubungan dengan tutorial ini. Cobalah untuk membuat _folder_ bernama `django_exercise` dan ubah direktori (`cd`) ke _folder_ tersebut.

4. Dalam direktori tersebut, ketik `git init` untuk membuat repositori `git` kosong.

5. Cobalah untuk mengeksekusi perintah `git status` untuk melihat status dari repositori kamu ketika perintah tersebut dijalankan.

Saat ini, kamu telah berhasil membuat respositori `git` lokal pertamamu. Sebelum melanjutkan tutorial, ada beberapa konfigurasi yang harus kamu lakukan ke repositori `git` lokalmu:

1. Atur _username_ dan _email_ yang akan diasosiasikan dengan pekerjaanmu ke repositori `git` ini.

    ```bash
    git config user.name "<NAME>"
    git config user.email "<EMAIL>"
    ```

    Contoh:

    ```bash
    git config user.name "P. Bepe"
    git config user.email "p.bepe@ui.ac.id"
    ```

2. Jika kamu ada dalam sebuah proxy (contoh: menggunakan PC di lab Fasilkom), kamu harus mengatur HTTP _proxy_ pada konfigurasi `git`.

    ```bash
    git config http.proxy <PROXYHOST>:<PORT>
    ```

    Contoh (Jika kamu menggunakan PC di lab Fasilkom):

    ```bash
    git config http.proxy 152.118.24.10:8080
    ```

3. Jika kamu ingin mengatur konfigurasi secara global (untuk setiap repositori lokal), tambahkan _flag_ `--global` pada pemanggilan `git config`.

4. Jika kamu ingin mengetahui konfigurasi yang diatur ke repositori lokalmu, kamu bisa menggunakan perintah berikut.

    ```bash
    git config --list --local
    ```

Setelah mengatur repositori `git`, silakan melanjutkan ke instruksi tutorial.

1. Buat file baru dengan nama `README.md` dalam direktori yang kamu inisiasi dengan repositori `git` dan tulis nama, NPM, dan kelas pada baris **pertama**, **ketiga**,  dan **kelima** pada file `README.md` tersebut.

    Contoh:

    ```markdown
    Nama    : P. Bepe

    NPM     : 2106123456

    Kelas   : Z
    ```

2. Eksekusi perintah `git status` dalam _bash_. Perhatikan bahwa terdapat _untracked file_ bernama `README.md`. Ini menandakan bahwa ada file yang belum di-_track_ oleh `git`.

3. Beritahu `git` untuk men-_track_ perubahan yang ada pada `README.md`.

    ```bash
    git add README.md
    ```

4. Eksekusi perintah `git status` lagi. Pesan status akan berubah dari eksekusi sebelumnya. Sekarang file tersebut masuk pada bagian _Changes to be committed_. Ini menandakan file tersebut akan di-_track_ oleh `git` pada _commit_ selanjutnya.

    > Walaupun kamu sudah mengeksekusi perintah `git add`, file `README.md` belum sepenuhnya di-_track_ oleh git. `git add` hanya memberi tahu git untuk memasukan perubahan dari file tersebut ke dalam _staging area_.

5. Untuk menyimpan perubahan secara permanen ke dalam `git`, eksekusi perintah `git commit`. _Text editor_ akan muncul untuk mengetikkan pesan yang menggambarkan _commit_ yang telah kamu buat dan akan disimpan pada riwayat `git`.

    > Sebuah _commit_ dapat berarti perubahan yang kamu lakukan pada repositori lokal. Perubahan tersebut dapat berupa penambahan, perubahan dalam file, atau penghapusan satu atau lebih file.

6. Setelah kamu selesai menulis pesan _commit_, simpan dan keluar dari _text editor_ yang kamu gunakan untuk menulis pesan. Semua perubahan akan disimpan sebagai _commit_ dan akan disimpan dalam riwayat `git`.

Kamu baru saja membuat repositori `git` lokal dan mulai memantau perubahan dari suatu file yang ada pada repositori. Jika kamu ingin membagikan hasil pekerjaanmu dengan tutor atau dengan tim kamu, kamu harus mengatur repositori tersebut agar dapat diakses melalui Internet. Untuk melakukan ini, kamu harus menaruh salinan dari repositori lokalmu ke repositori `git` daring seperti [GitHub](https://github.com).

1. Bukalah [GitHub](https://github.com) menggunakan _web browser_ favoritmu.

2. Buatlah akun baru atau akun yang kamu punya jika kamu telah melakukan registrasi sebelum mengikuti tutorial ini.

3. Buat repositori baru bernama **Django Tutorial** dan buka laman repositori. Pastikan kamu mengatur _project visibility_ menjadi **public**.

4. Cari dan klik tombol **clone** pada laman repositorimu. Perhatikan bahwa terdapat dua tipe cara untuk meng-_clone_ repositori, yaitu dengan menggunakan **HTTPS** dan **SSH**. Salin URL yang menggunakan **HTTPS**.

5. Perbarui repositori `git` lokalmu agar semua _commit_ dapat disimpan di repositori GitHub-mu. Gunakan perintah `git remote add origin <URL_REPOSITORY>` dan gunakan URL yang tadi kamu salin sebagai argumen dari perintah tersebut.

    ```bash
    git remote add origin <URL_REPOSITORY>
    ```

    Contoh:

    ```bash
    git remote add origin https://github.com/adrianholovaty/my-first-repo.git
    ```

    > `git remote add origin` akan memberi tahu repositori lokal untuk menambahkan _path_ bernama **origin** yang menunjuk ke URL yang diberikan. Dengan begitu, kamu dapat menyimpan semua _commit_ yang kamu buat ke repositori daring menggunakan perintah `git push`.

6. Untuk menyimpan semua _commit_ ke repositori daring di GitHub, eksekusi perintah `git push`. Kamu juga harus menambahkan nama **remote** dan **branch** yang akan diunggah (atau di-_push_).

    ```bash
    git push -u <REMOTE_NAME> <DEFAULT_BRANCH>
    ```

    Contoh:

    ```bash
    git push -u origin main
    ```

    > `git push` akan memerintah git untuk mengunggah semua _commit_ yang ada di _branch_ lokal `main` ke repositori yang ditunjuk oleh _remote_ `origin`. flag `-u` akan memastikan pemanggilan `git push` saat _branch_ `main` aktif akan di kirim ke _branch_ `main` di `origin`.  

7. Perhatikan laman repositori GitHub kamu. Kamu akan melihat file kamu berhasil disimpan dan dapat diakses di GitHub.

Kamu juga bisa unduh (**_clone_**) repositori `git` lainnya ke komputermu. Cobalah untuk membuat salinan dari repositori di GitHub pada direktori yang berbeda dalam komputermu.

1. Bukalah laman repositori kamu di GitHub.

2. Salin URL _clone_ dengan **HTTPS**.

3. Bukalah _command prompt_ atau _shell_ dan navigasi ke direktori berbeda di luar direktori repositori lokal yang telah kamu buat sebelumnya.

4. Eksekusi perintah `git clone <URL>` dengan keterangan `<URL>` adalah URL repositori yang akan di-_clone_.

5. Perhatikan bahwa nama direktori baru yang telah dibuat sama dengan nama dari repositorimu.

Pada tahap ini, kamu sebenarnya sudah punya 3 repositori: (1) orisinil, repositori lokal, (2) repositori daring di GitHub yang telah terkoneksi dengan repositori pertama, dan (3) repositori lainnya yang kamu _clone_ dari repositori (2). Sekarang coba tambahkan _commit_ baru di repositori (1), _push_ ke repositori (2), dan unduh (istilah `git`: **pull**) ke repositori (3).

1. Bukalah direktori repositori lokal yang kamu insiasi sebelumnya untuk pertama kalinya.

2. Ubah file `README.md` dengan menambahkan _string_ yang mendeskripsikan hobi kamu pada baris ketujuh.

    Contoh:

    ```markdown
    Nama    : P. Bepe

    NPM     : 2106123456

    Kelas   : Z

    Hobi    : Tidur
    ```

3. Simpan file tersebut dan tambahkan ke repositori `git` lokal.

4. _Commit_ file tersebut dan _push_ ke GitHub.

5. Cek laman repositori GitHub kamu. Pastikan `README.md` sudah ter-_update_. Kamu bisa membandingkannya dengan versi sebelumnya dengan mengecek _diff_ antara _commit_ terakhir dengan _commit_ sebelumnya.

6. Bukalah direktori repositori lokal hasil _clone_ repositori dari GitHub.

7. _Update_ repositori tersebut dengan mengeksekusi perintah `git pull origin main`.

8. Cek repositori yang kamu _clone_. Kamu dapat melihat bahwa file `README.md` juga telah ter-_update_.

Selamat! Anda setidaknya telah mengetahui perintah `git` dasar yang dapat kamu gunakan untuk mengelola pekerjaanmu di `git` dan GitHub. Kamu mungkin bertanya mengapa kita perlu bersusah-susah melakukan skilus _add-commit-push-pull_ ini? Mengapa kita tidak gunakan Dropbox atau Google Drive saja?

Benar bahwa Dropbox, Google Drive, atau layanan _cloud storage_ lainnya lebih mudah digunakan. Namun, _tools_ tersebut digunakan untuk hal yang lebih umum. _Tools_ tersebut tidak dibuat secara spesifik untuk mengatasi perubahan terhadap artefak-artefak perangkat lunak, khususnya ketika ada perubahan yang dilakukan secara **bersamaan** dan melibatkan banyak pihak. `git`, sebagai _version control system_, dapat memastikan integritas dari semua perubahan ketika ada beberapa pihak yang bekerja secara bersamaan dalam satu repositori. Kamu akan belajar lebih lanjut mengenai cara menggunakan _version control system_ di lingkup keja tim selanjutnya di mata kuliah ini dan mata kuliah selanjutnya (IK: Pemrograman Lanjut, SI: Arsitektur dan Pemrograman Aplikasi Perusahaan).

---

## Tutorial: Branch dan Merge

Setelah mempelajari beberapa dasar dari `git`, kamu akan mulai mempelajari beberapa konsep lanjutan dari `git`. Pada pengembangan aplikasi, kita sebagai _developer_ akan lebih banyak bekerja sama dengan orang lain sebagai tim. Beruntungnya, `git` memiliki fitur untuk mengakomodasi kolaborasi antar developer. Beberapa fitur yang dimaksud adalah _branch_ dan _merge_.

Secara sederhana, _branch_ adalah fitur `git` yang memungkinkan sebuah _source code_ yang disimpan pada `git` memiliki versi lain atau biasanya cabang yang berisikan perubahan-perubahan sesuai dengan kebutuhan dan _developer_ yang mengembangkannya. Umumnya setelah kita melakukan `git push`, perubahan yang kita simpan akan masuk ke dalam cabang yang dituju oleh kita. Kegunaan _branch_ ini adalah untuk menghindari tabrakan, konflik serta _race condition_ dalam hal melakukan perubahan ketika sedang dalam pengembangan.

Adapun _merge_ adalah fitur `git` yang digunakan untuk menggabungkan suatu perubahan yang telah disimpan dalam satu _branch_ ke dalam _branch_ target. Pada saat melakukan `git merge`, kejadian _merge conflict_ dapat terjadi. _Merge conflict_ adalah sebuah konflik yang terjadi apabila terdapat perubahan pada file yang sama dalam dua _branch_ berbeda atau ketika satu file telah dihapus pada _branch_ pertama, namun berkas tersebut ada dan mengalami perubahan pada _branch_ kedua. Untuk menyelesaikan _merge conflict_, biasanya _developer_ dapat menggunakan GUI yang telah disiapkan oleh `git` pada GitHub. Namun apabila platform tersebut sedang tidak dapat mengakomodasi proses _merge conflict_, biasanya _developer_ akan diminta untuk menyelesaikannya di repositori lokal mereka.

Sekarang kita akan mencoba untuk menerapkan konsep _branch_ dan _merge_.

1. Pada direktori `git` lokal yang telah kita kerjakan pada tutorial sebelumnya, buatlah sebuah _branch_ baru di repositori tersebut.

    ```bash
    git checkout -b <NAMA_BRANCH>
    ```

    Contoh:

    ```bash
    git checkout -b second
    ```

    > Sekarang, sebuah branch baru telah dibuat. Kamu bisa melihat branch apa saja yang ada di repositori lokal dengan command `git branch`. Untuk melakukan _switching_ ke branch lain, kamu dapat langsung melakukannya dengan perintah `git checkout <NAMA_BRANCH>`.

2. Buatlah sebuah perubahan pada file README.md dengan mengubah hobi kamu di baris ketujuh ke hobi lain.

    Contoh:

    ```markdown
    Nama    : P. Bepe

    NPM     : 2106123456

    Kelas   : Z

    Hobi    : Usil
    ```

3. Simpan file tersebut dan tambahkan ke repositori `git` lokal.

4. _Commit_ file tersebut dan _push_ ke GitHub.

5. Cek laman repositori GitHub kamu. Pada pilihan branch yang ada di repositori kamu, sekarang kamu dapat melihat terdapat branch baru yang baru saja kamu buat.

6. Sekarang _merge_ atau gabungkan _branch_ baru tersebut ke branch utama dari repositori. Kamu dapat melakukannya dengan memilih tab `pull request` pada halaman repositori kamu di GitHub dan memilih opsi `new pull request`.

7. Pilihlah _branch_ main sebagai base dan _branch_ baru kamu sebagai _compare_. Setelah memilih _branch_ tersebut, kamu dapat melihat perbedaan antara dua branch yang akan digabungkan. Pilihlah `create pull request` untuk menggabungkan kedua _branch_ tersebut.

8. Setelah itu, kamu akan masuk ke sebuah halaman form untuk mengisi informasi tentang _pull request_ yang akan kamu lakukan. Kamu dapat mengisi deskripsi tentang _pull request_ serta mengubah judul dari _pull request_. Untuk saat ini diamkan saja dulu dan langsung pilihlah `create pull request`.

9. GitHub akan secara otomatis melakukan cek dan membandingkan antara kedua _branch_ yang ingin digabungkan. Apabila tidak ada konflik, kamu bisa langsung memilih `merge pull request`.

10. Sekarang kedua _branch_ telah tergabung. Kamu bisa melihat perubahan yang kamu lakukan di branch baru telah tersimpan atau tergabung dalam _branch_ main.

---

## Tutorial: Membuat Proyek dan Aplikasi Django beserta Konfigurasi Model

1. Di dalam direktori `django_exercise`, bukalah _command prompt_ atau _shell_ dan buatlah sebuah _virtual environment_. _Virtual environment_ ini berguna untuk mengisolasi _package_ serta _dependencies_ dari aplikasi sehingga tidak bertabrakan dengan versi lain yang ada pada komputermu. Kamu dapat membuat _virtual environment_ dengan perintah:

    ```bash
    python -m venv env
    ```

2. Nyalakan _virtual environment_ yang telah dibuat dengan perintah berikut. Pastikan saat ini kamu sedang berada pada direktori `django_exercise` yang telah dibuat sebelumnya. Perhatikan pula bahwa Windows dengan Unix memiliki perintah yang berbeda. Apabila virtual environment berhasil dinyalakan, kamu dapat melihat sebuah teks `(env)` di posisi paling kiri dari baris input _shell_ milikmu.

    ```bash
    Windows:
    env\Scripts\activate.bat
    ```

    ```bash
    Unix (Linux & Mac OS):
    source env/bin/activate
    ```

3. Buatlah file baru pada folder tersebut dengan nama `requirements.txt` dan tambahkan beberapa dependencies berikut ini yang dibutuhkan ke dalam file tersebut.

    ```txt
    asgiref==3.6.0
    certifi==2022.12.7
    charset-normalizer==3.0.1
    Django==4.1.6
    gunicorn==20.1.0
    idna==3.4
    psycopg2-binary==2.9.5
    requests==2.28.2
    sqlparse==0.4.3
    tzdata==2022.7
    urllib3==1.26.14
    whitenoise==6.3.0
    ```

4. Instal _dependencies_ yang diperlukan untuk menjalankan proyek Django dengan perintah perintah `pip install -r requirements.txt`.

5. Buatlah sebuah proyek Django baru bernama `django_tutorial` dengan perintah `django-admin startproject django_tutorial .`.

6. Eksekusi perintah `python manage.py runserver` di Windows atau `./manage.py runserver` di OS berbasis Unix untuk menjalankan aplikasi Django. Pastikan bahwa file `manage.py` ada pada direktori yang aktif pada _shell_ kamu saat ini.

7. Bukalah <http://localhost:8000> menggunakan _browser_ favoritmu untuk melihat aplikasi Django yang telah kamu buat. Kamu sekarang dapat melihat sebuah roket sedang meluncur di halaman tersebut. Selamat! Kamu telah berhasil membuat aplikasi Django dari awal.

8. Untuk mematikan server Django yang sedang berjalan, kamu dapat menggunakan tombol `Ctrl+C` pada Windows/Linux atau `Command+C` pada MacOS.

9. Selanjutnya, buatlah sebuah `django-app` bernama `money_tracker` dengan perintah `python manage.py startapp money_tracker`.

10. Buka `settings.py` di folder `django_tutorial` dan tambahkan aplikasi `money_tracker` ke dalam variabel `INSTALLED_APPS` untuk mendaftarkan `django-app` yang sudah kamu buat ke dalam proyek Django-mu. Contohnya adalah sebagai berikut.

    ```python
    INSTALLED_APPS = [
        ...,
        'money_tracker',
    ]
    ```

11. Buka file `models.py` yang ada di folder `money_tracker` dan tambahkan potongan kode berikut.

    ```python
    from django.db import models

    class TransactionRecord(models.Model):
        name = models.CharField(max_length=50)
        type = models.Charfield(max_length=20)
        amount = models.IntegerField()
        date = models.DateTimeField(auto_now_add=True)
        description = models.TextField()
    ```

12. Lakukan perintah `python manage.py makemigrations` untuk mempersiapkan migrasi skema model ke dalam _database_ Django lokal.

13. Jalankan perintah `python manage.py migrate` untuk menerapkan skema model yang telah dibuat ke dalam _database_ Django lokal.

---

## Tutorial: Implementasi Views Dasar

Sebelum kita mengimplemetasikan _views_, kita perlu membuat suatu _skeleton_ yang berfungsi sebagai kerangka _views_ dari situs web kita.

Buatlah folder `templates` pada _root folder_ (jika belum ada) dan buatlah sebuah file baru bernama `base.html`. Isilah file tersebut dengan kode berikut.

```html


{% load static %}
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="{% static 'css/style.css' %}">
  {% block meta %}
  {% endblock meta %}
</head>

<body>
  {% block content %}
  {% endblock content %}
</body>

</html>
```

Setelah membuat kerangka dasar HTML untuk situs web, maka kita baru dapat membuat _view_ baru tanpa perlu mendeklarasikan struktur dasar HTML dari awal.

1. Buka `views.py` yang ada pada folder `money_tracker` dan buatlah sebuah fungsi yang menerima parameter `request` dan mengembalikan `render(request, "tracker.html")`. Contohnya adalah sebagai berikut.

    ```python
    def show_tracker(request):
        return render(request, "money_tracker.html")

    ```

2. Buatlah sebuah folder bernama `templates` di dalam folder aplikasi `money_tracker` dan buatlah sebuah berkas bernama `tracker.html`. Isi dari `tracker.html` dapat kamu isi dengan template berikut.

    ```html
    {% extends 'base.html' %}

    {% block content %}
    <h5>Nama: </h5>
    <p>Fill me!</p>

    <table>
        <tr>
            <th>Nama</th>
            <th>Jenis</th>
            <th>Jumlah</th>
            <th>Tanggal</th>
            <th>Deskripsi</th>
        </tr>
        {% comment %} Tambahkan data di bawah baris ini {% endcomment %}
    </table>

    {% endblock content %}
    ```

3. Buatlah sebuah berkas di dalam folder aplikasi `money_tracker` bernama `urls.py` untuk melakukan _routing_ terhadap fungsi `views` yang telah kamu buat sehingga nantinya halaman HTML dapat ditampilkan lewat _browser_-mu. Isi dari `urls.py` tersebut adalah sebagai berikut.

    ```python
    from django.urls import path
    from money_tracker.views import show_tracker

    app_name = 'money_tracker'

    urlpatterns = [
        path('', show_tracker, name='show_tracker'),
    ]
    ```

4. Daftarkan juga aplikasi `money_tracker` ke dalam `urls.py` yang ada pada folder `django_tutorial` dengan menambahkan potongan kode berikut pada variabel `urlpatterns`.

    ```python
    ...
    path('tracker/', include('tracker.urls')),
    ...
    ```

5. Jalankan proyek Django-mu dengan perintah `python manage.py runserver` dan bukalah <http://localhost:8000/tracker/> di browser favoritmu untuk melihat halaman yang sudah kamu buat.

Apabila muncul sebuah halaman yang berisikan tabel _money tracker_, maka selamat! Kamu telah berhasil melakukan routing sebuah fungsi views yang dapat melakukan render sebuah halaman HTML. Akan tetapi seperti yang dapat kamu lihat, tidak ada data pada tabel _money tracker_ tersebut. Kamu juga dapat melihat tidak jelas milik siapa _money tracker_ tersebut sehingga kamu ingin menampilkan nama kamu ke dalam _money tracker_ tersebut. Sekarang, kamu akan mempelajari bagaimana menampilkan data ke dalam HTML dari _database_ Django lokal maupun data atau variabel yang kamu definisikan dalam berkas `views.py`.

---

## Tutorial: Menghubungkan Models dengan Views dan Template

1. Pada fungsi views yang telah kamu buat, import models yang sudah kamu buat sebelumnya ke dalam file views.py. Kamu akan menggunakan class tersebut untuk melakukan pengambilan data dari database. Contohnya adalah sebagai berikut.

    ```python
    from django.shortcuts import render
    from money_tracker.models import TransactionRecord
    ...
    ```

2. Tambahkan potongan kode di bawah ini ke dalam fungsi `show_tracker` yang sudah kamu buat sebelumnya. Potongan kode ini berfungsi untuk memanggil fungsi _query_ ke _model database_ dan menyimpan hasil _query_ tersebut ke dalam sebuah variabel.

    Sesuaikan isi variabel `name` dengan nama kalian, ya. 😉

    ```python
    transaction_data = TransactionRecord.objects.all()
    context = {
        'list_of_transactions': transaction_data,
        'name': 'Kak Athal'
    }
    ```

3. Tambahkan `context` sebagai parameter ketiga pada pengembalian fungsi _render_ di fungsi yang sudah kamu buat sebelumnya. Data yang ada pada variabel `context` tersebut akan ikut di-_render_ oleh Django sehingga nantinya kamu dapat memunculkan data tersebut pada halaman HTML.

    ```python
    return render(request, "tracker.html", context)
    ```

Sekarang, kamu akan belajar melakukan _mapping_ terhadap data yang telah ikut di-_render_ pada fungsi `views` untuk dapat memunculkannya di halaman HTML. Untuk melakukan _mapping_ tersebut, kamu dapat menggunakan sintaks khusus _template_ yang ada pada Django, yakni `{{data}}`. Apabila kamu tertarik untuk mengetahui lebih jauh tentang sintaks dari _template_ yang ada pada Django, kamu dapat membaca dan mempelajari lebih dalam di [dokumentasi _template tags_ Django](https://docs.djangoproject.com/en/4.1/ref/templates/builtins/).

1. Bukalah file HTML yang sudah kamu buat sebelumnya pada folder `templates` yang ada di dalam direktori `money_tracker`.

2. Ubah `Fill me!` yang ada di dalam HTML tag `<p>` menjadi `{{nama}}` untuk menampilkan nama kamu di halaman HTML. Contohnya adalah sebagai berikut.

    ```html
    ...
    <h5>Nama: </h5>
    <b>{{nama}}</b>
    ...
    ```

3. Untuk menampilkan daftar transaksi ke dalam tabel, kamu perlu melakukan iterasi terhadap variabel `list_of_transactions` yang telah kamu ikut _render_ ke dalam HTML. Perhatikan bahwa kamu tidak dapat memanggil daftar transaksi tersebut secara langsung seperti yang kamu lakukan pada langkah 2 sebab variabel `list_of_transactions` merupakan sebuah kontainer yang berisikan objek. Kamu juga perlu memanggil nama variabel/atribut spesifik dari objek yang ada dalam kontainer tersebut untuk memanggil data dari objek tersebut. Contohnya adalah sebagai berikut.

    ```html
    ...
    {% for transaction in list_of_transactions %}
        <tr>
            <td>{{transaction.name}}</td>
            <td>{{transaction.type}}</td>
            <td>{{transaction.amount}}</td>
            <td>{{transaction.date}}</td>
            <td>{{transaction.description}}</td>
        </tr>
    {% endfor %}
    ...
    ```

---

## Tutorial: Melakukan Deploy Aplikasi Django ke Railway

Sebelum kita melakukan _automated deployment_, kita perlu melakukan konfigurasi tambahan agar situs web yang kita buat dapat bekerja dengan baik.

1. Buatlah sebuah file bernama `Procfile` (tanpa ada ekstensi file) pada _root folder_ dan isilah file tersebut dengan kode berikut.

    ```procfile
    web: python manage.py migrate && gunicorn django_tutorial.wsgi
    ```

2. Bukalah file `settings.py` yang ada pada folder `django_tutorial`. Tambahkan baris kode berikut setelah bagian `DEBUG`.

    ```python
    ALLOWED_HOSTS = [f'{APP_NAME}.up.railway.app']
    CSRF_TRUSTED_ORIGINS = [f'https://{APP_NAME}.up.railway.app']
    ```

Setelah melakukan konfigurasi, silakan push proyek kamu ke GitHub dan lakukan hal-hal berikut.

1. Bukalah situs web [Railway](https://railway.app/), klik tombol `Login` di pojok kanan atas, dan pilih `GitHub` sebagai metode login.

    ![Railway Login](https://i.ibb.co/CsndvKz/Screenshot-2023-02-12-21-21-45.png)

2. Selesaikan proses registrasi sehingga kamu kembali ke halaman pembuatan proyek baru.

3. Klik pilihan `Deploy from GitHub repo` dan pilih repositori tempat kamu menaruh proyek Django kamu.

4. Buka proyek, klik kotak `web`, dan klik menu `Variables`. Buatlah variabel baru bernama `APP_NAME` dan isilah dengan nama situs web yang kamu ingin pakai.

5. Buka menu `Settings` dan ubah nama domain situs web kamu sesuai yang telah kamu buat sebelumnya.

6. Lakukan push ulang apabila Railway tidak melakukan _deployment_ ulang setelah kamu mengubah pengaturan.

Voila! Seharusnya situs web kamu dapat dibuka dan menghasilkan halaman yang telah kamu buat sebelumnya.

---

## Credits

Tutorial ini dikembangkan berdasarkan [PBP Ganjil 2023](https://github.com/pbp-fasilkom-ui/ganjil-2023) yang ditulis oleh Tim Pengajar Pemrograman Berbasis Platform 2023. Segala tutorial serta instruksi yang dicantumkan pada repositori ini dirancang sedemikian rupa sehingga mahasiswa yang sedang mengambil mata kuliah Pemrograman Berbasis Platform dapat menyelesaikan tutorial saat sesi lab berlangsung.
