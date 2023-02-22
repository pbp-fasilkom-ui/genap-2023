# Tutorial 2: Form dan Data Delivery

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer Universitas Indonesia, Semester Genap 2022/2023

---

## Tujuan Pembelajaran​

Setelah menyelesaikan tutorial ini, mahasiswa diharapkan untuk dapat:

- Mengetahui XML dan JSON sebagai salah satu metode _data delivery_
- Memahami cara kerja submisi data yang diberikan oleh pengguna menggunakan elemen `form`
- Memahami cara mengirimkan data menggunakan format XML dan JSON
- Memahami cara mengambil data spesifik berdasarkan ID

---

## Pengenalan Data Delivery

Dalam mengembangkan suatu _platform_, ada kalanya kita perlu mengirimkan data dari satu _stack_ ke _stack_ lainnya. Data yang dikirimkan bisa bermacam-macam bentuknya. Beberapa contoh format data yang umum digunakan antara lain HTML, XML, dan JSON. Implementasi _data delivery_ dalam bentuk HTML sudah kamu pelajari pada tutorial sebelumnya. Tutorial ini akan mengajarkan _data delivery_ melalui XML dan JSON.

---

## XML (Extensible Markup Language)

XML adalah singkatan dari _eXtensible Markup Language_. XML didesain menjadi _self-descriptive_, sehingga dengan membaca XML tersebut kita bisa mengerti informasi apa yang ingin disampaikan dari data yang tertulis. XML digunakan pada banyak aplikasi web maupun _mobile_, yaitu untuk menyimpan dan mengirimkan data. XML hanyalah informasi yang dibungkus di dalam _tag_. Kita perlu menulis program untuk mengirim, menerima, menyimpan, atau menampilkan informasi tersebut.

Contoh data dalam format XML adalah sebagai berikut.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<subject>
    <name>Bahasa Italia Dasar A</name>
    <lecturer>Prof. Antonietta Sireci</lecturer>
    <credit>3</credit>
    <organizer>Sastra Perancis</organizer>
</subject>
```

XML di atas sangatlah _self-descriptive_:

- Ada informasi nama mata kuliah (`name`)
- Ada informasi nama dosen pengampu (`lecturer`)
- Ada informasi SKS (`credit`)
- Ada informasi penyelenggara (`organizer`)

Dokumen XML membentuk struktur seperti tree yang dimulai dari _root_, lalu _branch_, hingga berakhir pada _leaves_. Dokumen XML **harus mengandung sebuah _root element_** yang merupakan _parent_ dari elemen lainnya. Pada contoh di atas, `<phone>` adalah _root element_.

Untuk baris `<?xml version="1.0" encoding="UTF-8"?>` biasa disebut sebagai **XML Prolog**. XML Prolog bersifat opsional, akan tetapi jika ada maka posisinya harus berada di awal dokumen XML. Pada dokumen XML **semua elemen wajib memiliki _closing tag_**. **Tag pada XML sifatnya _case sensitive_**, sehingga tag `<subject>` berbeda dengan tag `<Subject>`.

---

## JSON (JavaScript Object Notation)

JSON adalah singkatan dari _JavaScript Object Notation_. JSON didesain menjadi _self-describing_, sehingga JSON sangat mudah untuk dimengerti. JSON digunakan pada banyak aplikasi web maupun _mobile_, yaitu untuk menyimpan dan mengirimkan data. Sintaks JSON merupakan turunan dari _Object_ JavaScript. Akan tetapi format JSON berbentuk _text_, sehingga kode untuk membaca dan membuat JSON banyak terdapat dibanyak bahasa pemrograman.

Contoh data dalam format JSON adalah sebagai berikut.

```json
{
    "name": "Bahasa Italia Dasar B",
    "lecturer": "Prof. Antonietta Sireci",
    "credit": "3",
    "organizer": "Sastra Perancis",
}
```

Data pada JSON disimpan dalam bentuk _key_ dan _value_. Pada contoh di atas yang menjadi _key_ adalah `name`, `lecturer`, `credit`, dan `organizer`. _Value_ dapat berupa tipe data primitif (_string, number, boolean_) ataupun berupa objek.

---

## Disclaimer

Dikarenakan belum adanya data yang dimasukkan ke dalam basis data hingga tutorial ini, janganlah kaget apabila fungsi yang akan dibuat tidak menghasilkan data apa-apa. Fungsi _data delivery_ akan tampak hasilnya setelah kamu menyelesaikan tutorial berikutnya (Input Data melalui Form).

---

## Tutorial: Mengembalikan Data dalam Bentuk XML

Catatan: Pada tutorial ini, kamu akan menggunakan proyek yang sudah kamu buat pada tutorial sebelumnya.

1. Buka `views.py` yang ada pada folder `money_tracker` dan buatlah sebuah fungsi yang menerima parameter _request_ (misal bernama `show_xml`).

2. Tambahkan _import_ `HttpResponse` dan `Serializer` pada bagian paling atas.

    ```python
    from django.http import HttpResponse
    from django.core import serializers
    ```

3. Buatlah sebuah variabel di dalam fungsi tersebut yang menyimpan hasil _query_ dari seluruh data yang ada pada `TransactionRecord`.

    ```python
    data = TransactionRecord.objects.all()
    ```

4. Tambahkan _return function_ berupa `HttpResponse` yang berisi parameter data hasil _query_ yang sudah diserialisasi menjadi XML dan parameter `content_type="application/xml"`.

    ```python
    return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")
    ```

5. Buka `urls.py` yang ada pada folder `money_tracker` dan _import_ fungsi yang sudah kamu buat tadi.

    ```python
    from money_tracker.views import show_xml #sesuaikan dengan nama fungsi yang dibuat
    ```

6. Tambahkan _path url_ ke dalam `urlpatterns` untuk mengakses fungsi yang sudah diimpor tadi.

    ```python
    ...
    path('xml/', show_xml, name='show_xml'), #sesuaikan dengan nama fungsi yang dibuat
    ...
    ```

7. Jalankan proyek Django-mu dengan perintah `python manage.py runserver` dan bukalah <http://localhost:8000/tracker/xml/> (sesuaikan dengan _path url_ yang dibuat) di browser favoritmu untuk melihat hasilnya.

---

## Tutorial: Mengembalikan Data dalam Bentuk JSON

1. Buka `views.py` yang ada pada folder `money_tracker` dan buatlah sebuah fungsi baru yang menerima parameter _request_ (misal bernama `show_json`).

2. Buatlah sebuah variabel di dalam fungsi tersebut yang menyimpan hasil _query_ dari seluruh data yang ada pada `TransactionRecord`.

    ```python
    data = TransactionRecord.objects.all()
    ```

3. Tambahkan _return function_ berupa `HttpResponse` yang berisi parameter data hasil _query_ yang sudah diserialisasi menjadi JSON dan parameter `content_type="application/json"`.

    ```python
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")
    ```

4. Buka `urls.py` yang ada pada folder `money_tracker` dan _import_ fungsi yang sudah kamu buat tadi.

    ```python
    from money_tracker.views import show_json #sesuaikan dengan nama fungsi yang dibuat
    ```

5. Tambahkan _path url_ ke dalam `urlpatterns` untuk mengakses fungsi yang sudah diimpor tadi.

    ```python
    ...
    path('json/', show_json, name='show_json'), #sesuaikan dengan nama fungsi yang dibuat
    ...
    ```

6. Jalankan proyek Django-mu dengan perintah `python manage.py runserver` dan bukalah <http://localhost:8000/tracker/json/> (sesuaikan dengan _path url_ yang dibuat) di browser favoritmu untuk melihat hasilnya.

---

## Tutorial: Mengembalikan Data Berdasarkan ID dalam Bentuk XML atau JSON

1. Buka `views.py` yang ada pada folder `money_tracker` dan buatlah sebuah fungsi baru yang menerima parameter _request_ dan ID (misal bernama `show_xml_by_id` dan `show_json_by_id`).

2. Buatlah sebuah variabel di dalam fungsi tersebut yang menyimpan hasil _query_ dari data dengan ID tertentu yang ada pada `TransactionRecord`.

    ```python
    data = TransactionRecord.objects.filter(pk=id)
    ```

3. Tambahkan _return function_ berupa `HttpResponse` yang berisi parameter data hasil _query_ yang sudah diserialisasi menjadi JSON atau XML dan parameter `content_type` dengan _value_ `"application/xml"` (untuk format XML) atau `"application/json"` (untuk format JSON).

    - XML

        ```python
        return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")
        ```

    - JSON

        ```python
        return HttpResponse(serializers.serialize("json", data), content_type="application/json")
        ```

4. Buka `urls.py` yang ada pada folder `money_tracker` dan impor fungsi yang sudah kamu buat tadi.

    ```python
    from money_tracker.views import show_xml_by_id, show_json_by_id #sesuaikan dengan nama fungsi yang dibuat
    ```

5. Tambahkan _path url_ ke dalam `urlpatterns` untuk mengakses fungsi yang sudah diimpor tadi.

    ```python
    ...
    path('xml/<int:id>', show_xml_by_id, name='show_xml_by_id'),
    path('json/<int:id>', show_json_by_id, name='show_json_by_id'), #sesuaikan dengan nama fungsi yang dibuat
    ...
    ```

6. Jalankan proyek Django-mu dengan perintah `python manage.py runserver` dan bukalah <http://localhost:8000/tracker/xml/[id]> atau <http://localhost:8000/tracker/json/[id]> (sesuaikan dengan _path url_ yang dibuat dan id yang diinginkan) di browser favoritmu untuk melihat hasilnya.

---

## Credits

Tutorial ini dikembangkan berdasarkan [PBP Ganjil 2023](https://github.com/pbp-fasilkom-ui/ganjil-2023) yang ditulis oleh Tim Pengajar Pemrograman Berbasis Platform 2023. Segala tutorial serta instruksi yang dicantumkan pada repositori ini dirancang sedemikian rupa sehingga mahasiswa yang sedang mengambil mata kuliah Pemrograman Berbasis Platform dapat menyelesaikan tutorial saat sesi lab berlangsung.
