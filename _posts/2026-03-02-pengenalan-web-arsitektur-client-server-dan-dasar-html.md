---
title: "Pengenalan Web, Arsitektur Client–Server, dan Dasar HTML"
date: 2026-03-02 08:30:00 +0700
categories: [Materi Kuliah, Pemrograman Web Dasar]
tags: [kuliah, web] # TAG names should always be lowercase
toc: true
---

Baik, berikut versi **modul resmi (bahasa akademik formal)** untuk Pertemuan 1 Mata Kuliah **Pemrograman Web Dasar (2 SKS Teori + 2 SKS Praktik)**.

---

## Capaian Pembelajaran Pertemuan (Sub-CPMK)

Setelah mengikuti perkuliahan ini, mahasiswa mampu:

1. Menjelaskan sejarah dan perkembangan teknologi web secara runtut.
2. Mendeskripsikan arsitektur client–server dalam sistem berbasis web.
3. Menjelaskan mekanisme kerja HTTP (request–response).
4. Mengidentifikasi komponen utama website (frontend, backend, database).
5. Menyusun dokumen HTML dasar sesuai standar HTML5.

## 1. Pendahuluan

Perkembangan teknologi informasi telah mendorong transformasi besar dalam cara manusia mengakses dan menyebarkan informasi. Salah satu teknologi yang memiliki pengaruh signifikan adalah World Wide Web (WWW).

World Wide Web pertama kali dikembangkan oleh **Tim Berners-Lee** pada tahun 1989 di **CERN**. Tujuan awal pengembangannya adalah untuk mempermudah pertukaran dokumen antar peneliti melalui sistem berbasis hypertext.

Sejak saat itu, web mengalami evolusi yang sangat pesat dan menjadi fondasi utama berbagai sistem informasi modern.

---

## 2. Evolusi Perkembangan Web

### 2.1 Web 1.0 (Static Web)

Karakteristik:

* Halaman bersifat statis
* Konten tidak interaktif
* Tidak terdapat partisipasi pengguna

Web 1.0 umumnya digunakan sebagai media penyampaian informasi satu arah.

---

### 2.2 Web 2.0 (Interactive Web)

Karakteristik:

* Interaktif
* User-generated content
* Integrasi media sosial
* Komunikasi dua arah

Teknologi seperti JavaScript dan server-side scripting mendorong lahirnya Web 2.0.

---

### 2.3 Web 3.0 (Semantic & Intelligent Web)

Karakteristik:

* Data terstruktur
* Integrasi kecerdasan buatan
* Personalisasi konten
* Interoperabilitas sistem

Dalam mata kuliah ini, fokus pembelajaran berada pada fondasi Web 1.0 dan Web 2.0.

---

## 3. Konsep Dasar Website

Website adalah kumpulan halaman web yang saling terhubung dan dapat diakses melalui jaringan internet menggunakan perangkat lunak peramban (browser).

---

### 3.1 Komponen Utama Website

#### a. Frontend

Bagian yang berinteraksi langsung dengan pengguna.

Teknologi utama:

* HTML (struktur)
* CSS (tampilan)
* JavaScript (interaksi)

---

#### b. Backend

Bagian yang berjalan di sisi server dan bertugas memproses logika aplikasi.

Contoh bahasa pemrograman:

* PHP
* Python
* Node.js

---

#### c. Database

Sistem penyimpanan data terstruktur.

Contoh:

* MySQL
* PostgreSQL

---

## 4. Arsitektur Client–Server

Arsitektur client–server merupakan model komunikasi antara dua komponen utama dalam sistem jaringan.

### 4.1 Client

Client adalah perangkat pengguna yang mengirim permintaan (request) ke server melalui browser.

Contoh browser:

* Google Chrome
* Mozilla Firefox
* Microsoft Edge

---

### 4.2 Server

Server adalah komputer atau sistem yang:

* Menyimpan file website
* Memproses permintaan pengguna
* Mengirim respons kembali ke client

---

### 4.3 Skema Komunikasi

User → Browser (Client) → Internet → Server → Internet → Browser → User

Model ini menjadi dasar seluruh sistem web modern.

---

## 5. Mekanisme Kerja HTTP

Web menggunakan protokol komunikasi bernama HTTP (HyperText Transfer Protocol).

### 5.1 Tahapan Proses

1. Pengguna mengetik URL pada browser.
2. Browser mengirim HTTP Request ke server.
3. Server menerima dan memproses permintaan.
4. Server mengirim HTTP Response.
5. Browser merender dan menampilkan halaman.

---

### 5.2 Metode HTTP Dasar

* GET → Mengambil data
* POST → Mengirim data

---

### 5.3 Status Code HTTP

* 200 OK → Permintaan berhasil
* 404 Not Found → Halaman tidak ditemukan
* 500 Internal Server Error → Kesalahan server
* 301 Redirect → Pengalihan halaman

Pemahaman status code penting dalam proses debugging.

---

## 6. Pengenalan HTML

HTML (HyperText Markup Language) adalah bahasa markup yang digunakan untuk menyusun struktur halaman web.

HTML:

* Bukan bahasa pemrograman
* Tidak memiliki logika komputasi
* Berfungsi untuk menyusun struktur dokumen

---

## 7. Konsep Tag, Elemen, dan Atribut

### 7.1 Tag

Ditulis menggunakan tanda kurung siku:

```html
<p>
```

---

### 7.2 Elemen

Kombinasi tag pembuka, isi, dan tag penutup:

```html
<p>Contoh paragraf</p>
```

---

### 7.3 Atribut

Memberikan informasi tambahan pada elemen.

```html
<a href="https://example.com">Link</a>
```

---

## 8. Struktur Dasar Dokumen HTML5

Struktur standar dokumen HTML:

```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Judul Halaman</title>
</head>
<body>
    <h1>Selamat Datang</h1>
    <p>Ini adalah halaman pertama saya.</p>
</body>
</html>
```

---

### 8.1 Penjelasan Struktur

#### a. `<!DOCTYPE html>`

Menunjukkan bahwa dokumen menggunakan HTML5.

#### b. `<html>`

Elemen root dari seluruh dokumen.

#### c. `<head>`

Berisi metadata seperti judul, encoding, dan pengaturan tampilan.

#### d. `<meta charset="UTF-8">`

Mengatur standar encoding karakter.

#### e. `<meta name="viewport">`

Mendukung desain responsif.

#### f. `<title>`

Judul halaman pada tab browser.

#### g. `<body>`

Konten utama yang ditampilkan kepada pengguna.

---

## 9. Elemen Dasar HTML

### 9.1 Heading

```html
<h1>Judul</h1>
<h2>Subjudul</h2>
```

Digunakan untuk struktur hierarki informasi.

---

### 9.2 Paragraf

```html
<p>Isi paragraf.</p>
```

---

### 9.3 Horizontal Rule

```html
<hr>
```

---

## 9.4 Line Break

```html
<br>
```

---

### 9.5 Elemen Semantik Dasar

Lebih disarankan menggunakan:

```html
<strong>Teks penting</strong>
<em>Teks penekanan</em>
```

Karena memiliki makna semantik.

---

## 10. Struktur Folder Proyek

Untuk praktik profesional sejak awal, gunakan struktur berikut:

```
project-web/
│
├── index.html
└── assets/
    ├── css/
    └── js/
```

Struktur ini memudahkan pengembangan lanjutan.

---

## Rangkuman

Pada pertemuan ini telah dibahas:

1. Sejarah dan evolusi web
2. Konsep dasar website
3. Arsitektur client–server
4. Mekanisme HTTP
5. Pengenalan HTML
6. Struktur dokumen HTML5
7. Praktik penulisan kode yang baik

Materi ini menjadi fondasi untuk pertemuan selanjutnya yang akan membahas elemen HTML lanjutan dan navigasi antar halaman.

---

# Praktikum

## A. Tujuan Praktikum

Setelah menyelesaikan praktikum ini, mahasiswa mampu:

1. Membuat struktur folder proyek web yang rapi dan terorganisir.
2. Membuat file HTML dengan struktur HTML5 yang benar.
3. Mengimplementasikan elemen dasar HTML.
4. Menjalankan file HTML di browser.
5. Menyimpan dan mengelola file proyek secara sistematis.

---

## B. Deskripsi Proyek Semester

Mahasiswa akan membangun:

> **Website Company Profile & Sistem Pendaftaran Online Sederhana**

Tahap 1 berfokus pada:

* Setup proyek
* Struktur dasar halaman utama (Home)
* Penulisan HTML sesuai standar

---

## C. Persiapan Alat dan Software

Mahasiswa wajib menyiapkan:

1. Text Editor:

   * Visual Studio Code (direkomendasikan)
   * Notepad++
   * Sublime Text

2. Browser:

   * Google Chrome
   * Mozilla Firefox

3. Folder kerja di komputer masing-masing.

---

## D. Langkah-Langkah Praktikum

---

### LANGKAH 1 – Membuat Struktur Folder Proyek

1. Buat folder utama dengan nama:

```
web-company-profile
```

2. Di dalamnya, buat struktur berikut:

```
web-company-profile/
│
├── index.html
└── assets/
    ├── css/
    └── js/
```

⚠️ Catatan:

* Gunakan huruf kecil.
* Jangan gunakan spasi pada nama folder.
* Gunakan tanda hubung (-) jika perlu.

---

### LANGKAH 2 – Membuat File index.html

Buka text editor dan buat file baru:

```
index.html
```

Simpan di dalam folder `web-company-profile`.

---

### LANGKAH 3 – Menulis Struktur HTML5 Dasar

Ketik kode berikut:

```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Company Profile - Beranda</title>
</head>
<body>

</body>
</html>
```

Penjelasan:

* `<!DOCTYPE html>` → Mendeklarasikan HTML5
* `lang="id"` → Bahasa Indonesia
* `meta charset` → Encoding UTF-8
* `meta viewport` → Responsive design

Simpan file.

---

## LANGKAH 4 – Menambahkan Konten Halaman Home

Tambahkan isi berikut di dalam `<body>`:

```html
<h1>PT Maju Jaya Teknologi</h1>

<hr>

<h2>Tentang Kami</h2>
<p>
PT Maju Jaya Teknologi adalah perusahaan yang bergerak di bidang
pengembangan perangkat lunak dan solusi digital.
</p>

<h2>Visi</h2>
<p>
Menjadi perusahaan teknologi terdepan dalam inovasi dan layanan digital.
</p>

<h2>Misi</h2>
<p>
Memberikan solusi teknologi yang efektif, efisien, dan berkualitas tinggi.
</p>
```

---

### LANGKAH 5 – Menjalankan File di Browser

1. Klik dua kali file `index.html`
2. Atau klik kanan → Open With → Browser
3. Pastikan halaman tampil dengan benar

---

### LANGKAH 6 – Validasi Struktur

Periksa:

✔ Semua tag ditutup dengan benar
✔ Indentasi rapi
✔ Tidak ada kesalahan penulisan tag
✔ Struktur lengkap (DOCTYPE, html, head, body)

---

## E. Standar Kode yang Wajib Dipenuhi

Mahasiswa WAJIB:

* Menggunakan huruf kecil pada tag
* Menggunakan indentasi konsisten (2 atau 4 spasi)
* Tidak menggunakan inline style
* Tidak menghapus struktur dasar HTML5
* Menyimpan file dengan ekstensi `.html`

---

## F. Tantangan Tambahan (Opsional – Nilai Plus)

Tambahkan:

1. Paragraf tambahan tentang layanan perusahaan
2. Informasi alamat perusahaan
3. Gunakan elemen `<strong>` dan `<em>` secara tepat

Contoh:

```html
<p>
Kami menyediakan layanan <strong>pengembangan web</strong>,
<em>mobile application</em>, dan sistem informasi.
</p>
```

---

## G. Output yang Harus Dikumpulkan

Mahasiswa mengumpulkan laporan praktikum yang menampilkan:

1. Kode file `index.html`
2. Screenshot tampilan di browser

---

## H. Refleksi Praktikum

Mahasiswa diminta menjawab secara singkat:

1. Apa fungsi `<!DOCTYPE html>`?
2. Apa perbedaan `<head>` dan `<body>`?
3. Mengapa struktur folder penting dalam pengembangan web?

---

## Referensi

* Duckett, J. (2011). *HTML and CSS: Design and Build Websites*.
* [MDN Web Docs.] (https://developer.mozilla.org/en-US/docs/Web/HTML).
* [W3Schools HTML Tutorial.](https://www.w3schools.com/html/)
