# Tugas 3: Pengimplementasian Data Delivery Menggunakan Django

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer Universitas Indonesia, Semester Genap 2022/2023

---

## Deskripsi Tugas

Pada tugas ini, kamu akan mengimplementasikan konsep _form_ dan _data delivery_ serta beberapa hal yang sudah kamu pelajari selama tutorial.

Adapun pada tugas ini, kamu diminta untuk:

1. Membuat sebuah _form_ dengan membuat file `forms.py` pada aplikasi `study_tracker` agar aplikasi dapat menambah data tugas. Sesuaikanlah `fields` pada file `forms.py` dengan `models` yang sudah dibuat pada lab sebelumnya.

2. Membuat fungsi baru pada `views.py` untuk menambahkan data tugas pada _form_ secara otomatis.

3. Membuat _file_ HTML baru yang menampilkan _form_ untuk menambahkan data tugas baru.

4. Modifikasi _file_ HTML yang menampilkan tabel tugas dengan menambahkan _button_ untuk menuju ke halaman _form_.

5. Mengimplementasi sebuah fitur untuk menyajikan data yang telah dibuat sebelumnya dalam dua format:

    - XML
    - JSON

6. Membuat _routing_ sehingga data di atas dapat diakses melalui URL:

    - <http://localhost:8000/study_tracker/xml> untuk mengakses `Assignment` dalam format XML
    - <http://localhost:8000/study_tracker/json> untuk mengakses `Assignment` dalam format JSON

7. Membuat sebuah `README.md` yang berisi tautan menuju aplikasi Railway yang sudah kamu _deploy_ (jika dapat di-_deploy_) serta jawaban dari beberapa pertanyaan berikut:

    - Apakah kita dapat menginput data selain melalui _form_? Namun mengapa _form_ dapat dikatakan lebih baik daripada menggunakan cara tersebut?
    - Jelaskan perbedaan antara JSON, XML, dan HTML!
    - Jelaskan mengapa kita memerlukan _data delivery_ dalam pengimplementasian sebuah platform.
    - Jelaskan bagaimana cara kamu mengimplementasikan _checklist_ di atas.

## Tenggat Waktu Pengerjaan

Tugas ini memiliki tenggat waktu pengumpulan pada tanggal 5 Maret 2023 pada pukul 23.59. Asisten dosen akan mengecek _last commit_ dari repositori tugas lab, sehingga kamu tidak perlu mengumpulkan tautan repositori ke dalam slot submisi.

## Bonus

Kamu akan mendapatkan nilai bonus pada penilaian tugas ini apabila kamu membuat teks pada halaman tugas yang menampilkan: "Hai {nama}, kamu memiliki {jumlah_tugas} tugas yang harus dikerjakan!". Lokasi teks dapat berada di atas atau di bawah halaman tugas.
