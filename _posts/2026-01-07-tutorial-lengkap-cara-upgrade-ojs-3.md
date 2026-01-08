---
title: "Tutorial Lengkap Cara Mudah Upgrade OJS 3"
date: 2026-01-07 21:30:00 +0700
categories: [Tutorial, OJS]
tags: [tutorial, ojs] # TAG names should always be lowercase
toc: true
---

## Pendahuluan

Open Journal Systems (OJS) adalah perangkat lunak open-source yang banyak digunakan untuk mengelola jurnal ilmiah secara daring. Pada artikel sebelumnya, kita sudah membahas [cara untuk meningkatkan keamanan OJS](../tips-pengamanan-ojs-panduan-lengkap-mencegah-serangan-malware-cloacking-dan-peretasan), kali ini kita akan membahas **cara melakukan pembaruan/_upgrade_ OJS**. Hal ini sangat disarankan untuk menjaga keamanan, stabilitas, dan kompatibilitas sistem.

Dalam ekosistem Open Journal Systems, PKP juga memperkenalkan konsep **LTS (Long Term Support)**. Versi LTS adalah versi OJS yang mendapatkan **dukungan pemeliharaan lebih lama** dibandingkan versi reguler.

Karakteristik utama OJS versi LTS antara lain:

1. Mendapatkan **pembaruan keamanan (security fixes)** dalam jangka waktu yang lebih panjang.
2. Lebih **stabil** dan minim perubahan fitur besar.
3. Direkomendasikan untuk jurnal yang mengutamakan **keandalan sistem** dibandingkan fitur eksperimental.

Sebagai contoh, **OJS 3.3.x** dikategorikan sebagai **versi LTS** oleh PKP. Artinya, versi ini:

* Cocok untuk penggunaan jangka panjang
* Aman untuk digunakan
* Menjadi target upgrade yang direkomendasikan dari versi sebelumnya (salah satu jurnal yang saya kelola saat ini menggunakan versi 3.2.1)

Sementara itu, versi non-LTS biasanya memiliki siklus rilis lebih cepat dengan fitur baru, namun masa dukungannya lebih singkat. Oleh karena itu, bagi pengelola jurnal yang tidak ingin sering melakukan upgrade, **menggunakan versi LTS adalah pilihan yang paling aman dan praktis**.

Kesimpulannya, upgrade dari **OJS 3.2.1 ke OJS 3.3.0** bukan hanya didukung secara teknis, tetapi juga merupakan langkah strategis karena berpindah ke **versi LTS yang stabil dan direkomendasikan oleh PKP**.

Artikel ini membahas **cara upgrade OJS dari versi 3.2.1 ke 3.3.0 secara manual melalui File Manager/FTP**, termasuk **aktivasi maintenance mode**, serta **informasi lompatan versi (upgrade path) yang didukung berdasarkan panduan resmi PKP**.

---

## Tentang Upgrade OJS dan Lompatan Versi

Berdasarkan **panduan resmi PKP**:  
[https://docs.pkp.sfu.ca/dev/upgrade-guide/en/](https://docs.pkp.sfu.ca/dev/upgrade-guide/en/)

Beberapa prinsip penting terkait upgrade OJS:

- Upgrade **antar minor version dalam satu major version** (misalnya 3.2.x → 3.3.x) **dapat dilakukan langsung**
- Upgrade dari **versi yang sangat lama (misalnya OJS 2.x)** **tidak boleh langsung ke 3.3.x**
- Upgrade **lintas major version** harus melalui **versi perantara (intermediate versions)**

### Contoh Upgrade yang Didukung

| Versi Awal | Versi Tujuan | Keterangan |
| :--------------------------- | :--------------- | :------ |
| 3.2.x | 3.3.x | ✅ Langsung |
| 3.1.x | 3.3.x | ✅ Langsung |
| 2.4.x | 3.3.x | ❌ Tidak langsung (harus via 2.4.8-x → 3.2.1-x → 3.3 atau lebih) |

> **Kesimpulan:**  
> Jika Anda menggunakan **OJS 3.2.1**, maka **upgrade langsung ke OJS 3.3.0 didukung secara resmi**.
{: .prompt-info }

---

## Persiapan Sebelum Upgrade

Sebelum memulai proses upgrade, pastikan Anda telah melakukan **backup penuh**:

- Backup **database** (via phpMyAdmin)
- Backup folder **`files/`**
- Backup folder instalasi **OJS**
- Akses ke **File Manager / FTP / cPanel**
- Pastikan versi PHP & database kompatibel dengan OJS 3.3

> **Kesalahan Umum yang Harus Dihindari:**<br>
> Tidak melakukan backup<br>
> Menggunakan patch, bukan full package<br>
> Lupa menyalin `config.inc.php`<br>
> Menonaktifkan maintenance sebelum upgrade database selesai<br>
> Mengakses OJS saat file masih diganti
{: .prompt-danger }

---

## Langkah 1 — Aktifkan Maintenance Mode

OJS **tidak memiliki maintenance mode bawaan**, sehingga kita perlu membuatnya secara manual agar:

- Pengunjung tidak mengakses sistem saat file diganti
- Proses editorial tidak berjalan selama upgrade
- Mencegah error akibat file setengah ter-update

### 1. Buat File Maintenance

Buat file `maintenance.html` di root OJS (misalnya `public_html/maintenance.html`). Berikut contohnya:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Maintenance</title>
</head>
<body>
    <h1>Maintenance</h1>
    <p>The site is under maintenance, the system is being upgraded. Please check back later.</p>
</body>
</html>
```

---

### 2. Redirect Semua URL ke Maintenance Page

Edit file `.htaccess` di root OJS, lalu **tambahkan di bagian paling atas**:

```apache
# ---------------------------------------
# Maintenance Mode
# ---------------------------------------
RewriteEngine On

# Allow maintenance page itself
RewriteCond %{REQUEST_URI} !maintenance\.html$

# Allow static assets
RewriteCond %{REQUEST_URI} !\.(css|js|png|jpg|jpeg|gif|svg|webp|ico)$

# Redirect all requests
RewriteRule ^.*$ /maintenance.html [R=302,L]
````

**HTTP 302 (Temporary Redirect)** digunakan agar tidak berdampak buruk pada SEO.

> **Pastikan rule maintenance berada di atas rule OJS.**
{: .prompt-warning }

---

## Langkah 2 — Unduh OJS 3.3.0

Unduh **paket lengkap (full package)** OJS 3.3.0 dari situs resmi PKP:
[https://pkp.sfu.ca/software/ojs/download/](https://pkp.sfu.ca/software/ojs/download/)


> **Sebaiknya gunakan versi LTS** dan jangan gunakan *patch* untuk upgrade lintas minor version.
{: .prompt-info }

---

## Langkah 3 — Upload dan Extract via File Manager

1. Upload file `.zip` atau `.tar.gz` ke server
2. Extract → akan muncul folder seperti:

   ```
   ojs-3.3.0-x/
   ```

---

## Langkah 4 — Salin File Penting dari OJS Lama

Dari instalasi OJS 3.2.1 lama, **salin ke folder OJS baru**:

| File / Folder     | Keterangan                   |
| ----------------- | ---------------------------- |
| `config.inc.php`  | Konfigurasi utama (WAJIB)    |
| `public/`         | Logo, cover, file publik     |
| `files/`          | File artikel & submission    |
| `plugins/themes/` | Jika menggunakan tema kustom |

> Jangan menyalin folder `lib/`, `classes/`, `pages/`
{: .prompt-danger }

---

## Langkah 5 — Ganti Folder OJS Lama

* Rename folder OJS lama → `ojs_old/`
* Rename folder OJS baru → `public_html/` (atau nama folder OJS Anda)

---

## Langkah 6 — Jalankan Upgrade Database

Buka file `config.inc.php`, cari teks:

```php
[general]

; Set this to On once the system has been installed
; (This is generally done automatically by the installer)
installed = On
```

Ubah `installed = On` menjadi `installed = Off`

Selanjutnya buka browser dan akses: 
`https://domainanda.com/index.php/index/install`

Pilih opsi **Upgrade an existing installation**, lalu ikuti wizard sampai selesai.

---

## Langkah 7 — Periksa Permission Folder

Pastikan folder `cache/`, `public/`, dan `files/` memiliki permission `755`. Hal ini untuk memastikan agar bisa folder tersebut bisa ditulis oleh web server.

---

## Langkah 8 — Finalisasi & Uji Sistem

1. Login sebagai **Site Administrator**
2. Clear cache OJS
3. Upgrade plugin dan periksa plugin yang tidak kompatibel
4. Periksa dan update template email
5. Cek tampilan jurnal & workflow editorial, pastikan semuanya sudah sesuai. Lakukan setidaknya satu kali uji coba proses editorial, mulai dari submit artikel sampai artikel diterbitkan.

---

## Langkah 9 — Matikan Maintenance Mode

Setelah upgrade berhasil:

* Hapus atau komentari rule maintenance di `.htaccess` yang telah kita buat di langkah 1
* Hapus file `maintenance.html` (opsional)

Situs akan kembali normal.

---

## Penutup

Upgrade OJS **3.2.1 ke 3.3.0** dapat dilakukan dengan aman melalui **File Manager**, asalkan mengikuti tahapan yang benar dan sesuai panduan resmi PKP. Dengan maintenance mode dan backup yang baik, risiko error dapat diminimalkan.

Semoga tutorial ini membantu proses upgrade jurnal Anda berjalan lancar.