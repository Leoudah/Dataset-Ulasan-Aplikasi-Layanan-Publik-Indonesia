# Dataset Ulasan Aplikasi Layanan Publik Indonesia

[![DOI](https://zenodo.org/badge/1337572813.svg)](https://doi.org/10.5281/zenodo.21984958)

Dataset ulasan pengguna berbahasa Indonesia dari tiga aplikasi layanan publik digital di Google Play Store: **Identitas Kependudukan Digital (IKD)**, **Mobile JKN**, dan **MyPertamina**. Dataset ini dikumpulkan untuk mendukung penelitian klasifikasi ulasan aplikasi berbasis tipe (Bug Report / Feature Request / Other) dan aspek/modul.

## Sumber Data

| Aplikasi | Package ID (Google Play) |
|---|---|
| IKD | `gov.dukcapil.mobile_id` |
| Mobile JKN | `app.bpjs.mobile` |
| MyPertamina | `com.dafturn.mypertamina` |

## Metode Pengumpulan

- **Tool**: [`google-play-scraper`](https://pypi.org/project/google-play-scraper/) (Python)
- **Parameter**: `sort=Sort.NEWEST`
- **Waktu pengambilan**: 9 Agustus 2026, 18.54 WITA
- **Volume**: 20.000 ulasan per aplikasi → 60.000 ulasan mentah
- **Atribut yang diambil**: ID ulasan, nama aplikasi, teks ulasan, rating, tanggal

## Proses Pembersihan Data

Data mentah dibersihkan melalui tahapan berikut:
1. Deduplikasi
2. Penghapusan ulasan tanpa teks atau hanya berisi emoji
3. Penghapusan konten spam dan promosi

Setelah pembersihan, tersisa **27.142** data bersih dari total 60.000 ulasan mentah.

## Stratified Sampling

Untuk menjaga keseimbangan representasi antaraplikasi, dilakukan *stratified random sampling* sebanyak **2.000 ulasan per aplikasi**, menghasilkan dataset akhir sebanyak **6.000 ulasan**.

## Skema Anotasi

Setiap ulasan diberi dua label independen:

**Label Tipe** (pilih satu, prioritas jika ambigu: Bug Report > Feature Request > Other)
| Label | Definisi |
|---|---|
| Bug Report | Aplikasi tidak berjalan sesuai fungsinya, error, force close, OTP tidak masuk, alur pendaftaran bermasalah/gagal/rusak secara teknis |
| Feature Request | Mengusulkan penambahan/perubahan fitur/alur yang belum ada, atau harapan pengguna agar alur diperbaiki |
| Other | Pujian, hinaan tanpa penjelasan, keluhan non-teknis, ulasan generik/ambigu, tidak actionable |

**Aspek/Modul** (enam kategori)
| Label | Definisi |
|---|---|
| Login/OTP/Verifikasi | Masuk akun, kode OTP, registrasi, lupa password, autentikasi biometrik/PIN, verifikasi KTP/wajah |
| Update Data | Ubah profil, data pribadi, dokumen, pengaturan akun |
| Performa Umum | Loading lambat, force close, crash, bug teknis generik |
| Transaksi | Pembayaran, checkout, riwayat transaksi, metode bayar, saldo |
| Layanan Inti | Fitur utama spesifik aplikasi (mis. KTP/KK/Cetak di IKD; Antrean/Rujukan/BPJS/KIS di Mobile JKN; BBM/Subsidi Tepat/SPBU/Barcode di MyPertamina) |
| Other | Pujian generik, keluhan non-teknis/institusi/kantor fisik, ulasan tidak jelas |

## Proses Anotasi

- **Annotator utama**: Google Gemini 3.6 Flash, diakses melalui API dengan skema keluaran terstruktur (*structured output*)
- **Validasi keandalan**: Fleiss' Kappa terhadap dua annotator manusia pada subset 300 data (5% dari total dataset)
  - Label Tipe: κ = 0,8201
  - Aspek/Modul: κ = 0,8236
  - Kategori kesepakatan: *almost perfect* (0,81–1,00) menurut Landis & Koch

## Struktur File

| Kolom | Deskripsi |
|---|---|
| `id` | ID unik ulasan |
| `nama_aplikasi` | IKD / Mobile JKN / MyPertamina |
| `ulasan` | Teks ulasan pengguna |
| `label_tipe` | Bug Report / Feature Request / Other |
| `aspek_modul` | Salah satu dari enam kategori aspek |

## Lisensi & Penggunaan

Dataset ini disediakan untuk keperluan riset akademik non-komersial di bawah lisensi [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Data bersumber dari ulasan publik pengguna di Google Play Store; identitas nama pengguna (*display name*) **tidak disertakan** dalam dataset ini untuk menjaga privasi.

## Cara Sitasi

```
Leonardo Pramudyo Hutomo,  I Putu Nanda Aditya. (2026). Dataset Ulasan Aplikasi Layanan Publik Indonesia (IKD, Mobile JKN, MyPertamina) 
```

## Kontak

Pertanyaan atau permintaan kolaborasi dapat diarahkan ke [isi kontak/email].
