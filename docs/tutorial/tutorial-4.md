# Tutorial 4: Metode Update dan Delete pada Data & Web Design Menggunakan HTML dan CSS3

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer Universitas Indonesia, Semester Genap 2022/2023

---

## Tujuan Pembelajaran

Setelah menyelesaikan tutorial ini, mahasiswa diharapkan untuk dapat:

- Memahami konsep _update_ dan _delete_
- Memahami cara _update_ dan _delete_ pada Django
- Memahami susunan tag pada HTML5
- Mengetahui berbagai jenis tag HTML5
- Memahami sintaks penulisan CSS
- Memahami konsep _static files_ pada Django
- Memahami penggunaan _selector_ pada CSS

## Pengenalan HTML

Silakan pelajari dan mencoba sendiri HTML pada referensi [ini](https://www.w3schools.com/html/default.asp).

Perbedaan antara HTML dan HTML5 bisa kamu baca pada referensi [ini](https://www.geeksforgeeks.org/difference-between-html-and-html5/).

## Pengenalan CSS

### Apa itu CSS?

Cascading Style Sheets (CSS) adalah bahasa yang digunakan untuk mendeskripsikan tampilan dan format dari sebuah situs web yang ditulis pada _markup language_ (seperti HTML). Kegunaannya menjadikan tampilan situs web lebih menarik.

Untuk mempelajari perbedaan antara CSS dan CSS3 bisa kamu baca pada referensi [ini](https://www.geeksforgeeks.org/difference-between-css-and-css3/).

### Cara Penulisan CSS

Secara umum, CSS dapat dituliskan dalam bentuk sebagai berikut.

```css
selector {
  properties: value;
}
```

Silakan pelajari dan mencoba sendiri CSS pada referensi [ini](https://www.w3schools.com/css/).

Terdapat tiga jenis cara penulisan CSS:

1. **Inline Styles**
2. **Internal Style Sheet**
3. **External Style Sheet**

Silakan pelajari tentang ketiga jenis CSS tersebut pada referensi [ini](https://www.geeksforgeeks.org/types-of-css-cascading-style-sheet/).

Perlu diperhatikan, jika kamu membuat jenis External Style Sheet, kamu perlu menambahkan tag `{% load staticfiles %}` pada halaman HTML kamu. Contohnya seperti potongan kode di bawah ini.

```html
{% load staticfiles %}
<html>
  <head>
    <title>Tutorial CSS Yay</title>
    <link rel="stylesheet" href="{% static 'css/tutorial.css' %}" />
  </head>
  <body>
    <div>
      <h1>Tutorial CSS Yay</h1>
    </div>
    <div id="main">
      <div>
        <p>published: 04 Oktober 2021</p>
        <h1><a href="">Tutorial CSS ku</a></h1>
        <p>Yay ini tutorial yang gampang!</p>
      </div>
    </div>
  </body>
</html>
```

Hal ini dapat terjadi karena CSS merupakan _static files_ di Django. _Static files_ akan dijelaskan pada bagian selanjutnya.

### Catatan Tambahan

Jika terdapat lebih dari satu _style_ yang didefinisikan untuk suatu elemen, maka _style_ yang akan diterapkan adalah yang memiliki prioritas yang lebih tinggi. Berikut ini urutan prioritasnya, nomor 1 yang memiliki prioritas paling tinggi.

1. Inline style
2. External dan internal style sheets
3. Browser default

## Static files pada Django

Pada _framework_ Django, terdapat file-file yang disebut dengan _static files_. _Static files_ merupakan file-file pendukung HTML pada suatu situs web. Contoh _static files_ antara lain seperti CSS, JavaScript dan gambar. Pengaturan untuk _static files_ terletak pada file `settings.py`.

```python
  ...
  # Static files (CSS, JavaScript, Images)
  # httpsdocs.djangoproject.comen1.9howtostatic-files
  STATIC_ROOT = os.path.join(PROJECT_ROOT, 'static')
  STATIC_URL = 'static'
  ...
```

Pada `settings.py`, terdapat `STATIC_ROOT` yang menentukan _absolute path_ ke direktori _static files_ ketika menjalankan perintah `collectstatic` pada proyek dan terdapat `STATIC_URL` yang merupakan URL yang dapat diakses publik untuk memperoleh _static files_ tersebut.

Perintah `collectstatic` adalah perintah untuk mengumpulkan _static files_ dari semua app sehingga mempermudah akses untuk semua app.

Penjelasan lebih lengkap mengenai _static files_ dapat kamu baca pada referensi [ini](https://docs.djangoproject.com/en/4.1/ref/contrib/staticfiles/).

## Selector pada CSS

Pada bagian ini kamu akan mempelajari 3 buah _selector_ pada CSS, yaitu _element selector_, _class selector_, dan _ID selector_.

1. Element Selector
  
    _Element selector_ menggunakan tag HTML sebagai _selector_ untuk mengubah properti yang terdapat dalam tag tersebut.

    ```css
    h1 {
      color: #fca205;
      font-family: "Monospace";
      font-style: italic;
    }
    ```

2. ID Selector

    _ID selector_ menggunakan ID pada tag sebagai _selector_-nya.

    Kamu dapat menambahkan ID pada templat HTML sebagai berikut (ID harus bersifat unik).

    ```css
    ...
    <body>
      <div id="header">
        <h1>Tutorial CSS Yay</h1>
      </div>
      ...
    </body>
    ```

    Kemudian tambahkan ID tersebut sebagai _selector_ pada file CSS kamu.

    ```css
    #header {
      background-color: #f0f0f0;
      margin-top: 0;
      padding: 20px 20px 20px 40px;
    }
    ```

    Dapat dilihat perubahan tampilan yang terjadi. Silakan menambahkan _ID selector_ lain untuk mengubah properti lainnya.

3. Class Selector

    Selanjutnya, class selector yang dapat digunakan untuk memperindah tampilan templat HTML.
    Tambahkan beberapa class pada tag HTML

    ```html
    ...
    <div id="main">
        <div class="content_section">
            <p class="date">published: 28 September 2022</p>
            <h2><a href="">Tutorial CSS ku</a></h2>
            <p id="content_1">Yay ini tutorial yang gampang!</p>
        </div>
        <div class="content_section">
            <p class="date ">published: 29 September 2022</p>
            <h2><a href="">Tutorial CSS mu</a></h2>
            <p id="content_2">Yay ini tutorial yang mudah!</p>
        </div>
        <div class="content_section">
            <p>published: 30 September 2022</p>
            <h2><a href="">Tutorial CSS semua</a></h2>
            <p id="content_3">Yay ini tutorial yang tidak sulit!</p>
        </div>
    </div>
    ...
    ```

    Kemudian taambahkan _class selector_ berikut pada file CSS kamu.

    ```css
    .content_section {
      background-color: #3696e1;
      margin-bottom: 30px;
      color: #000000;
      font-family: cursive;
      padding: 20px 20px 20px 40px;
    }
    ```

    Silakan menambahkan _class selector_ lain untuk mengubah properti lainnya.

Perbedaan penulisan _ID selector_ dan _class selector_ adalah _ID selector_ menggunakan format `#[id_name]` (selalu diawali `#`) sedangkan _class selector_ menggunakan format `.[class_name]` (diawali `.`).

Untuk memperdalam pengetahuan mengenai _CSS Selector Reference_, kamu dapat membaca referensi [ini](https://www.w3schools.com/cssref/css_selectors.asp).

## Tips & Trik untuk CSS

### Mengenal Combinators

Setelah mengetahui _selector_ pada CSS, kamu dapat mengenal _combinators_ pada CSS. _Combinators_ adalah suatu penanda yang menandakan hubungan antar elemen, _class_, atau ID pada CSS.

Terdapat empat _combinators_ pada CSS.

1. Descendant selector (_space_)
2. Child selector (>)
3. Adjacent sibling selector (+)
4. General sibling selector (~)

Silakan pelajari keempat jenis _combinators_ tersebut CSS tersebut pada referensi [ini](https://www.w3schools.com/css/css_combinators.asp).

### Mengenal CSS Pseudo-class

_Pseudo-class_ digunakan untuk mendefinisikan _state_ khusus dari sebuah elemen. Contoh beberapa _pseudo-class_ adalah sebagai berikut.

- **:active** memilih elemen yang sedang aktif
- **:checked** memilih elemen yang telah dicentang
- **:disabled** memilih elemen yang telah dinonaktifkan
- **:enabled** memilih elemen yang telah diaktifkan
- **:link** memilih tautan yang belum pernah dikunjungi
- **:hover** memilih elemen pada saat kursor berada diatasnya
- **:visited** memilih link yang sudah pernah dikunjungi

Umumnya _pseudo-class_ dituliskan dalam bentuk sebagai berikut.

```css
selector:pseudo-class {
  properties: value;
}
```

### Perbedaan Margin, Border dan Padding

Kamu dapat melihat perbedaan _margin_, _border_, dan _padding_ pada referensi [ini](https://www.w3schools.com/css/css_boxmodel.asp).

## Pengenalan Bootstrap

Terdapat banyak _framework_ CSS yang sering digunakan sekarang ini, salah satunya adalah Bootstrap CSS. Bootstrap CSS menyediakan _class_-_class_ yang sering digunakan dalam pengembangan suatu situs web. _Class_-_class_ yang disediakan seperti _navbar_, _card_, _footer_, _carousel_, dan lain-lain. Selain itu, Bootstrap CSS juga menyediakan banyak fitur yang berguna. Salah satu fitur yang berguna pada Bootstrap CSS adalah _grid system_ yang berguna untuk membagi halaman situs web menjadi lebih mudah dan menarik.

Untuk mempelajari lebih lanjut mengenai Bootstrap CSS, kamu dapat membaca referensi [ini](https://getbootstrap.com/docs/5.2/getting-started/introduction/).

## Responsive Web Design

_Responsive web design_ merupakan metode atau pendekatan sistem desain web yang bertujuan untuk memberikan tampilan situs web yang terlihat baik pada semua perangkat (baik pada komputer meja, tablet, atau ponsel). _Responsive web design_ tidak mengubah konten yang ada pada situs web, melainkan hanya mengubah cara penyajian pada setiap perangkat agar sesuai dengan ukuran layar dan perilaku perangkat masing-masing. _Responsive web design_ menggunakan CSS untuk mengubah ukuran (seperti menyusutkan dan membesarkan) suatu elemen.

Untuk mengecek penerapan _responsive web design_ pada suatu situs web, kamu dapat mengakses situs web tersebut dan membuka fitur `Toggle Device Mode` pada browser.

Berikut adalah _keyboard shortcut_ untuk mengakes fitur tersebut pada browser Google Chrome.

- Windows/Linux : `CTRL + SHIFT + M`
- Mac : `Command + Shift + M`

Untuk mempelajari lebih lengkap mengenai Reponsive Web Design, kamu dapat membuka referensi [ini](https://web.dev/responsive-web-design-basics/).

## Tutorial: Menambahkan Bootstrap pada Aplikasi Money Tracker

Berikut adalah hal yang perlu kamu lakukan untuk menyelesaikan bagian tutorial ini.

1. Menambahkan barisan kode yang dibutuhkan agar aplikasi kamu dapat menggunakan Bootstrap.

    > Silakan merujuk kepada informasi pada laman [ini](https://getbootstrap.com/docs/5.2/getting-started/introduction/).

2. Silakan lakukan modifikasi pada tampilan aplikasi `money_tracker` kamu sekreatif mungkin dengan menggunakan Bootstrap.

## Tutorial: Menambahkan Navbar pada Keseluruhan Laman Aplikasi

Tambahkan _navigation bar_ (boleh menggunakan Bootstrap) pada halaman `tracker.html` kamu dan tampilkan **nama kamu** dan **tombol _logout_** pada _navigation bar_ yang kamu buat.

## Tutorial: Membuat Fungsi untuk Memperbarui Data Transaksi

Berikut adalah yang perlu kamu lakukan untuk menyelesaikan bagian tutorial ini.

1. Buat fungsi baru dengan nama `modify_transaction` yang menerima parameter `request` dan `id` pada `views.py` di folder `money_tracker` untuk melakukan perbaruan data transaksi. Kamu dapat menggunakan templat kode berikut untuk memuat fungsinya.

    > Jangan lupa untuk memahami isi kodenya, ya. 😉
  
    ```python
    def modify_transaction(request, id):
        # Get data berdasarkan ID
        transaction = TransactionRecord.objects.get(pk = id)

        # Set instance pada form dengan data dari transaction
        form = TransactionRecordForm(request.POST or None, instance=transaction)

        if form.is_valid() and request.method == "POST":
            # Simpan form dan kembali ke halaman awal
            form.save()
            return HttpResponseRedirect(reverse('money_tracker:show_tracker'))
        
        context = {'form': form}
        return render(request, "modify_transaction.html", context)
    ```
  
2. Buka `urls.py` yang ada pada folder `money_tracker` dan impor fungsi yang sudah kamu buat tadi.

    ```python
    from money_tracker.views import modify_transaction
    ```

3. Tambahkan _path url_ ke dalam `urlpatterns` untuk mengakses fungsi yang sudah diimpor tadi.

    ```python
    ...
    path('modify/<int:id>', modify_transaction, name='modify_transaction'), #sesuaikan dengan nama fungsi yang dibuat
    ...
    ```

4. Buatlah sebuah berkas baru pada folder `money_tracker/templates` dengan nama `modify_transaction.html`. Kemudian, isilah file tersebut dengan templat berikut ini.

    ```html
    {% extends 'base.html' %}

    {% load static %}

    {% block content %}

    <h1>Ubah Data Transaksi</h1>

    <form method="POST">
        {% csrf_token %}
        <table>
            {{ form.as_table }}
            <tr>
                <td></td>
                <td>
                    <input type="submit" value="Ubah"/>
                </td>
            </tr>
        </table>
    </form>

    {% endblock %}
    ```

5. Bukalah berkas `tracker.html` yang ada pada folder `money_tracker/templates` dan ubahlah kode yang sudah ada menjadi seperti berikut agar terdapat tombol ubah untuk setiap transaksi.

    ```html
    <table>
        <tr>
            <th>Nama</th>
            <th>Jenis</th>
            <th>Jumlah</th>
            <th>Tanggal</th>
            <th>Deskripsi</th>
            <th>Aksi</th>
        </tr>
        {% comment %} Tambahkan data di bawah baris ini {% endcomment %}
        {% for transaction in list_of_transactions %}
            <tr>
                <td>{{transaction.name}}</td>
                <td>{{transaction.type}}</td>
                <td>{{transaction.amount}}</td>
                <td>{{transaction.date}}</td>
                <td>{{transaction.description}}</td>
                <td>
                    <a href="{% url 'money_tracker:modify_transaction' transaction.pk %}">
                        <button>
                            Ubah
                        </button>
                    </a>
                </td>
            </tr>
        {% endfor %}
    </table>
    ...
    ```

## Tutorial: Membuat Fungsi untuk Menghapus Data Transaksi

Berikut adalah yang perlu kamu lakukan untuk membuat fungsi penghapusan data transaksi.

1. Buat fungsi baru dengan nama `delete_transaction` yang menerima parameter `request` dan `id` pada `views.py` di folder `money_tracker` untuk melakukan _delete_ data transaksi. Kamu dapat menggunakan templat kode berikut untuk memuat fungsinya.

    > Jangan lupa untuk memahami isi kodenya, ya. 😉

    ```python
    def delete_transaction(request, id):
        # Get data berdasarkan ID
        transaction = TransactionRecord.objects.get(pk = id)
        # Hapus data
        transaction.delete()
        # Kembali ke halaman awal
        return HttpResponseRedirect(reverse('money_tracker:show_tracker'))
    ```

2. Buka `urls.py` yang ada pada folder `money_tracker` dan impor fungsi yang sudah kamu buat tadi.

    ```python
    from money_tracker.views import delete_transaction
    ```

3. Tambahkan _path url_ ke dalam `urlpatterns` untuk mengakses fungsi yang sudah diimpor tadi.

    ```python
    ...
    path('delete/<int:id>', delete_transaction, name='delete_transaction'), #sesuaikan dengan nama fungsi yang dibuat
    ...
    ```

4. Bukalah berkas `tracker.html` yang ada pada folder `money_tracker/templates` dan ubahlah kode yang sudah ada menjadi seperti berikut agar terdapat tombol hapus untuk setiap transaksi.

    ```html
    <table>
        <tr>
            <th>Nama</th>
            <th>Jenis</th>
            <th>Jumlah</th>
            <th>Tanggal</th>
            <th>Deskripsi</th>
            <th>Aksi</th>
        </tr>
        {% comment %} Tambahkan data di bawah baris ini {% endcomment %}
        {% for transaction in list_of_transactions %}
            <tr>
                <td>{{transaction.name}}</td>
                <td>{{transaction.type}}</td>
                <td>{{transaction.amount}}</td>
                <td>{{transaction.date}}</td>
                <td>{{transaction.description}}</td>
                <td>
                  <a href="{% url 'money_tracker:modify_transaction' transaction.pk %}">
                      <button>
                          Ubah
                      </button>
                  </a>
                  <a href="{% url 'money_tracker:delete_transaction' transaction.pk %}">
                      <button>
                          Hapus
                      </button>
                  </a>
                </td>
            </tr>
        {% endfor %}
    </table>
    ...
    ```

Jalankan proyek Django-mu dan cobalah untuk menghapus data transaksi yang sudah ada pada browser favoritmu.

## Referensi Tambahan

- Kamu dapat membuka tautan [ini](https://getbootstrap.com/docs/5.2/components/navbar/) untuk melihat kode yang dapat kamu gunakan untuk menambahkan _navigation bar_ dengan menggunakan Bootstrap.
- Kamu dapat membuka tautan [ini](https://www.w3schools.com/css/css_navbar.asp) untuk melihat kode yang dapat kamu gunakan untuk menambahkan _navigation bar_ dengan menggunakan CSS secara manual.

## Akhir Kata

Selamat! Kamu telah menyelesaikan Tutorial 4 dengan baik. 😄

Seperti biasa, jangan lupa untuk melakukan `add`, `commit`, dan `push` perubahan yang sudah kamu lakukan untuk menyimpannya ke dalam repositori GitHub sebelum kamu menutup pekerjaan kamu. 😉

## Credits

Tutorial ini dikembangkan berdasarkan [PBP Ganjil 2023](https://github.com/pbp-fasilkom-ui/ganjil-2023) yang ditulis oleh Tim Pengajar Pemrograman Berbasis Platform 2023. Segala tutorial serta instruksi yang dicantumkan pada repositori ini dirancang sedemikian rupa sehingga mahasiswa yang sedang mengambil mata kuliah Pemrograman Berbasis Platform dapat menyelesaikan tutorial saat sesi lab berlangsung.
