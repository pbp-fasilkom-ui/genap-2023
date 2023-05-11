# Tugas 9: Integrasi Web Service dengan Aplikasi Flutter

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer, Universitas Indonesia, Semester Genap 2022/2023

---

## Deskripsi Tugas

Pada tugas ini, kamu akan mengintegrasikan servis Django yang sudah kamu buat pada tugas-tugas sebelumnya dengan aplikasi Flutter yang sudah kamu buat sebelumnya.

*Checklist* untuk tugas ini adalah sebagai berikut.

- Migrasi proyek tugas Django kamu ke salah satu PaaS alternatif.

- Membuat halaman login pada proyek tugas Flutter.

- Mengintegrasikan sistem autentikasi Django dengan proyek tugas Flutter.

- Membuat model kustom sesuai dengan proyek aplikasi Django.

- Membuat halaman yang berisi semua tugas yang ada pada *endpoint* `JSON` di Django yang telah kamu *deploy* sebelumnya. Pada bagian ini, kamu cukup menampilkan judul, mata kuliah, dan tanggal tambah tugas.

    ![Tugas](https://i.ibb.co/W2qQN3f/contoh-tugas.png)

- Membuat halaman detail untuk setiap tugas yang ada pada daftar tersebut. Halaman ini menampilkan judul, mata kuliah, tanggal, progress, dan deskripsi tugas. Halaman ini diakses dengan menekan tugas pada halaman daftar tugas.

- Menambahkan tombol untuk kembali ke daftar tugas.

    ![Detail](https://i.ibb.co/VCQz3xq/Tugas-9.png)

-  Menjawab beberapa pertanyaan berikut pada `README.md` pada *root folder* (silakan modifikasi `README.md` yang telah kamu buat sebelumnya; tambahkan subjudul untuk setiap tugas).

    - Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?

    - Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.

    - Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.

    - Sebutkan seluruh *widget* yang kamu pakai pada tugas ini dan jelaskan fungsinya masing-masing.

    - Jelaskan bagaimana cara kamu mengimplementasikan *checklist* di atas secara *step-by-step* (bukan hanya sekadar mengikuti tutorial).

-  Melakukan `add`-`commit`-`push` ke GitHub.

## Tenggat Waktu Pengerjaan

Tugas ini memiliki tenggat waktu pengumpulan pada tanggal **21 Mei 2023** pada pukul 23.59. Asisten dosen akan mengecek *last commit* dari repositori tugas lab, sehingga kamu tidak perlu mengumpulkan tautan repositori ke dalam slot submisi.

## Bonus

Kamu akan mendapatkan nilai bonus pada penilaian tugas ini apabila kamu mengimplementasikan fitur registrasi akun pada tugas ini.
