# Tugas 2: Pengenalan Aplikasi Django dan Models View Template (MVT) pada Django

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer Universitas Indonesia, Semester Genap 2022/2023

---

## Deskripsi Tugas

Pada tugas ini, kamu akan mengimplementasikan konsep Model-View-Template serta beberapa hal yang sudah kamu pelajari di kelas dan tutorial lab. Kamu dapat menyelesaikan tugas ini dengan memanfaatkan [_source code_ berikut](https://github.com/determinedguy/django-railway-template). Silakan baca dan ikuti petunjuk penggunaan _source code_ templat pada file `README.md`.

Adapun pada tugas ini, kamu diminta untuk:

1. Membuat sebuah aplikasi baru pada proyek tersebut bernama `study_tracker`.

2. Melakukan `routing` pada `django_project` agar dapat menjalankan aplikasi `study_tracker`.

3. Membuat model pada aplikasi `study_tracker` yang bernama `Assignment` dan memiliki atribut sebagai berikut.

    - `name` untuk nama tugas dengan tipe `CharField`,
    - `subject` untuk mata kuliah tugas dengan tipe `CharField`,
    - `date` untuk waktu input tugas dengan tipe `DateTimeField`,
    - `progress` untuk indikator _progress_ tugas dengan tipe `IntegerField`,
    - `description` untuk deskripsi tugas dengan tipe `TextField`.

4. Membuat sebuah fungsi pada `views.py` yang dapat melakukan pengambilan data dari model yang telah dibuat sebelumnya dan dikembalikan ke dalam sebuah HTML.

5. Membuat sebuah routing pada `urls.py` aplikasi `study_tracker` untuk memetakan fungsi yang telah dibuat pada `views.py`.

6. Memetakan data yang didapatkan ke dalam HTML dengan sintaks dari Django untuk pemetaan data _template_ (dapat menggunakan _template_ yang diberikan pada tutorial 1, namun sesuaikan atribut data sesuai dengan model yang telah dibuat).

7. Melakukan `deployment` ke Railway terhadap aplikasi yang sudah dibuat sehingga nantinya dapat diakses oleh teman-temanmu melalui Internet.

8. Membuat sebuah `README.md` yang berisi tautan menuju aplikasi Railway yang sudah di-_deploy_ (jika dapat di-_deploy_) serta jawaban dari beberapa pertanyaan berikut.

    - Buatlah bagan yang berisi _request client_ ke web aplikasi berbasis Django beserta responnya dan jelaskan pada bagan tersebut kaitan antara `urls.py`, `views.py`, `models.py`, dan berkas `html`.
    - Jelaskan kenapa menggunakan _virtual environment_? Apakah kita tetap dapat membuat aplikasi web berbasis Django tanpa menggunakan _virtual environment_?
    - Jelaskan bagaimana cara kamu mengimplementasikan poin 1 sampai dengan 4 di atas.

Perhatikan bahwa kamu harus mengerjakan tugas ini menggunakan **repositori berbeda** dengan tutorial.

## Tenggat Waktu Pengerjaan

Tugas ini memiliki tenggat waktu pengumpulan pada tanggal **26 Februari 2023** pada pukul **23.59**. Harap mengumpulkan link repositori yang kamu gunakan ke dalam slot submisi yang telah disediakan di SCELE.

## Bonus

Kamu akan mendapatkan nilai bonus pada penilaian tugas ini apabila kamu berhasil mengimplementasikan dan mendemonstrasikan _testing_ dasar (contoh: _unit testing_, _functional testing_, dan lain-lain). Silakan cari di Google untuk melihat cara membuat _testing_ di Django.
