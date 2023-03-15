# Tutorial 5: JavaScript dan AJAX

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer Universitas Indonesia, Semester Genap 2022/2023

---

## Tujuan Pembelajaran

Setelah menyelesaikan tutorial ini, mahasiswa diharapkan untuk mengerti:

- Penggunaan fungsi JavaScript pada _front-end development_
- Penggunaan dasar JavaScript
- Penggunaan AJAX

---

## Pengenalan JavaScript

### Apa itu JavaScript?

JavaScript merupakan bahasa pemrograman multi-paradigma tingkat tinggi lintas
platform (_cross platform high-level multi-paradigm programming language_). Sifat
multi-paradigma membuat JavaScript mendukung konsep _object-oriented programming_,
_imperative programming_, dan _functional programming_. JavaScript sendiri merupakan
implementasi dari ECMAScript, yang merupakan inti dari bahasa JavaScript. Beberapa
implementasi lain dari ECMAScript yang mirip dengan JavaScript antara lain JScript
(Microsoft) dan ActionScript (Adobe).

JavaScript, bersama dengan HTML dan CSS, menjadi tiga teknologi utama yang dipakai
pada pengembangan web. Keuntungan menggunakan JavaScript dalam pengembangan
web, pada dasarnya, antara lain JavaScript dapat memanipulasi halaman web secara
dinamis dan memberikan interaksi lebih kepada pengguna. Oleh karena itu, hampir semua
situs web modern saat ini menggunakan JavaScript dalam halaman web mereka untuk memberikan
pengalaman terbaik kepada pengguna. Beberapa contoh hal yang dapat kita lakukan dengan
menggunakan JavaScript antara lain menampilkan informasi berdasarkan waktu, mengenali jenis
browser pengguna, melakukan validasi form atau data, membuat cookies (bukan kue, tapi
[cookies](https://en.wikipedia.org/wiki/HTTP_cookie)), mengganti _styling_ dan CSS suatu
_element_ secara dinamis, dan lain-lain.

Pada pengembangan web umumnya kode JavaScript digunakan pada _client-side_ suatu
web (_Client-side JavaScript_) namun beberapa jenis kode JavaScript saat ini digunakan pada
_server-side_ suatu web (_Server-side JavaScript_) seperti **node.js**. Istilah _client-side_
menunjukkan bahwa kode JavaScript akan dieksekusi atau dijalankan pada browser pengguna,
bukan pada server situs web. Hal ini berarti kompleksitas kode JavaScript tidak akan memengaruhi
performa server situs web tersebut namun memengaruhi performa browser dan komputer; semakin
kompleks kode JavaScript, maka semakin banyak memori komputer yang dikonsumsi oleh browser.

Pada mata kuliah PBP, kita hanya akan fokus kepada kode _client-side_ JavaScript.

### Bagaimana tahapan JavaScript dieksekusi oleh browser?

Perhatikan diagram berikut.

![javascript-works](https://preview.ibb.co/e258TG/Screenshot_from_2017_10_31_14_29_13.png)

Setelah browser mengunduh halaman HTML web maka tepat dimana tag `<script></script>`
berada, browser akan melihat _tag script_ tersebut, apakah tag tersebut berisi kode _embedded_
JavaScript atau merujuk file eksternal JavaScript. Jika merujuk pada file eksternal JavaScript,
maka browser akan mengunduh file tersebut terlebih dahulu.

### Cara penulisan JavaScript

Cara penulisan JavaScript bisa dilakukan dengan **_embedded JavaScript_** atau **_external JavaScript_**.
Kode JavaScript dapat didefinisikan atau dituliskan secara _embedded_ pada file HTML maupun
secara terpisah pada file tersendiri. Jika ditulis dalam file terpisah dari HTML, ekstensi file yang
digunakan untuk file JavaScript adalah `.js`. Berikut contoh beberapa pendefinisian dari JavaScript.

JavaScript dapat diletakkan pada _head_ atau _body_ dari halaman HTML. Selain itu, kode JavaScript
**harus** dimasukkan di antara tag `<script>` dan `</script>`. Kamu dapat meletakkan lebih dari satu
_tag script_ yang berisi JavaScript pada suatu file HTML.

#### Embedded JavaScript pada HTML

`index.html`

```html
<script type="text/JavaScript">
  alert("Hello World!");
</script>
```

#### External JavaScript pada HTML

`index.html`

```html
<script type="text/JavaScript" src="js/script.js"></script>
```

`js/script.js`

```javascript
alert("Hello World!");
```

Pada file eksternal JavaScript, tag `<script>` tidak perlu lagi ditambahkan.

Memisahkan JavaScript pada file tersendiri dapat memberikan beberapa keuntungan seperti kode dapat
digunakan di file HTML lain, kode JavaScript dan HTML tidak bercampur sehingga lebih fokus saat
mengembangkan aplikasi, serta mempercepat loading halaman. File `.js` biasanya akan di-_cache_ oleh
browser sehingga jika kita membuka halaman yang sama dan tidak ada perubahan pada file `.js`, maka
browser tidak akan meminta file `.js` tersebut kepada server lagi, namun akan menggunakan file dari
_cache_ yang sudah disimpan sebelumnya.

### Eksekusi JavaScript

Setelah JavaScript sudah terunduh dengan sempurna, maka browser akan langsung mulai
mengeksekusi kode JavaScript. Jika kode tersebut BUKAN merupakan _event-triggered_,
maka kode langsung dieksekusi. Jika kode tersebut merupakan _event-triggered_, maka
kode tersebut hanya akan dieksekusi jika event yang didefinisikan terpicu (_triggered_).

```javascript
// langsung dieksekusi
alert("Hello World");

// langsung dieksekusi
var obj = document.getElementById("object");
// langsung dieksekusi, menambahkan event handler onclick untuk element object
obj.onclick = function () {
  // hanya dieksekusi jika element 'object' di klik
  alert("You just click the object!");
};
```

### Sintaks JavaScript

#### Variabel

Mendefinisikan variabel pada JavaScript cukup mudah. Contohnya seperti berikut.

```javascript
var example = 0; // var example merupakan sebuah bilangan
var example = "example"; // var example merupakan sebuah string
var example = true; // var example merupakan sebuah boolean
```

JavaScript dapat menampung banyak tipe data; mulai dari string, integer, hingga _object_ sekalipun.
Berbeda dengan Java yang penandaan tipe datanya dibedakan dengan _head variable_ (contoh ingin
membuat variabel dengan tipe data `int`, maka sintaknya seperti `int x = 9`), JavaScript mempunyai
ciri khas _loosely typed_ atau _dynamic language_, yakni kamu tidak perlu menuliskan tipe data
pada _head variable_ dan JavaScript nantinya akan secara otomatis membaca tipe data kamu
berdasarkan standar yang ada (seperti pada contoh diatas).

Ada beberapa aturan dalam pemilihan _indentifiers_ atau nama variabel dalam JavaScript. Karakter
pertama HARUS merupakan alfabet, _underscore_ ( \_ ), atau karakter dollar ($). Selain itu,
JavaScript _identifiers_ bersifat _case sensitive_.

#### String Concatenation

Dalam JavaScript, kita juga dapat menyambungkan `string` dengan `string` lainnya seperti pada Java.

```javascript
var str1 = "PBP" + " " + "Fun";
var str2 = "PBP";
var str3 = "Fun";
var str4 = str2 + " " + str3;
var str5 = "Fun";
var str6 = `PBP ${str5}`;  // Memiliki hasil yang sama seperti "PBP" + " " + str5
```

### JavaScript Scope

#### Variabel Lokal

Variabel yang didefinisikan **di dalam** fungsi bersifat lokal, sehingga hanya dapat diakses oleh kode didalam fungsi tersebut.

```javascript
// kode diluar fungsi thisFunction() tidak dapat mengakses variabel courseName
function thisFunction() {
  var courseName = "PBP";
  // kode di dalam fungsi ini dapat mengakses variabel courseName
}
```

#### Variabel Global

Variabel yang didefinisikan **di luar** fungsi bersifat global dan dapat diakses oleh kode lain dalam file JavaScript tersebut.

```javascript
var courseName = "PBP";
function thisFunction() {
  // kode di dalam fungsi ini dapat mengakses variabel courseName
}
```

#### Auto Global Variable

Value yang di-_assign_ pada variabel yang belum dideklarasikan otomatis menjadi _global variable_ walaupun variabel tersebut berada di dalam suatu fungsi.

```javascript
thisFunction(); // function thisFunction() perlu dipanggil terlebih dahulu
console.log(courseName); // print "PBP" pada JavaScript console
function thisFunction() {
  courseName = "PBP";
}
```

#### Mengakses Variabel Global dari HTML

Kamu dapat mengakses variabel yang berada dalam file JavaScript
pada file HTML yang mengunduh file JavaScript tersebut.

```html
...
<input type="text" onclick="this.value=courseName" />
...
```

```javascript
...
var courseName = "PBP";
...
```

### Function dan Event

_Function_ adalah sekumpulan grup dari kode-kode yang bisa dipanggil dimanapun pada bagian
kode program (mirip dengan `method` pada Java). Hal ini mengurangi redundansi kode yang ada
(mengurangi kode-kode yang dapat sama berulang-ulang). Selain itu, _function_ pada JavaScript
sangat berguna untuk memudahkan elemen pemanggilan secara dinamis. _Function_ dapat dipanggil
sesama _function_ dan dapat juga dipanggil karena _event_ (akan dijelaskan di bawah).
Sebagai contoh, berikut kode yang terdapat pada `index.html`.

```html
...
<input type="button" value="magicButton" id="magicButton" onclick="hooray();" />
...
```

Kemudian berikut adalah kode pada `javascript.js`.

```javascript
...
function hooray(){
    alert("Yahoo!");
}
...
```

Apabila `magicButton` ditekan, maka fungsi `onclick` akan menjalankan _function_ `hooray()`
pada `javascript.js`, lalu muncul _alert_ sesuai yang sudah di-_assign_ sebelumnya.

Kode `onclick` sebenarnya adalah salah satu contoh kemampuan JavaScript yang disebut
_event_. _Event_ adalah kemampuan JavaScript untuk membuat sebuah situs web dinamis. Maksud
dari `onclick` adalah penanda apa yang akan dilakukan JavaScript jika elemen tersebut ditekan.
Selain itu, _event_ biasanya diberikan sebuah fungsi yang berguna sebagai perintah-perintah
untuk JavaScript. Selain itu, banyak contoh-contoh _event_ lainnya seperti `onchange`,
`onmouseover`, `onmouseout`, dan lain sebagainya yang bisa kamu baca pada tautan
[ini](https://www.w3schools.com/js/js_events.asp).

### JavaScript HTML & CSS DOM

#### HTML DOM

HTML DOM (_Document Object Model_) adalah standar bagaimana mengubah, mengambil, dan menghapus HTML _elements_. HTML DOM dapat diakses melalui JavaScript atau dengan bahasa pemrograman lainnya. Detail lengkapnya dapat dilihat [di sini](https://www.w3schools.com/js/js_htmldom.asp).

Berikut contoh implementasinya.

```html
...     
<div>
  <p onclick="myFunction()" id="demo">Example of HTML DOM</p>
      
</div>
...
```

```javascript
...
    function myFunction() {
document.getElementById("demo").innerHTML = "YOU CLICKED ME!";
    }
...
```

#### CSS DOM

Sama dengan HTML DOM, CSS DOM dapat mengubah CSS secara dinamis melalui JavaScript.
Detail lengkapnya dapat dilihat [di sini](https://www.w3schools.com/js/js_htmldom_css.asp).

Berikut adalah contohnya.

`index.html`

```html
...
<p id="blueText" onclick="changeColor()">Click me v2</p>
...
```

`javascript.js`

```javascript
...
function changeColor(){
    document.getElementById("blueText").style.color="blue";
}
...
```

---

## Pengenalan AJAX

AJAX merupakan singkatan dari _**A**synchronous **J**avaScript **A**nd **X**ML_.

AJAX bukanlah sebuah bahasa pemrograman. AJAX menggunakan browser untuk meminta data dari _web server_ dan JavaScript serta HTML DOM untuk menampilkan data. AJAX dapat menggunakan XML untuk mengirim data tetapi dapat juga menggunakan teks ataupun JSON. AJAX membuat halaman web memperbarui data secara asinkronus dengan mengirimkan data ke server di balik layar, artinya kita dapat memperbarui sebagian elemen data pada halaman tanpa harus me-_reload_ keseluruhan halaman.

Berikut ini adalah cara kerja AJAX.

![ajax-works](https://www.w3schools.com/js/pic_ajax.gif)

1. Sebuah _event_ terjadi pada halaman web (contohnya tombol _submit data_ ditekan)
2. Sebuah `XMLHttpRequest` _object_ dibuat oleh JavaScript
3. `XMLHttpRequest` _object_ mengirimkan _request_ ke server
4. Server memproses _request_ tersebut
5. Server mengembalikan _response_ kembali kepada halaman web
6. _Response_ dibaca oleh JavaScript
7. Aksi berikutnya akan dipicu oleh JavaScript sesuai dengan langkah yang dibuat (contohnya memperbarui data di halaman tersebut)

Kamu bisa menggunakan `jQuery` untuk melakukan AJAX. JQuery adalah _library_ JavaScript yang dibuat untuk mempermudah akses ke beberapa _Core API_ yang disediakan oleh browser.

Selain itu, kamu juga dapat melakukan AJAX di browser modern dengan menggunakan fungsi `fetch()` yang diberikan oleh JavaScript. Penggunaan `fetch()` untuk melakukan pemanggilan AJAX dapat dilihat di tautan berikut ini: <https://www.w3schools.com/jsref/api_fetch.asp>

---

## Tutorial: Views untuk AJAX

Kamu diminta untuk menambahkan fungsionalitas AJAX ke projek `money_tracker` yang sudah dibuat pada tutorial sebelumnya.

1. Import `JsonResponse` dari `django.http`dan `csrf_exempt` dari `django.views.decorators.csrf` ke dalam file `views.py`

2. Buatlah fungsi baru dengan nama `create_transaction_ajax` yang menerima parameter `request` pada _file_ `money_tracker/views.py`.

3. Salinlah kode berikut pada fungsi baru tersebut (dengan `@csrf_exempt`).

    ```python
    @csrf_exempt
    def create_transaction_ajax(request):  
    # create object of form
    form = TransactionRecordForm(request.POST or None)
    
    if form.is_valid() and request.method == "POST":
        form.save()
        data = TransactionRecord.objects.last()

        # parsing the form data into json
        result = {
            'id':data.id,
            'name':data.name,
            'type':data.type,
            'amount':data.amount,
            'date':data.date,
            'description':data.description,
        }
        return JsonResponse(result)
    
        context = {'form': form}
        return render(request, "create_transaction.html", context)
    ```

4. Import _function_ yang telah kamu buat sebelumnya pada `money_tracker/urls.py`.

    ```python
    # contoh
    from money_tracker.views import create_transaction_ajax
    ```

5. Tambahkan _path_ baru untuk membuat objek transaksi baru dengan baris kode berikut ini pada `urlpatterns`.

    ```python
    ...
    path('create-ajax/', create_transaction_ajax, name='create_transaction_ajax'),
    ```

6. Modifikasi _file_ `money_tracker/tracker.html` dengan kode baru berikut ini agar dapat menambahkan data baru dengan AJAX.

    ```html
    {% extends 'base.html' %}

    {% block content %}
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>

    ```

7. Tambahkan potongan kode berikut untuk menampilkan data transaksi dalam bentuk _cards_.

    ```html
    <script>
    $(document).ready(function(){
        $.get("/tracker/json/", function(data) {
            for (i=0; i<data.length; i++){
                $('#tracker').append(`
                <div id="${data[i].id}--task" class="col-md-6 col-lg-3 mb-3">
                    <div class="card d-flex">
                        <div class="card-body d-flex flex-column">
                            <h5 class="card-title">${data[i].fields.name}</h5>
                            <p class="card-text date">${data[i].fields.date}</p>
                            <p class="card-text">${data[i].fields.type}</p>
                            <p class="card-text">${data[i].fields.amount}</p>
                            <p class="card-text">${data[i].fields.description}</p>
                            <div class="mt-auto">
                                <a href="/tracker/delete/${data[i].pk}" class="btn btn-primary delete mb-2">Hapus</a>
                                <a href="/tracker/modify/${data[i].pk}" class="btn btn-secondary mb-2">Ubah</a>
                            </div>
                        </div>
                    </div>
                </div>
                `)
            }
        });
    </script>
    ```

8. Tambahkan kode berikut untuk membuat sebuah modal popup yang berfungsi untuk menambahkan transaksi baru pada laman tracker.

    ```html
    <body>
        <h5>Nama: </h5>
        <p>{{name}}</p>
        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#createModal">
            Tambah Transaksi
        </button>
        
        <!-- Modal -->
        <div class="modal" id="createModal" tabindex="-1" aria-labelledby="createModalLabel" aria-hidden="true">
            <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                <h1 class="modal-title fs-5" id="createModalLabel">Tambah Transaksi</h1>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Cancel"></button>
                </div>
                <div class="modal-body">
                {% csrf_token %}
                <label for="name" class="form-label">Judul transaksi:</label><br>
                <input type="text" id="name" class="form-control" name="name" placeholder="Bayar UKT"><br>
                <label for="type" class="form-label">Tipe transaksi:</label>
                <select name="type" id="type" class="form-select" aria-label="Default select example">
                    <option selected value="Pemasukan">Pemasukan</option>
                    <option value="Pengeluaran">Pengeluaran</option>
                </select><br>
                <label for="amount" class="form-label">Jumlah transaksi:</label><br>
                <input type="number" id="amount" class="form-control" name="amount" placeholder="100000"><br>
                <label for="description" class="form-label">Deskripsi transaksi:</label><br>
                <input type="text" id="description" class="form-control" name="description" placeholder="UKT untuk Bulan Mei"><br>
                </div>
                <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                <button id="submit_btn" type="button" class="btn btn-primary create" id="add-task" data-bs-dismiss="modal">Add</button>
                </div>
            </div>
            </div>
        </div>
    </body>

    <div class="row m-2" id="tracker"></div>

    {% endblock content %}
    ```

9. Modifikasi potongan kode yang sudah ditulis sebelumnya pada poin ke 6 menjadi kode berikut untuk membuat fungsi pada tombol _submit_ modal agar dapat menambahkan data transaksi secara asinkronus.

    ```html
    <script>
        $(document).ready(function(){
            $.get("/tracker/json/", function(data) {
                for (i=0; i<data.length; i++){
                    $('#tracker').append(`
                    <div id="${data[i].id}--task" class="col-md-6 col-lg-3 mb-3">
                        <div class="card d-flex">
                            <div class="card-body d-flex flex-column">
                                <h5 class="card-title">${data[i].fields.name}</h5>
                                <p class="card-text date">${data[i].fields.date}</p>
                                <p class="card-text">${data[i].fields.type}</p>
                                <p class="card-text">${data[i].fields.amount}</p>
                                <p class="card-text">${data[i].fields.description}</p>
                                <div class="mt-auto">
                                    <a href="/tracker/delete/${data[i].pk}" class="btn btn-primary delete mb-2">Hapus</a>
                                    <a href="/tracker/modify/${data[i].pk}" class="btn btn-secondary mb-2">Ubah</a>
                                </div>
                            </div>
                        </div>
                    </div>
                    `)
                }
            });

            $("#submit_btn").click(function(){
                $.post("/tracker/create-ajax/", {
                    name: $("#name").val(),
                    type: $("#type").val(),
                    amount: $("#amount").val(),
                    description: $("#description").val()
                },
                function(result, status){
                    if (status == 'success'){
                        $("#tracker").append(`
                        <div id="${result.id}--task" class="col-md-6 col-lg-3 mb-3">
                            <div class="card d-flex">
                                <div class="card-body d-flex flex-column">
                                    <h5 class="card-title">${result.name}</h5>
                                    <p class="card-text date">${result.date}</p>
                                    <p class="card-text">${result.type}</p>
                                    <p class="card-text">${result.amount}</p>
                                    <p class="card-text">${result.description}</p>
                                    <div class="mt-auto">
                                        <a href="/tracker/delete/${result.id}" class="btn btn-primary delete mb-2">Hapus</a>
                                        <a href="/tracker/modify/${result.id}" class="btn btn-secondary mb-2">Ubah</a>
                                    </div>
                                </div>
                            </div>
                        </div>
                        `);
                    $('#name').val('')
                    $('#date').val('')
                    $('#amount').val('')
                    $('#description').val('')
                    }
                })
            })
        })
    </script>
    ```

10. Jalankan aplikasi kamu dan cobalah untuk menanmbahkan beberapa data transaksi baru. Sekarang, data transaksi baru dapat ditambahkan secara asinkronus tanpa harus melakukan _synchronous refresh page_ terlebih dahulu.

---

## Materi Tambahan: Web Storage

Dengan penyimpanan lokal, aplikasi web dapat menyimpan data secara lokal dalam browser pengguna. Hal ini berguna apabila anda menggunakan _framework front-end_ seperti React ataupun Vue, karena kemampuan penggunaan _cookies_ pada _framework-framework_ tersebut terbatas.
Sebelum HTML5, data aplikasi harus disimpan dalam _cookies_ (termasuk dalam setiap permintaan server). Penyimpanan lokal bersifat lebih aman dan sejumlah besar data dapat disimpan secara lokal tanpa mempengaruhi kinerja situs web.
Tidak seperti _cookies_, batas penyimpanan jauh lebih besar (setidaknya 5MB) dan informasi yang disimpan tidak pernah ditransfer ke server.
Penyimpanan lokal adalah per asal (per domain dan protocol). Semua halaman (dari satu asal) dapat menyimpan dan mengakses data yang sama.

Terdapat 2 cara menyimpan data menggunakan web storage.

- `window.localStorage` - menyimpan data tanpa tanggal kadaluarsa

- `window.sessionStorage` - menyimpan data untuk satu session (data hilang ketika tab browser ditutup)

### Obyek localStorage

Objek `localStorage` menyimpan data tanpa tanggal kedaluwarsa. Data tidak akan dihapus ketika browser ditutup, dan akan tersedia pada hari berikutnya, minggu, atau tahun.

Berikut adalah contoh implementasinya.

`index.html`

```html
...
<p><button onclick="clickCounter()" type="button">Click me!</button></p>
<div id="result"></div>
<p>Click the button to see the counter increase.</p>
<p>
  Close the browser tab (or window), and try again,
  and the counter will continue to count (is not reset).
</p>
...
```

`javascript.js`

```javascript
...
function clickCounter() {
    if(typeof(Storage) !== "undefined") {
        if (localStorage.clickcount) {
            localStorage.clickcount = Number(localStorage.clickcount)+1;
        } else {
            localStorage.clickcount = 1;
        }
        document.getElementById("result").innerHTML = "You have clicked the button " + localStorage.clickcount + " time(s).";
    } else {
        document.getElementById("result").innerHTML = "Sorry, your browser does not support web storage...";
    }
}
...
```

Apabila halaman tersebut dijalankan, ketika tombol ditekan maka terhitung jumlah _click_ akan bertambah.
Ketika browser ditutup dan kita membuka kembali halaman sebelumnya, dapat dilihat bahwa perhitungan jumlah _click_ akan dilanjutkan dari yang sebelumnya.

### Obyek sessionStorage

Objek `sessionStorage` bekerja dengan cara yang mirip dengan `localStorage` (untuk mencoba `sessionStorage`, silakan gunakan kode sebelumnya namun ganti objek `localStorage` dengan `sessionStorage`). Namun apabila browser ditutup dan halaman sebelumnya dibuka kembali, _click count_ akan dimulai kembali dari 0.

Untuk membaca lebih lanjut mengenai HTML5 WebStorage, silakan baca referensi berikut: [HTML5 WebStorage](http://www.w3im.com/id/html/html5_webstorage.html).

---

## Akhir Kata

Selamat! Kamu telah menyelesaikan tutorial Django terakhir. 😄

Seperti biasa, jangan lupa untuk melakukan `add`, `commit`, dan `push` perubahan yang sudah kamu lakukan untuk menyimpannya ke dalam repositori GitHub sebelum kamu menutup pekerjaan kamu. 😉

---

## Credits

Tutorial ini dikembangkan berdasarkan [PBP Ganjil 2023](https://github.com/pbp-fasilkom-ui/ganjil-2023) yang ditulis oleh Tim Pengajar Pemrograman Berbasis Platform 2023. Segala tutorial serta instruksi yang dicantumkan pada repositori ini dirancang sedemikian rupa sehingga mahasiswa yang sedang mengambil mata kuliah Pemrograman Berbasis Platform dapat menyelesaikan tutorial saat sesi lab berlangsung.
