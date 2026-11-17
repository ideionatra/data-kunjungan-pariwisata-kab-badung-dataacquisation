# Akuisisi Data Jumlah Wisatawan Kabupaten Bandung
## 1. Identitas Pengambil Data

- Nama: **I Made Dio Kartiana Putra**
- NIM: **2501010142**
- Program Studi: Informatika
- Institusi: Institut Bisnis dan Teknologi Indonesia (INSTIKI)
- Mata Kuliah: Akuisisi dan Manajemen Data

---

## 2. Deskripsi Proyek

Proyek ini merupakan tugas praktik individu mata kuliah **Akuisisi dan Manajemen Data (BIFP-243)**, Program Studi Informatika, Institut Bisnis dan Teknologi Indonesia (INSTIKI).

Tujuan proyek adalah mengambil data publik yang berkaitan dengan sektor pariwisata melalui API, memeriksa struktur respons JSON, mengubah data menjadi DataFrame menggunakan Pandas, kemudian menyimpannya ke dalam format CSV.

Dataset yang digunakan berjudul **Jumlah Wisatawan** dengan cakupan data tingkat desa/kelurahan di Kabupaten Bandung.

## 3. Informasi Sumber Data

| Komponen | Keterangan |
|---|---|
| Nama dataset | Jumlah Wisatawan |
| Kode dataset | `DISPAREKRAF/001` |
| Sumber | Satu Data Kabupaten Bandung |
| Penerbit/pengelola | Pemerintah Kabupaten Bandung; kode sumber menunjukkan `DISPAREKRAF` |
| URL portal | https://satudata.bandungkab.go.id/ |
| Endpoint API | https://satudata.bandungkab.go.id/api/dataset/DISPAREKRAF/jumlah-wisatawan |
| Metode akuisisi | REST API menggunakan HTTP GET |
| Format respons | JSON |
| Cakupan | Desa/kelurahan di Kabupaten Bandung |
| Rentang tahun pada data yang diperoleh | 2021–2025 |
| Jumlah record pada hasil pemeriksaan | 1.328 record |
| Jumlah kolom | 13 kolom |

> Catatan: kode sumber pada endpoint adalah `DISPAREKRAF`. Silakan cocokkan nama resmi perangkat daerah/penerbit dengan keterangan yang tercantum pada halaman dataset di portal.

## 4. Waktu Akuisisi

- Tanggal akuisisi: **16 November 2026** .
- Jam akuisisi: **22.24**.


## 5. Metode Akuisisi Data

Akuisisi dilakukan menggunakan Python dan library `requests`. Notebook mengirimkan HTTP GET request ke endpoint API dengan header `User-Agent` dan batas waktu permintaan (`timeout`) selama 20 detik.

Sebelum mengambil data, notebook memeriksa file `robots.txt` pada domain sumber menggunakan `RobotFileParser`. Jika hasil pemeriksaan secara eksplisit menyatakan URL tidak diizinkan, proses dihentikan. Jika `robots.txt` tidak tersedia atau tidak dapat diperiksa, ketentuan penggunaan portal/API tetap perlu diperiksa secara manual.

Setelah request berhasil, notebook:
1. Memeriksa HTTP status code dan `Content-Type`.
2. Mencoba membaca respons sebagai JSON.
3. Menampilkan key utama dan cuplikan struktur JSON.
4. Mengambil nama kolom dari `data_column` dan isi record dari `data_row`.
5. Membentuk DataFrame menggunakan `pandas.DataFrame`.
6. Menampilkan data dan menyimpan DataFrame ke CSV.

### Endpoint dan parameter

Endpoint yang digunakan:

```text
https://satudata.bandungkab.go.id/api/dataset/DISPAREKRAF/jumlah-wisatawan
```

Metode: `GET`

Parameter URL: tidak ada parameter query yang ditambahkan pada notebook. Dataset diambil dari endpoint yang telah ditentukan.

Header yang digunakan:

```text
User-Agent: INSTIKI-BIFP243-Praktikum/1.0 (mahasiswa@instiki.ac.id)
```

Batas waktu request: `20` detik.

## 6. Struktur Dataset

Data yang diperoleh memiliki 13 kolom berikut.

| No. | Nama kolom | Keterangan |
|---:|---|---|
| 1 | `No` | Nomor urut record pada dataset. |
| 2 | `Kode Wilayah` | Kode wilayah administratif. |
| 3 | `Wilayah` | Nama wilayah yang dicatat pada dataset (merujuk pada Kabupaten). |
| 4 | `Tahun` | Tahun pencatatan data kunjungan wisatawan. |
| 5 | `Asal Wisatawan` | Kategori asal wisatawan sebagaimana disediakan sumber. |
| 6 | `Kode Kecamatan` | Kode kecamatan. |
| 7 | `Kecamatan` | Nama kecamatan. |
| 8 | `Kode Desa/Kelurahan` | Kode desa atau kelurahan. |
| 9 | `Desa/Kelurahan` | Nama desa atau kelurahan. |
| 10 | `Bidang Usaha Pariwisata` | Kategori bidang usaha pariwisata. |
| 11 | `Nama Usaha Pariwisata` | Nama usaha pariwisata yang tercatat. |
| 12 | `Alamat` | Alamat usaha pariwisata sebagaimana disediakan sumber. |
| 13 | `Jumlah Kunjungan Wisatawan` | Jumlah kunjungan wisatawan pada record tersebut. |

Beberapa nama usaha dan alamat pada respons sumber ditampilkan dengan penyamaran karakter. Nilai tersebut dipertahankan sesuai respons API dan tidak ditebak atau dilengkapi sendiri.

## 7. Etika dan Batasan Pengambilan Data

- **Sumber publik:** data diambil dari endpoint API pada portal Satu Data Kabupaten Bandung.
- **Pemeriksaan robots.txt:** notebook memeriksa `robots.txt` sebelum request data. Simpan output pemeriksaan tersebut sebagai bukti. Pemeriksaan `robots.txt` bukan pengganti pemeriksaan syarat penggunaan, lisensi, atau ketentuan API.
- **User-Agent:** request menggunakan identitas praktikum yang ditulis pada notebook. Ganti alamat email contoh dengan alamat kampus yang benar-benar digunakan jika diperlukan.
- **Timeout:** setiap request memiliki batas waktu 20 detik.
- **Jumlah request:** notebook melakukan satu request utama ke endpoint dataset, selain request untuk memeriksa `robots.txt`.
- **Jeda request:** notebook ini tidak melakukan pengambilan data berulang atau pagination, sehingga tidak menambahkan jeda antar-request. Jika proses dikembangkan menjadi beberapa request, tambahkan jeda minimal 1 detik sesuai instruksi tugas.
- **Data pribadi:** notebook tidak melakukan pengambilan data kontak pribadi seperti nomor telepon, email, foto, atau akun media sosial perorangan. Jika informasi pribadi ditemukan pada sumber, jangan sertakan dalam dataset.
- **Kredensial:** endpoint yang digunakan tidak memerlukan API key pada kode notebook ini. Jangan menaruh API key atau kredensial lain di notebook/repository.
- **Lisensi dan atribusi:** periksa ketentuan penggunaan atau lisensi yang dicantumkan pada halaman dataset/portal. Informasi lisensi spesifik belum dicantumkan di notebook, sehingga perlu diverifikasi dan ditambahkan sebelum pengumpulan.

## 8. Struktur Folder Proyek

Struktur yang disarankan agar sesuai dengan ketentuan tugas:

```text
rtm1_<NIM>/
├── notebooks/
│   └── scrapping-data-bps.ipynb
├── data/
│   └── raw/
│       └── data_kunjungan_wisata_kabupaten_bandung-16-nov-26.csv
├── docs/
│   ├── provenance.json
│   └── data_ethics_checklist.csv
└── README.md
```

Nama notebook saat ini adalah `scrapping-data-bps.ipynb`. Nama tersebut dapat dipertahankan atau disesuaikan dengan nama sumber data agar lebih jelas.

## 9. Cara Menjalankan Notebook

### Persyaratan

Pastikan Python dan Jupyter Notebook/JupyterLab sudah terpasang. Install library yang digunakan:

```bash
pip install requests pandas beautifulsoup4 lxml ipython
```

### Langkah menjalankan

1. Unduh atau clone repository proyek.
2. Pastikan struktur folder `notebooks/` dan `data/raw/` sudah tersedia.
3. Buka file `scrapping-data-bps.ipynb` menggunakan Jupyter Notebook atau JupyterLab.
4. Jalankan seluruh cell dari atas ke bawah.
5. Periksa hasil pemeriksaan `robots.txt` dan pastikan ketentuan penggunaan sumber telah dipenuhi.
6. Pastikan request API berhasil dan respons dapat dibaca sebagai JSON.
7. Periksa jumlah record dan kolom pada DataFrame.
8. Periksa folder `data/raw/` untuk memastikan file CSV berhasil dibuat.

Notebook menggunakan path relatif `../data/raw/`. Karena itu, jalankan notebook dengan direktori kerja di folder `notebooks/`, dan pastikan folder `data/raw/` sudah dibuat. Jika folder belum tersedia, tambahkan kode berikut sebelum proses penyimpanan CSV:

```python
os.makedirs(folder, exist_ok=True)
```

## 10. Hasil Akuisisi

Berdasarkan respons API yang diperiksa, dataset berisi **1.328 record dan 13 kolom**, dengan rentang tahun 2021 sampai 2025. Jumlah tersebut telah melampaui target minimal tugas, yaitu 100 record dan minimal 5 kolom bermakna.

File hasil akuisisi disimpan dalam format CSV dengan encoding `utf-8-sig` agar lebih kompatibel ketika dibuka menggunakan Microsoft Excel.

Nama file:

```text
data_kunjungan_wisata_kabupaten_bandung-16-nov-26.csv
```

Data pada folder `data/raw/` merupakan data hasil akuisisi mentah. Jangan mengubah isi file tersebut; proses pembersihan dan transformasi dilakukan pada tahap/tugas berikutnya.



## Catatan Sebelum Pengumpulan

Sesuai instruksi Tugas 1, README merupakan salah satu bagian dokumentasi. Lengkapi hal-hal berikut sebelum repository dikumpulkan:

- [ ] Isi jam akuisisi yang sebenarnya.
- [ ] Isi nama lengkap dan NIM.
- [ ] Verifikasi nama resmi penerbit/perangkat daerah pada portal.
- [ ] Cantumkan lisensi atau ketentuan penggunaan yang benar-benar berlaku.
- [ ] Simpan bukti hasil pemeriksaan `robots.txt` dan ketentuan API.
- [ ] Buat `docs/provenance.json` yang memuat nama berkas, ukuran, hash MD5, sumber, URL, lisensi, waktu akuisisi, serta nama/NIM pengambil.
- [ ] Isi `docs/data_ethics_checklist.csv` berdasarkan 9 butir checklist pada Modul 04 beserta buktinya.
- [ ] Jalankan ulang notebook dari awal dan pastikan tidak ada API key atau kredensial di dalamnya.
