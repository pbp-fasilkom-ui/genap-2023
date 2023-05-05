# Tugas 8: Flutter Form

Pemrograman Berbasis Platform (CSGE602022) - diselenggarakan oleh Fakultas Ilmu Komputer, Universitas Indonesia, Semester Genap 2022/2023

---

## Deskripsi Tugas

Pada tugas ini, kamu akan membuat `Form` untuk aplikasi *study tracker* yang sudah kamu buat pada tugas sebelumnya.

*Checklist* untuk tugas ini adalah sebagai berikut.

- Menambahkan *drawer/hamburger* menu pada app yang telah dibuat sebelumnya.
- Menambahkan dua tombol navigasi pada *drawer/hamburger*.

    - Navigasi pertama untuk ke halaman menu.
    - Navigasi kedua untuk ke halaman form tambah tugas.

- Menambahkan halaman form

    - Menambahkan elemen input `TextField` dengan tipe data `String` berupa nama tugas.
    - Menambahkan elemen input `TextField` dengan tipe data `String` berupa nama mata kuliah.
    - Menambahkan elemen input `TextField` dengan tipe data `Integer` berupa persentase *progress*.
    - Menambahkan elemen input `TextField` dengan tipe data `String` berupa deskripsi tugas.

    > Catatan: Silakan sesuaikan form di atas dengan form yang sudah dibuat pada tugas sebelumnya (jika ada atribut tambahan).

- Menampilkan *popup* berisi informasi data yang diisi pada form ketika tombol tambah ditekan.

    > Data yang ditampilkan berupa nama tugas, mata kuliah, persentase *progress*, dan deskripsi tugas.

- Mengubah fungsi tombol `Tambah Tugas` pada halaman menu untuk mengarahkan pengguna ke halaman form saat tombol ditekan.

    > Catatan: Gunakan `Navigator.pushReplacement` untuk mengimplementasikan poin ini.

- Menjawab beberapa pertanyaan berikut pada `README.md` pada *root folder* (silakan modifikasi `README.md` yang telah kamu buat sebelumnya; tambahkan subjudul untuk setiap tugas).

    - Jelaskan bagaimana cara kerja `Navigator` dalam "mengganti" halaman dari aplikasi Flutter.
    - Sebutkan dan jelaskan tipe *routing* yang disediakan oleh `Navigator`.
    - Sebutkan jenis-jenis *event* yang ada pada Flutter (contoh: `onPressed`).
    - Sebutkan seluruh *widget* yang kamu pakai di proyek kali ini dan jelaskan fungsinya masing-masing.
    - Jelaskan bagaimana cara kamu mengimplementasikan *checklist* di atas secara *step-by-step* (bukan hanya sekadar mengikuti tutorial).

- Melakukan `add`-`commit`-`push` ke GitHub.

## Tenggat Waktu Pengerjaan

Tugas ini memiliki tenggat waktu pengumpulan pada tanggal **14 Mei 2023** pada pukul 23.59. Asisten dosen akan mengecek *last commit* dari repositori tugas lab, sehingga kamu tidak perlu mengumpulkan tautan repositori ke dalam slot submisi.

## Bonus

Kamu akan mendapatkan nilai bonus pada penilaian tugas ini apabila kamu membuat fitur berikut.

- Mengimplementasikan prinsip *clean architecture* dengan menerapkan *refactor* sesuai dengan tutorial 7.
- Mengganti ikon *launcher* menjadi *custom icon*.

    > Kamu dapat menggunakan paket [flutter_launcher_icons](https://pub.dev/packages/flutter_launcher_icons) untuk mengerjakan poin ini.
