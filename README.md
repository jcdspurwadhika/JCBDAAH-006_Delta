# Bank Marketing Analysis
## Analisis Hasil dan Strategi Kampanye Telemarketing Bank di Portugal

Proyek analisis data untuk mengevaluasi efektivitas kampanye telemarketing produk **deposito berjangka** pada sebuah institusi perbankan di Portugal.

Analisis mencakup pembersihan data, eksplorasi karakteristik nasabah, evaluasi riwayat kontak dan kondisi ekonomi, serta penyusunan rekomendasi strategi pemasaran berbasis data.


---

## Daftar Isi

- [Tim Proyek](#-tim-proyek)
- [Latar Belakang](#-latar-belakang)
- [Tujuan Analisis](#-tujuan-analisis)
- [Dataset](#-dataset)
- [Struktur Repository](#-struktur-repository)
- [Metodologi](#-metodologi)
- [Temuan Utama](#-temuan-utama)
- [Rekomendasi Strategi](#-rekomendasi-strategi)
- [Simulasi Potensi Konversi](#-simulasi-potensi-konversi)
- [Cara Menjalankan](#-cara-menjalankan)
- [Keterbatasan Analisis](#-keterbatasan-analisis)
- [Kesimpulan](#-kesimpulan)

## Tim Proyek

**Delta Team — JCBDAAH-006**

- Handrady Jonathan
- Michael Heydermans
- Razhar N.J.

## Latar Belakang

Krisis finansial global tahun 2008 memberikan tekanan terhadap likuiditas sektor perbankan Portugal. Salah satu pendekatan untuk memperkuat pendanaan adalah menghimpun dana masyarakat melalui produk deposito berjangka.

Kampanye telemarketing menjadi sarana untuk menawarkan produk tersebut. Namun, tingkat konversi keseluruhan dalam dataset hanya sekitar **11,3%**, sehingga diperlukan evaluasi untuk menentukan:

- Nasabah yang lebih berpotensi menerima penawaran.
- Pola kontak yang lebih efisien.
- Hubungan kondisi ekonomi dengan keberhasilan kampanye.
- Peluang penawaran ulang kepada nasabah dari kampanye sebelumnya.

## Tujuan Analisis

1. Mengidentifikasi karakteristik nasabah dengan tingkat konversi tinggi.
2. Menganalisis hubungan riwayat kampanye dan indikator ekonomi dengan keputusan nasabah.
3. Menyusun rekomendasi segmentasi, saluran komunikasi, dan frekuensi kontak.
4. Mengestimasi potensi konversi melalui simulasi penawaran ulang.

## Dataset

Dataset awal terdiri dari **41.188 baris dan 21 kolom**, termasuk variabel target.

**Variabel target:** `y`
- `yes`: nasabah setuju untuk membuka deposito berjangka.
- `no`: nasabah tidak membuka deposito berjangka.


### Data Dictionary

| Kelompok | Variabel | Deskripsi |
|---|---|---|
| Profil nasabah | `age` | Usia nasabah |
| Profil nasabah | `job` | Jenis pekerjaan |
| Profil nasabah | `marital` | Status pernikahan |
| Profil nasabah | `education` | Tingkat pendidikan |
| Profil nasabah | `default` | Status gagal bayar kredit |
| Profil nasabah | `housing` | Status pinjaman perumahan |
| Profil nasabah | `loan` | Status pinjaman pribadi |
| Kampanye berjalan | `contact` | Saluran komunikasi |
| Kampanye berjalan | `month` | Bulan kontak terakhir |
| Kampanye berjalan | `day_of_week` | Hari kontak terakhir |
| Kampanye berjalan | `duration` | Durasi kontak terakhir dalam detik |
| Kampanye berjalan | `campaign` | Jumlah kontak selama kampanye berjalan |
| Kampanye sebelumnya | `pdays` | Hari sejak kontak pada kampanye sebelumnya; `999` berarti belum pernah dihubungi |
| Kampanye sebelumnya | `previous` | Jumlah kontak sebelum kampanye berjalan |
| Kampanye sebelumnya | `poutcome` | Hasil kampanye sebelumnya |
| Indikator ekonomi | `emp.var.rate` | Tingkat variasi ketenagakerjaan |
| Indikator ekonomi | `cons.price.idx` | Indeks harga konsumen |
| Indikator ekonomi | `cons.conf.idx` | Indeks kepercayaan konsumen |
| Indikator ekonomi | `euribor3m` | Suku bunga Euribor tiga bulan |
| Indikator ekonomi | `nr.employed` | Indikator jumlah tenaga kerja |
| Target | `y` | Keputusan berlangganan deposito berjangka |

## Struktur Repository

File utama proyek:

```text
.
├── README.md
└── Delta_Team_Final_Project_Bank_Marketing_Analysis.ipynb
```


## Metodologi
Digunakan analisis deskriptif

### 1. Data Cleaning

- Mengidentifikasi kategori `unknown` sebagai informasi yang tidak tersedia.
- Mempertahankan `unknown` sebagai kategori tersendiri.
- Menghapus **12 baris duplikat identik**, sehingga tersisa **41.176 baris**.
- Menghapus **4 baris dengan `duration = 0`**, sehingga tersisa **41.172 baris** jika seluruh langkah diterapkan berurutan.

Kolom `default` memiliki proporsi `unknown` tertinggi, sekitar **20,87%**.

### 2. Feature Engineering

| Fitur Baru | Deskripsi |
|---|---|
| `age group` | Kelompok usia: <25, 25–35, 36–55, 56–60, dan >60 tahun |
| `pdaycat` | Penanda apakah nasabah pernah dihubungi pada kampanye sebelumnya |
| `campaign_range` | Kelompok jumlah kontak: 1, 2, 3, 4–5, 6–10, dan 11+ |
| `year` | Estimasi tahun berdasarkan kronologi data dan indikator Euribor |


### 3. Exploratory Data Analysis

Analisis dilakukan terhadap:

- Profil demografi dan kondisi kredit nasabah.
- Frekuensi kontak selama kampanye berjalan.
- Riwayat dan hasil kampanye sebelumnya.
- Hubungan indikator ekonomi dengan tingkat konversi.

**Conversion rate** dihitung sebagai jumlah observasi dengan `y = yes` dibagi total observasi pada kelompok yang dianalisis, kemudian dikalikan 100%.

## Temuan Utama

Angka berikut merujuk pada hasil analisis yang dilaporkan dalam proyek.

### Karakteristik Nasabah

| Segmen | Temuan |
|---|---|
| Student | Tingkat konversi **31,43%** |
| Retired | Tingkat konversi **25,26%** |
| Usia >60 tahun | Tingkat konversi **45,54%** |
| Admin | Menyumbang **1.351 konversi**, atau **29,12%** dari total konversi sukses |
| University degree | Menyumbang **1.669 konversi**, atau **35,98%** dari total konversi sukses |

Segmen dengan tingkat konversi tinggi belum tentu menghasilkan jumlah konversi terbesar. Karena itu, prioritas pemasaran perlu mempertimbangkan **tingkat konversi sekaligus ukuran segmen**.

### Riwayat Kampanye

- Nasabah dengan `poutcome = success` memiliki tingkat konversi **65,11%**.
- Nasabah dengan `previous > 0` memiliki tingkat konversi **26,65%**.
- Nasabah tanpa kontak sebelumnya memiliki tingkat konversi **8,83%**.

**Implikasi:** Riwayat keberhasilan kampanye merupakan indikator penting untuk menentukan prioritas penawaran ulang.

### Saluran dan Frekuensi Kontak

- Saluran **cellular** menyumbang **83,04% dari total konversi sukses**.
- Kelompok dengan satu kontak memiliki tingkat konversi **13,04%**.
- Kelompok dengan lebih dari 10 kontak memiliki proporsi tidak berlangganan sebesar **96,89%**.

> Kontribusi cellular terhadap total konversi bukan berarti tingkat konversi saluran tersebut sebesar 83,04%. Perbandingan efektivitas saluran tetap perlu memperhitungkan total kontak pada masing-masing saluran.

### Kondisi Ekonomi

- Terdapat hubungan negatif antara Euribor tiga bulan dan tingkat konversi dalam data historis.
- Pada periode Euribor sekitar **0,6%–1,4%**, tingkat konversi bulanan tertentu dapat melebihi **50%**.
- Pada periode Euribor sekitar **5%**, tingkat konversi berada pada kisaran **3%–6%**.


## Rekomendasi Strategi

### 1. Prioritaskan Nasabah Berdasarkan Riwayat

- Utamakan nasabah dengan `poutcome = success`.
- Evaluasi nasabah yang pernah dihubungi sebelumnya sebagai kandidat penawaran ulang.
- Gunakan profil demografi sebagai informasi pendukung, bukan satu-satunya dasar seleksi.

### 2. Optimalkan Saluran Komunikasi

- Pertimbangkan cellular sebagai saluran utama.
- Bandingkan conversion rate, biaya per kontak, dan biaya per konversi antarsaluran.
- Hormati persetujuan komunikasi dan preferensi nasabah.

### 3. Kendalikan Frekuensi Kontak

- Uji batas operasional awal sebanyak **maksimal tiga kontak per nasabah**.
- Hentikan kontak jika nasabah menolak atau meminta tidak dihubungi.
- Evaluasi batas kontak melalui eksperimen sebelum diterapkan secara luas.

### 4. Pertimbangkan Kondisi Ekonomi

- Pantau Euribor dan indikator ekonomi lainnya.
- Gunakan kondisi makroekonomi sebagai salah satu masukan untuk perencanaan kampanye.
- Validasi pola historis pada data yang lebih baru.

### 5. Kelola Database Kampanye

- Simpan riwayat kontak, respons, dan hasil penawaran secara terstruktur.
- Evaluasi ulang nasabah yang belum berkonversi berdasarkan relevansi produk dan respons sebelumnya.
- Jangan otomatis memprioritaskan seluruh nasabah yang pernah menolak hanya karena telah dihubungi.

## Simulasi Potensi Konversi

Simulasi dilakukan terhadap observasi yang belum berhasil dikonversi pada periode **Mei 2008–Mei 2009**, berdasarkan pembagian periode dalam analisis.

| Tahap | Hasil |
|---|---:|
| Observasi awal dengan `y = no` | 33.779 |
| Kandidat setelah seleksi | 17.790 |
| Asumsi conversion rate | 34%–44,5% |
| Estimasi konversi tambahan | 6.049–7.917 |


## Cara Menjalankan

### Prasyarat

- Python 3.
- Jupyter Notebook atau Google Colab
- Dataset yang digunakan oleh notebook.
- Library Python sesuai perintah `import` dalam notebook.

sumber dataset:
https://www.kaggle.com/datasets/volodymyrgavrysh/bank-marketing-campaigns-dataset

### Langkah Penggunaan

1. Clone atau unduh repository ini.
2. Pastikan dataset tersedia sebelumnya.
3. Jalankan Google Colab.
4. Buka `Delta_Team_Final_Project_Bank_Marketing_Analysis.ipynb`.
5. Upload dataset/file CSV
6. Jalankan seluruh cell secara berurutan.


## Kesimpulan

Terlihat dari hasil analisa bahwa ada beberapa faktor yang bisa mempengaruhi conversion rate yang harus dipertimbangkan sebagai prioritas sebelum melancarkan kampanye telemarketing agar tidak membuang resource secara sia-sia. 
Diperlukan strategi yang berkesinambungan untuk melakukan kampanye telemarketing berikutnya, jangan menggunakan strategi yang benar-benar terpisah tanpa mempedulikan hasil yang lalu maupun tanpa memperhitungkan 
untuk ke masa depannya lagi.

---

**Delta Team | JCBDAAH-006**
