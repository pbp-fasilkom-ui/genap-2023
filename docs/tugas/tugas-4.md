# Tugas 4: Pengimplementasian Form dan Autentikasi Menggunakan Django

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer Universitas Indonesia, Semester Genap 2022/2023

---

## Deskripsi Tugas

Pada tugas ini, kamu akan mengimplementasikan konsep autentikasi, dan beberapa hal yang sudah kamu pelajari selama tutorial.

Adapun pada tugas ini, kamu diminta untuk:

1. Membuat _form_ registrasi pada aplikasi _study tracker_.

2. Membuat _form_ _login_ pada aplikasi _study tracker_.

3. Membuat fungsi _logout_ pada aplikasi _study tracker_.

4. Melakukan restriksi akses pada halaman _study tracker_.


5. Membuat sebuah `README.md` yang berisi tautan menuju aplikasi Railway yang sudah kamu _deploy_ (jika dapat di-_deploy_) serta jawaban dari beberapa pertanyaan berikut:

    - Apa kegunaan `{% csrf_token %}` pada elemen `<form>`? Apa yang terjadi apabila tidak ada potongan kode tersebut pada elemen `<form>`?
    - Apakah kita dapat membuat elemen `<form>` secara manual (tanpa menggunakan _generator_ seperti `{{ form.as_table }}`)? Jelaskan secara gambaran besar bagaimana cara membuat `<form>` secara manual.
    - Jelaskan proses alur data dari submisi yang dilakukan oleh pengguna melalui HTML form, penyimpanan data pada _database_, hingga munculnya data yang telah disimpan pada _template_ HTML.
    - Jelaskan bagaimana cara kamu mengimplementasikan _checklist_ di atas.

## Tenggat Waktu Pengerjaan

Tugas ini memiliki tenggat waktu pengumpulan pada tanggal 12 Maret 2023 pada pukul 23.59. Asisten dosen akan mengecek _last commit_ dari repositori tugas lab, sehingga kamu tidak perlu mengumpulkan tautan repositori ke dalam slot submisi.

## Bonus

Kamu akan mendapatkan nilai bonus pada penilaian tugas ini apabila kamu menambahkan _Cookies_ yang menampilkan data _last login_ pada halaman _study tracker_