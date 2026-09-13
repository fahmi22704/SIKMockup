# SIMRS GROUP 2 SIK — RS OTTEN 32

Prototipe antarmuka **Sistem Informasi Manajemen Rumah Sakit (SIMRS)** untuk RS Otten 32. Dibangun sebagai satu file HTML statis (dengan CSS & JavaScript inline) — cocok untuk demo, uji coba alur kerja, atau dasar pengembangan lebih lanjut.

## Cara Menjalankan

Tidak perlu instalasi atau server khusus.

1. Buka file `index.html` langsung di browser (double click), **atau**
2. Jalankan local server sederhana lalu buka di browser:
   ```bash
   python3 -m http.server 8000
   # lalu buka http://localhost:8000
   ```

## Login

Aplikasi selalu dimulai dari layar login. Isi bebas — nama pengguna & kata sandi apa saja diterima (data dummy, belum terhubung ke backend).

Pilih salah satu peran sebelum masuk:

| Peran | Deskripsi |
|---|---|
| 🧑‍💼 Staff | Admin/petugas administrasi |
| 🩺 Dokter | Tenaga medis dokter |
| ➕ Nakes | Tenaga kesehatan (perawat, dll) |

Menu di sidebar akan otomatis menyesuaikan (tampil/sembunyi) berdasarkan peran yang dipilih.

## Struktur Halaman

| Menu | data-page | Akses Peran |
|---|---|---|
| Dashboard | `dashboard` | Staff, Dokter, Nakes |
| Pendaftaran | `pendaftaran` | Staff |
| Rawat Jalan | `rawat-jalan` | Staff, Dokter, Nakes |
| Rawat Inap | `rawat-inap` | Staff, Dokter, Nakes |
| Persetujuan Rawat Inap | `persetujuan-rawat-inap` | Staff, Dokter, Nakes |
| Rujukan | `rujukan` | Staff, Dokter, Nakes |
| IGD | `igd` | Staff, Dokter, Nakes |
| Farmasi | `farmasi` | Staff, Nakes |
| Laboratorium | `laboratorium` | Staff, Dokter, Nakes |
| Keuangan | `keuangan` | Staff |
| Laporan | `laporan` | Staff |
| Pengaturan | `pengaturan` | Staff |

### Ringkasan Fungsi per Halaman

- **Dashboard** — ringkasan okupansi ranjang seluruh ruangan, antrean per poli, pasien rawat inap terbaru, dan daftar peringatan operasional (stok, hasil lab, dsb).
- **Pendaftaran** — formulir pendaftaran kunjungan baru + daftar antrean verifikasi berkas.
- **Rawat Jalan** — antrean pemeriksaan poli hari ini.
- **Rawat Inap** — okupansi ranjang per ruangan (grid visual) + daftar pasien rawat inap aktif.
- **Persetujuan Rawat Inap** — formulir *informed consent* admisi (data pasien, ruangan, dokter penanggung jawab, pemberi persetujuan, hubungan dengan pasien, diagnosis, checkbox persetujuan) + riwayat formulir yang sudah diisi.
- **Rujukan** — formulir rujukan pasien (rujukan keluar/masuk/internal antar poli, asal & tujuan fasilitas, dokter perujuk, diagnosis & alasan) + daftar rujukan berjalan.
- **IGD** — status kapasitas, jumlah pasien menunggu dokter, rata-rata waktu tangani, dan daftar triase aktif.
- **Farmasi** — status stok obat & alat kesehatan.
- **Laboratorium** — antrean pemeriksaan penunjang.
- **Keuangan** — ringkasan pendapatan harian, klaim BPJS, piutang, dan transaksi terbaru.
- **Laporan** — daftar laporan operasional/keuangan yang dapat diunduh.
- **Pengaturan** — profil rumah sakit dan manajemen pengguna sistem.

## Teknologi

- **HTML5** — struktur halaman, semua halaman berada dalam satu file (`<div class="page" data-page="...">`), ditampilkan/disembunyikan lewat JavaScript tanpa reload.
- **CSS murni** (custom, tanpa framework) — desain berbasis CSS variables (`:root`) untuk warna, radius, dan shadow agar mudah dikustomisasi.
- **Font**: [IBM Plex Sans](https://fonts.google.com/specimen/IBM+Plex+Sans) & [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono) via Google Fonts.
- **JavaScript vanilla** (tanpa library) untuk:
  - Jam berjalan (live clock)
  - Render grid ranjang secara terprogram (`renderBeds()`)
  - Navigasi antar halaman tanpa reload (`goToPage()`)
  - Alur login/logout & filter menu berdasarkan peran (`applyRoleAccess()`)

## Catatan Penting

⚠️ Ini adalah **prototipe front-end statis**:

- Semua data (pasien, stok, transaksi, dsb.) bersifat **dummy/hardcoded** di dalam HTML.
- Form (pendaftaran, persetujuan rawat inap, rujukan, dll.) **belum terhubung ke backend/database** — tombol submit belum menyimpan data secara nyata.
- Login menerima kredensial apa saja tanpa validasi terhadap server.
- Cocok digunakan untuk: demo alur kerja, mockup UI/UX, atau titik awal integrasi dengan backend (REST API, database, dsb).

## Struktur File

```
index.html   # seluruh aplikasi (HTML + CSS + JS) dalam satu file
```

## Pengembangan Lanjutan (Saran)

- Hubungkan formulir ke backend/API (misal Node.js/Express, Laravel, atau lainnya) dan database (MySQL/PostgreSQL) untuk penyimpanan data sungguhan.
- Tambahkan autentikasi & otorisasi sungguhan (JWT/session) menggantikan login dummy saat ini.
- Tambahkan validasi input pada tiap formulir.
- Pertimbangkan migrasi ke framework front-end (React/Vue) jika kompleksitas aplikasi bertambah.
