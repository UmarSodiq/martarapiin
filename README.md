# Martarapiin - Nota Layanan Website

Aplikasi web generator nota/invoice untuk layanan pengolahan dokumen (pengetikan, editing, formatting). Dibangun sebagai Single-Page Application berbasis file HTML tunggal tanpa framework atau build tool, sehingga dapat dijalankan langsung di browser.

---

## Fitur Utama

- **Autentikasi berbasis password** — Akses dibatasi untuk 2 akun pengguna terdaftar menggunakan session storage.
- **Pembuatan nota** — Formulir lengkap dengan input nama pelanggan, tanggal, nomor nota otomatis (format `MRP-YYYYMMDD-XXX`), dan daftar layanan.
- **Kalkulasi harga otomatis** — Harga dihitung secara real-time berdasarkan jenis layanan dan jumlah halaman, termasuk tarif bertingkat untuk layanan Merapikan dan Cek Typo.
- **Pratinjau nota** — Tampilan visual nota sebelum disimpan atau diunduh.
- **Unduh nota sebagai JPG** — Menggunakan html2canvas untuk menghasilkan file gambar beresolusi tinggi (scale 3x).
- **Riwayat nota** — Semua nota tersimpan secara persisten di localStorage dan dapat dilihat, diunduh ulang, atau dihapus.
- **Info pembayaran dan QRIS** — Bagian bawah nota menampilkan informasi pembayaran dan gambar QRIS yang di-embed langsung.
- **Antarmuka responsif** — Mendukung lebar layar 320px hingga 1920px dengan breakpoint untuk ponsel, tablet, dan desktop.

---

## Layanan yang Didukung

| Layanan | Tarif |
|---|---|
| Nomor Halaman | Rp 10.000 per file |
| Daftar Lengkap | Rp 10.000 per file |
| Bookmark PDF | Rp 15.000 (tetap) |
| Footnote | Rp 20.000 per file |
| Merapikan | Rp 15.000 untuk 1-100 hal, +Rp 200/hal di atas 100 |
| Cek Typo | Rp 10.000 untuk 1-100 hal, +Rp 150/hal di atas 100 |
| Daftar Pustaka | Rp 20.000 per file |

---

## Cara Menjalankan

Tidak diperlukan instalasi atau build tool. Cukup buka file `index.html` langsung di browser.

```
Buka index.html di browser
```

Pastikan file `QRIS.png` berada di folder yang sama dengan `index.html` agar gambar QRIS tampil pada nota.

---

## Deployment ke GitHub Pages

1. Buat repository baru di GitHub (pilih **Public**).
2. Upload file `index.html` dan `QRIS.png` ke repository.
3. Buka **Settings** > **Pages**, pilih branch `main` dan folder `/ (root)`, lalu klik **Save**.
4. Akses aplikasi melalui:

```
https://<username>.github.io/<nama-repo>/
```

---

## Struktur Folder

```
/
├── index.html          # Aplikasi lengkap (HTML + CSS + JavaScript)
├── QRIS.png            # Gambar QRIS untuk info pembayaran pada nota
├── src/                # Modul ES untuk pengujian unit (tidak digunakan di produksi)
│   ├── calculator.js
│   ├── history.js
│   ├── auth.js
│   └── download.js
├── tests/              # File pengujian Vitest
│   ├── calculator.test.js
│   ├── history.test.js
│   ├── auth.test.js
│   └── download.test.js
├── package.json
└── vitest.config.js
```

> Untuk deployment, hanya `index.html` dan `QRIS.png` yang diperlukan.

---

## Teknologi yang Digunakan

| Teknologi | Keterangan |
|---|---|
| HTML5 | Struktur halaman |
| CSS3 (Vanilla) | Styling dengan CSS custom properties |
| JavaScript (ES6+) | Logika aplikasi, inline di dalam `index.html` |
| html2canvas 1.4.1 | Konversi elemen HTML menjadi file JPG |
| Google Fonts (Poppins) | Tipografi |
| localStorage | Penyimpanan riwayat nota secara persisten |
| sessionStorage | Manajemen sesi login |
| Vitest | Test runner untuk pengujian unit dan property-based |
| fast-check | Library property-based testing |

---

## Pengujian

Pengujian hanya diperlukan selama development dan tidak berpengaruh pada aplikasi produksi.

```bash
# Install dependensi pengujian
npm install

# Jalankan semua test
npx vitest --run

# Jalankan test file tertentu
npx vitest --run tests/calculator.test.js
```

---

## Konfigurasi Password

Password pengguna dikonfigurasi langsung di dalam `index.html` pada baris:

```javascript
const VALID_PASSWORDS = ['password1', 'password2'];
```

Ganti nilai tersebut sesuai kebutuhan sebelum deployment.
