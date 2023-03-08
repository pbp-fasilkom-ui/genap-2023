# Proyek Tengah Semester PBP

**Membuat Situs Web menggunakan _Framework_ Django secara Berkelompok**

## Tujuan Pembelajaran Khusus

- Merancang halaman web
- Mengimplementasikan situs web dengan _framework_ Django dengan memenuhi _models_, _views_, dan _templates_
- Memanfaatkan _framework_ CSS untuk mewujudkan _responsive web design_
- Mengimplementasikan _unit test_ dan _deployment_ **(bonus)**

### Catatan

Perlu diperhatikan bahwa selain tujuan pembelajaran khusus seperti yang tertulis di atas, peserta kuliah juga perlu mempelajari dan dilatih beberapa aspek kecendekiaan sebagai calon sarjana. Di antaranya yang relevan dalam kuliah ini adalah keteguhan (_grit_), kemandirian, ketelitian, termasuk juga metakognitif (secara sederhana bisa diartikan kemampuan mengatur strategi belajar yang sesuai dengan dirinya meliputi perencanaan, pengawasan dan evaluasi proses belajar mandiri), termasuk di dalamnya kemampuan untuk memahami, mengomunikasikan masalah, diskusi dan bertanya sehingga peserta kuliah juga perlu siap bersikap positif dengan kondisi-kondisi yang secara tidak langsung atau tidak pasti akan dihadapi dan mungkin dapat menghabiskan banyak waktu. Kondisi tersebut bisa dianggap kendala, seperti keterbatasan sumber daya, _bug tools_, kesulitan teknis atau lainnya. Walaupun dirasakan menyulitkan, perlu diupayakan untuk disikapi dengan positif agar dapat menjadi manfaat terkait aspek kecendekiaan yang perlu dilatih peserta kuliah. Sikap negatif hanya akan memperburuk keadaan dan menghilangkan manfaat tugas ini untuk pembelajaran yang akan dapat dirasakan di kemudian hari. Tim asisten dan dosen melalui sarana yang ada, akan berusaha semampunya melayani pertanyaan, keluhan, dan membantu proses pembelajaran peserta agar peserta bisa menjalani perkuliahan dan belajar semaksimal mungkin.

Sebagai selingan, bila rekan-rekan lelah dan bingung menghadapi _error_ yang belum kunjung terselesaikan, berikut ini ada video yang cukup populer dan mudah-mudahan bisa menambah semangat untuk tetap teguh mengerjakan dan berlatih demi kesuksesan di kemudian hari.

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/42-hh-iMJJI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe><br /><br />

Selamat mengerjakan. 😃

## Aturan Umum Tugas Kelompok  

1. Satu kelompok terdiri atas 5-6 orang. Pembagian kelompok dapat dilihat di SCELE.
2. Satu kelompok membuat satu repositori git yang digunakan oleh seluruh anggota kelompok untuk bekerja sama. Kumpulkan tautan repositori git ke SCELE.
3. Setiap kelompok dipersilakan mencari ide sendiri mengenai aplikasi yang akan dibuat. Mahasiswa dapat berdiskusi dengan anggota kelompok dan berkonsultasi dengan asisten dosen untuk menentukan ide aplikasi yang akan dibuat.
4. Setiap anggota kelompok mengerjakan modul yang berbeda. Modul ditentukan oleh kelompok yang disesuaikan dengan ide aplikasi yang sudah didiskusikan dalam kelompok.
5. Tugas kelompok di-_deploy_ sebagai kesatuan aplikasi web dalam satu Railway _app_.

## Aturan Khusus per Anggota Kelompok

Setiap anggota kelompok wajib mengimplementasikan sebuah modul.

1. Menerapkan models dengan membuat, memanfaatkan yang sudah disediakan Django, atau memanfaatkan yang sudah dibuat oleh anggota kelompok (pada modul lain).
2. Menerapkan views untuk memproses request dan mengolah data untuk menghasilkan respons menggunakan templat HTML maupun mengembalikan respon JSON.
3. Menerapkan templates menggunakan responsive framework (contohnya Bootstrap atau Tailwind).
4. Memiliki halaman form yang dapat menerima masukan dari pengguna dan kemudian diproses oleh views. Contoh pemrosesan oleh views adalah insert ke dalam model, query dari model, dan update data di dalam model.
5. Menerapkan JavaScript dengan pemanggilan AJAX.
6. Menerapkan filter informasi bagi pengguna yang sudah login saja. Contohnya adalah data alamat, umur, dan nomor handphone hanya dapat dilihat oleh pengguna yang sudah login saja.

## Tahapan Tugas Kelompok

<table>
    <tr>
        <th>Tahapan dan <em>deliverables</em></th>
        <th>Tenggat Waktu dan Keterangan</th>
    </tr>
    <tr>
        <td>
            <b>Tahap I (40%)</b>
            <ul>
                <li>Pembuatan GitHub kelompok</li>
                <li>Pembuatan aplikasi Railway kelompok</li>
                <li>README.md pada GitHub yang berisi:</li>
                    <ol>
                        <li>Nama-nama anggota kelompok</li>
                        <li>Tautan aplikasi Railway</li>
                        <li>Cerita aplikasi yang diajukan serta manfaatnya</li>
                        <li>Daftar modul yang akan diimplementasikan</li>
                    </ol>
                <li><em>Role</em> atau peran pengguna beserta deskripsinya (karena bisa saja lebih dari satu jenis pengguna yang mengakses aplikasi)</li>
            </ul>
        </td>
        <td>
            <b>Tenggat Waktu:</b>
            <b style="color:red;">Minggu, 26 Maret 2023, pukul 23:59 WIB</b>
            <br />
            <b>Kumpulkan tautan GitHub dan Railway</b> dengan <em>code base</em> proyek Django yang sudah disiapkan di GitHub.
            <br />
            <br />
            <p><b>Kriteria Submisi:</b> <em>Code base</em> proyek Django sudah muncul di Railway (minimal Hello World)</p>
        </td>
    </tr>
    <tr>
        <td>
            <b>Tahap II (60%)</b>
            <p>(Modul sudah terimplementasi dengan baik)</p>
            <ul>
                <li>Modul aplikasi dari tiap anggota kelompok</li>
                <li><em>URL Mapping</em> untuk modul</li>
                <li><em>Models</em> untuk modul</li>
                <li><em>Views</em> untuk modul</li>
                <li>Terintegrasi sebagai satu kesatuan aplikasi</li>
                <li>Fungsionalitas sesuai dengan rancangan desain</li>
            </ul>
        </td>
        <td>
            <b>Tenggat Waktu:</b>
            <b style="color:red;">Minggu, 23 April 2023, pukul 23:59 WIB</b>
            <br />
            <p><b>Kriteria Submisi:</b> Seluruh modul yang dikerjakan oleh setiap anggota kelompok sudah muncul dan dapat diakses pada proyek Django</p>
        </td>
    </tr>
    <tr>
        <td>
            <b>Bonus (5%)</b>
            <ul>
                <li>Unit Test (<em>passed</em>) untuk semua aspek, diharapkan <em>code coverage</em> bisa mencapai minimal 80%</li>
                <li>GitHub Actions (CI/CD) sudah terkonfigurasi hingga <em>deployment</em></li>
                <li>README.md pada GitHub yang berisi <em>pipeline status</em></li>
            </ul>
        </td>
        <td></td>
    </tr>
</table>