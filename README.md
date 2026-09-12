# SIMRS GROUP 2 SIK — RS OTTEN 32

Dashboard operasional Sistem Informasi Manajemen Rumah Sakit (SIMRS) dalam bentuk **satu file HTML statis** (Single Page Application). Proyek ini adalah **prototipe front-end/demo** — semua data yang tampil adalah data contoh (dummy), dan belum terhubung ke server atau database sungguhan.

## Daftar Isi

- [Fitur](#fitur)
- [Struktur File](#struktur-file)
- [Cara Menjalankan](#cara-menjalankan)
- [Deploy ke GitHub Pages](#deploy-ke-github-pages)
- [Login & Hak Akses per Peran](#login--hak-akses-per-peran)
- [Daftar Halaman/Menu](#daftar-halamanmenu)
- [Kustomisasi](#kustomisasi)
- [Batasan (Yang Belum Ada)](#batasan-yang-belum-ada)
- [Rencana Pengembangan Lanjutan](#rencana-pengembangan-lanjutan)

## Fitur

- **Single Page Application (SPA)** — perpindahan antar menu terjadi tanpa reload halaman.
- **Login berbasis peran** — tiga peran pengguna: Staff, Dokter, dan Nakes (Tenaga Kesehatan), masing-masing dengan menu yang berbeda.
- **Dashboard ringkasan** — jumlah kunjungan, antrian aktif, okupansi ranjang, dan pendapatan harian.
- **Visualisasi okupansi ranjang** per ruangan (Melati, Anggrek, Dahlia, ICU, IGD, Mawar) dalam bentuk grid kotak.
- **10 halaman/menu** operasional rumah sakit (lihat [Daftar Halaman/Menu](#daftar-halamanmenu)).
- **Jam berjalan otomatis** di topbar.
- Desain responsif dasar (sidebar menyusut pada layar sempit).
- Tidak menggunakan framework atau build tool apa pun — murni HTML, CSS, dan JavaScript vanilla dalam satu file.

## Struktur File

```
index.html   → seluruh aplikasi (markup, styling, dan logika JavaScript)
README.md    → dokumentasi ini
```

Semua kode (HTML, CSS di dalam tag `<style>`, dan JavaScript di dalam tag `<script>`) berada dalam satu file `index.html` agar mudah di-hosting di mana saja, termasuk GitHub Pages, tanpa proses build.

## Cara Menjalankan

**Secara lokal**, tidak perlu instalasi apa pun:

1. Unduh file `index.html`.
2. Klik dua kali file tersebut, atau buka lewat browser (klik kanan → *Open with* → pilih browser).
3. Aplikasi langsung berjalan di layar login.

## Deploy ke GitHub Pages

1. Buat repository baru di GitHub (atau gunakan repository yang sudah ada).
2. Upload file `index.html` ke **root** repository (bukan di dalam subfolder, kecuali kamu memang ingin memakai folder `/docs`).
3. Buka **Settings → Pages** pada repository tersebut.
4. Pada bagian **Build and deployment**, pilih:
   - Source: `Deploy from a branch`
   - Branch: `main` (atau branch tempat file di-upload), folder `/root`
5. Simpan, lalu tunggu 1–3 menit hingga proses build selesai (cek tab **Actions**).
6. Akses situs melalui URL yang muncul, biasanya berformat:
   - `https://<username>.github.io/<nama-repo>/`

> Jika halaman menampilkan 404, periksa kembali: nama file harus persis `index.html` (huruf kecil), berada di folder root/`docs` sesuai pengaturan Pages, dan proses build di tab Actions sudah selesai.

## Login & Hak Akses per Peran

Layar login berada di paling awal saat aplikasi dibuka. Pilih salah satu peran, isi nama pengguna dan kata sandi (bebas, karena ini demo tanpa server autentikasi), lalu klik **Masuk**.

| Peran   | Menu yang Bisa Diakses |
|---------|------------------------|
| **Staff** | Semua menu (akses penuh): Dashboard, Pendaftaran, Rawat Jalan, Rawat Inap, IGD, Farmasi, Laboratorium, Keuangan, Laporan, Pengaturan |
| **Dokter** | Dashboard, Rawat Jalan, Rawat Inap, IGD, Laboratorium |
| **Nakes** (perawat/tenaga kesehatan) | Dashboard, Rawat Jalan, Rawat Inap, IGD, Farmasi, Laboratorium |

Setelah login, nama dan peran pengguna tampil di pojok kanan atas (topbar). Tombol **Keluar** di sebelahnya akan mengembalikan ke layar login.

> Catatan: karena ini prototipe front-end tanpa backend, sesi login **tidak tersimpan** setelah halaman di-refresh — pengguna akan diminta login kembali. Validasi username/password juga hanya mengecek bahwa kolomnya tidak kosong, bukan mencocokkan ke basis data pengguna sungguhan.

## Daftar Halaman/Menu

| Menu | Isi |
|------|-----|
| Dashboard | Ringkasan kunjungan hari ini, antrian aktif, okupansi ranjang, pendapatan, okupansi per ruangan, antrian per poli, pasien rawat inap terbaru, dan daftar peringatan operasional |
| Pendaftaran | Formulir pendaftaran pasien baru dan daftar pendaftaran yang menunggu verifikasi berkas |
| Rawat Jalan | Antrean pemeriksaan poli hari ini beserta status tiap pasien |
| Rawat Inap | Grid okupansi ranjang per ruangan dan daftar pasien rawat inap yang sedang aktif |
| IGD | Statistik kapasitas IGD dan daftar pasien berdasarkan level triase (Merah/Kuning/Hijau) |
| Farmasi | Tabel stok obat dan alat kesehatan beserta status ketersediaannya |
| Laboratorium | Antrean pemeriksaan penunjang (lab, radiologi) dan statusnya |
| Keuangan | Ringkasan pendapatan, klaim BPJS, piutang, dan daftar transaksi terbaru |
| Laporan | Daftar laporan yang tersedia untuk diunduh (kunjungan, okupansi, keuangan, stok) |
| Pengaturan | Profil rumah sakit dan daftar pengguna sistem |

## Kustomisasi

Karena semuanya berada dalam satu file `index.html`, beberapa hal yang mudah diubah:

- **Nama rumah sakit / sistem** — cari teks `RS OTTEN 32` dan `SIMRS GROUP 2 SIK`, ganti sesuai kebutuhan (muncul di beberapa tempat: judul tab, logo sidebar, layar login, dan halaman Pengaturan).
- **Warna tema** — ubah nilai warna pada bagian `:root { ... }` di dalam tag `<style>` (variabel seperti `--teal`, `--teal-deep`, `--bg`, dll).
- **Data okupansi ranjang** — cari pemanggilan fungsi `renderBeds('idRuangan', totalRanjang, terisi, dibersihkan)` di bagian `<script>`, ubah angkanya sesuai data nyata.
- **Menu per peran** — cari atribut `data-roles="..."` pada setiap `<li>` di sidebar, tambahkan/kurangi peran yang dipisah spasi (`staff`, `dokter`, `nakes`).
- **Isi tabel** (pasien, transaksi, stok obat, dll) — semuanya berupa baris `<tr>` biasa di dalam `<table>`, bisa diedit langsung sesuai data yang ingin ditampilkan.

## Batasan (Yang Belum Ada)

- Belum terhubung ke server/API/database — semua data bersifat statis (hardcoded) di dalam HTML.
- Login belum memvalidasi ke sistem autentikasi sungguhan (tidak ada pengecekan password ke database, tidak ada enkripsi, dan sesi tidak tersimpan setelah refresh).
- Formulir (misalnya Pendaftaran Pasien, Pengaturan Profil) belum benar-benar menyimpan data — tombol submit belum terhubung ke penyimpanan apa pun.
- Belum ada pencarian (search bar di topbar bersifat visual, belum fungsional).
- Belum ada manajemen banyak pengguna secara dinamis (daftar pengguna di halaman Pengaturan masih data contoh).

## Rencana Pengembangan Lanjutan

Beberapa hal yang bisa ditambahkan jika proyek ini dikembangkan menjadi sistem produksi:

- Backend dan basis data (misalnya untuk data pasien, rekam medis, transaksi, stok obat).
- Autentikasi sungguhan (hash password, token sesi/JWT, manajemen hak akses per pengguna).
- Integrasi data real-time (WebSocket/polling) untuk antrian dan okupansi ranjang.
- Modul cetak (kwitansi, resep, surat rujukan) dan ekspor laporan ke PDF/Excel.
- Audit log aktivitas pengguna.
