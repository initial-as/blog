---
title: "PBO 1: Pengantar Pemrograman Berorientasi Objek (PBO) dan Python"
date: 2025-07-09 14:00:00 +0700
categories: [Materi Kuliah, Pemrograman Berorientasi Objek (PBO)]
tags: [kuliah, pbo] # TAG names should always be lowercase
toc: true
---
## Tujuan Pembelajaran:

Pada akhir pertemuan ini, mahasiswa diharapkan mampu:

1.  Menjelaskan perbedaan mendasar antara paradigma pemrograman prosedural dan berorientasi objek.
2.  Memahami konsep dasar dari Pemrograman Berorientasi Objek.
3.  Merefresh kembali dasar-dasar pemrograman Python yang diperlukan sebagai fondasi PBO.
4.  Mempersiapkan lingkungan pengembangan Python.

-----

## A. Pengantar Paradigma Pemrograman

Sebelum kita menyelami PBO, mari kita pahami dulu apa itu **paradigma pemrograman**. Bayangkan Anda ingin membangun sebuah rumah. Ada banyak cara untuk membangunnya, kan? Ada yang suka gaya minimalis, ada yang tradisional, ada yang modern. Setiap gaya punya pendekatan, aturan, dan filosofi sendiri.

Nah, dalam pemrograman, **paradigma pemrograman** itu seperti *gaya atau filosofi* dalam membangun sebuah program. Ini adalah cara kita berpikir dan menstrukturkan kode untuk memecahkan masalah. Secara umum, ada dua paradigma utama yang sering kita bandingkan:

### 1\. Pemrograman Prosedural

  * **Filosofi:** Program adalah urutan langkah-langkah (prosedur atau fungsi) yang harus dieksekusi secara berurutan untuk mencapai tujuan tertentu. Fokus utamanya adalah "apa yang harus dilakukan".
  * **Struktur:** Kode diatur dalam fungsi-fungsi atau prosedur-prosedur terpisah. Data seringkali terpisah dari fungsi yang mengoperasikannya.
  * **Analogi:** Resep masakan. Resep adalah urutan langkah-langkah: "potong bawang", "tumis bumbu", "masukkan ayam", dll. Setiap langkah (prosedur) menjelaskan suatu aksi.
  * **Kelebihan:** Sederhana untuk program kecil, mudah dipahami urutan eksekusinya.
  * **Kekurangan:** Sulit dikelola untuk program besar (kompleksitas meningkat), data bisa diakses dan dimodifikasi di mana saja (risiko *bug*), sulit untuk digunakan kembali (reuse) kode.
  * **Contoh Kode (Python - Konsep Prosedural):**
    ```python
    # Program untuk menghitung luas persegi panjang
    panjang = 10
    lebar = 5

    def hitung_luas(p, l):
        return p * l

    luas = hitung_luas(panjang, lebar)
    print(f"Luas persegi panjang: {luas}")

    # Data (panjang, lebar) terpisah dari fungsi (hitung_luas)
    ```

### 2\. Pemrograman Berorientasi Objek (PBO / OOP - Object-Oriented Programming)

  * **Filosofi:** Program adalah kumpulan **objek-objek** yang saling berinteraksi. Fokus utamanya adalah "siapa yang melakukan" (objek apa yang bertanggung jawab) dan "bagaimana mereka berinteraksi". Setiap objek menggabungkan **data** (informasi) dan **perilaku** (aksi/fungsi) yang relevan.
  * **Struktur:** Kode diorganisir dalam **kelas-kelas**, yang berfungsi sebagai cetak biru untuk membuat **objek**.
  * **Analogi:** Bayangkan smartphone Anda. Smartphone adalah sebuah objek. Ia punya **data** (merek, model, ukuran layar, sisa baterai) dan **perilaku** (menelepon, mengambil foto, mengirim pesan, bermain game). Anda tidak perlu tahu bagaimana sirkuit dalamnya bekerja; Anda hanya perlu tahu cara menggunakannya. Setiap aplikasi di smartphone Anda juga bisa dianggap objek yang berbeda.
  * **Kelebihan:**
      * **Modularitas:** Kode lebih terstruktur dan terorganisir.
      * **Reusable:** Objek yang sudah dibuat bisa digunakan kembali di bagian program lain atau di program yang berbeda.
      * **Maintenance:** Lebih mudah memelihara dan mengembangkan program besar.
      * **Keamanan Data:** Data lebih terlindungi.
  * **Kekurangan:** Konsep awal mungkin sedikit lebih kompleks bagi pemula.

-----

## B. Konsep Dasar Pemrograman Berorientasi Objek (OOP)

PBO dibangun di atas beberapa pilar utama. Mari kita pahami secara sederhana:

### 1\. Objek (Object)

  * **Apa itu?** Objek adalah *instansi* atau wujud nyata dari sebuah **kelas**. Objek memiliki **state (data/atribut)** dan **behavior (perilaku/metode)**.
  * **Analogi:** Jika **mobil** adalah sebuah konsep umum (kelas), maka "mobil saya merek Toyota Avanza warna hitam tahun 2023" adalah sebuah **objek**.
      * **Atribut (data):** Merek (Toyota), Model (Avanza), Warna (Hitam), Tahun (2023).
      * **Metode (perilaku):** NyalakanMesin(), Maju(), Rem(), BelokKiri().

### 2\. Kelas (Class)

  * **Apa itu?** Kelas adalah **cetak biru (blueprint)** atau **template** untuk membuat objek. Kelas mendefinisikan struktur (atribut apa saja yang dimiliki objek) dan perilaku (metode apa saja yang bisa dilakukan objek) dari semua objek yang akan dibuat dari kelas tersebut.
  * **Analogi:** Sebuah **cetak biru rumah**. Cetak biru ini tidak bisa Anda tinggali, tapi dari cetak biru ini, Anda bisa membangun banyak rumah yang memiliki struktur dan fungsi yang sama. Setiap rumah yang dibangun adalah **objek** dari cetak biru tersebut.

### 3\. Atribut (Attributes) / Properti (Properties)

  * **Apa itu?** Atribut adalah **data** atau **karakteristik** yang dimiliki oleh sebuah objek.
  * **Analogi:** Pada objek "mobil saya", **merk, warna, tahun, nomor plat** adalah atribut.

### 4\. Metode (Methods)

  * **Apa itu?** Metode adalah **fungsi** atau **perilaku** yang dapat dilakukan oleh sebuah objek. Metode beroperasi pada atribut objek.
  * **Analogi:** Pada objek "mobil saya", **menyalakan mesin, berjalan, mengerem, membunyikan klakson** adalah metode.

-----

## C. Dasar Python

Sebelum kita membuat kelas dan objek, mari kita *refresh* sedikit dasar-dasar Python yang akan sering kita gunakan.

### 1\. Variabel dan Tipe Data

  * Python adalah bahasa yang *dynamically typed*, artinya Anda tidak perlu mendeklarasikan tipe data secara eksplisit.

  * **Tipe Data Umum:**

      * `int` (integer): Bilangan bulat (contoh: `10`, `-5`)
      * `float`: Bilangan desimal (contoh: `3.14`, `-0.5`)
      * `str` (string): Teks (contoh: `"Halo Dunia"`, `'Python'`)
      * `bool` (boolean): `True` atau `False`
      * `list`: Kumpulan item yang terurut dan bisa diubah (contoh: `[1, 2, 3]`, `['apel', 'pisang']`)
      * `tuple`: Kumpulan item yang terurut dan *tidak bisa* diubah (contoh: `(1, 2)`, `('a', 'b')`)
      * `dict` (dictionary): Kumpulan pasangan kunci-nilai (key-value pairs) (contoh: `{'nama': 'Budi', 'umur': 20}`)

    <!-- end list -->

    ```python
    nama = "Alice"       # str
    umur = 25            # int
    tinggi = 170.5       # float
    is_mahasiswa = True  # bool
    hobi = ["membaca", "coding", "olahraga"] # list
    koordinat = (10, 20) # tuple
    data_diri = {"nama": "Budi", "nim": "12345"} # dict

    # Menggunakan f-string (Python 3.6+)
    print(f"Nama: {nama}, Umur: {umur}, Hobi: {hobi[0]}")

    # Menggunakan format() method
    print("Nama: {}, Umur: {}, Hobi: {}".format(nama, umur, hobi[0]))
    ```

### 2\. Operator

  * **Aritmatika:** `+`, `-`, `*`, `/`, `%` (modulus), `**` (pangkat), `//` (pembagian bulat)

  * **Perbandingan:** `==` (sama dengan), `!=` (tidak sama dengan), `<`, `>`, `<=`, `>=`

  * **Logika:** `and`, `or`, `not`

    ```python
    x = 10
    y = 3
    print(f"x + y = {x + y}")      # 13
    print(f"x == y: {x == y}")     # False
    print(f"True and False: {True and False}") # False
    ```

### 3\. Struktur Kontrol Aliran (Control Flow)

  * **`if-elif-else`:** Untuk percabangan kondisi.
    ```python
    nilai = 75
    if nilai >= 80:
        keterangan = "Sangat Baik"
    elif nilai >= 60:
        keterangan = "Baik"
    else:
        keterangan = "Cukup"
    print(f"Nilai: {nilai}, Keterangan: {keterangan}")
    ```
  * **`for` Loop:** Untuk iterasi pada koleksi (list, string, dll.).
    ```python
    buah = ["apel", "pisang", "ceri"]
    for b in buah:
        print(f"Saya suka {b}")
    ```
  * **`while` Loop:** Untuk perulangan selama kondisi `True`.
    ```python
    hitung = 0
    while hitung < 3:
        print(f"Hitungan ke-{hitung + 1}")
        hitung += 1
    ```

### 4\. Fungsi (Functions)

  * Blok kode yang dapat digunakan kembali untuk melakukan tugas tertentu.

  * Didefinisikan dengan kata kunci `def`.

    ```python
    def sapa(nama):
        """Fungsi ini menyapa seseorang."""
        print(f"Halo, {nama}!")

    def tambah(a, b):
        """Fungsi ini menjumlahkan dua angka."""
        return a + b

    sapa("Mahasiswa")
    hasil_tambah = tambah(5, 3)
    print(f"Hasil penjumlahan: {hasil_tambah}")
    ```

-----

## D. Persiapan Lingkungan Pengembangan Python

Untuk praktikum, kita memerlukan lingkungan pengembangan yang siap.

1.  **Instalasi Python:**

      * Pastikan Python terinstal di komputer Anda. Anda bisa mengunduhnya dari situs resmi: [https://www.python.org/downloads/](https://www.python.org/downloads/)
      * **Rekomendasi:** Untuk penggunaan akademis dan data science, seringkali disarankan untuk menginstal **Anaconda**. Anaconda adalah distribusi Python yang sudah dilengkapi dengan banyak pustaka penting dan lingkungan `conda` yang memudahkan manajemen paket. Unduh dari: [https://www.anaconda.com/products/individual](https://www.anaconda.com/products/individual)

2.  **Menambahkan Python ke PATH Windows (Jika tidak mencentang *add to path* saat instalasi atau menggunakan versi portabel):**
    Jika Anda tidak mencentang opsi "Add Python to PATH" saat instalasi, atau jika Anda menginstal Python secara manual (misalnya dengan mengekstrak file zip), Anda perlu menambahkannya secara manual ke variabel lingkungan PATH. Ikuti langkah-langkah berikut:

    * **Cari Lokasi Instalasi Python:**
        Biasanya Python terinstal di `C:\Users\NamaPengguna\AppData\Local\Programs\Python\PythonXX\` (di mana XX adalah versi Python, misal `Python39` atau `Python310`).
        Cari juga folder `Scripts` di dalam folder instalasi Python Anda, misalnya `C:\Users\NamaPengguna\AppData\Local\Programs\Python\PythonXX\Scripts\`.

    * **Buka Pengaturan Variabel Lingkungan:**
        * Klik kanan pada **Start Menu** (ikon Windows).
        * Pilih **System** (Sistem) atau **Settings > System > About** (Pengaturan > Sistem > Tentang).
        * Klik <kbd>Advanced system settings</kbd> (Pengaturan sistem lanjutan) di sisi kanan atau di bawah "Related settings".
        * Pada jendela "System Properties" (Properti Sistem), klik tombol <kbd>Environment Variables</kbd> (Variabel Lingkungan).

    * **Edit Variabel PATH:**
        * Di bagian "System variables" (Variabel sistem), cari variabel bernama **`Path`**.
        * Pilih `Path`, lalu klik tombol <kbd>Edit</kbd>.
        * Pada jendela "Edit environment variable" (Edit variabel lingkungan), klik <kbd>New</kbd> (Baru).
        * Tempelkan atau ketikkan path lengkap ke folder instalasi Python Anda (misalnya: `C:\Python39` atau `C:\Users\NamaPengguna\AppData\Local\Programs\Python\Python39\`) lalu tekan Enter.
        * Klik **New** lagi, dan tempelkan atau ketikkan path lengkap ke folder `Scripts` di dalam instalasi Python Anda (misalnya: `C:\Users\NamaPengguna\AppData\Local\Programs\Python\Python39\Scripts\`) dan tekan Enter.
        * Klik **OK** pada semua jendela yang terbuka (`Edit environment variable`, `Environment Variables`, `System Properties`) untuk menyimpan perubahan.

    * **Verifikasi:**
        * Buka **Command Prompt (CMD)** atau **PowerShell** *baru* (penting untuk membuka yang baru agar perubahan PATH terdeteksi).
        * Ketik `python --version` atau `python3 --version` dan tekan Enter. Jika Python sudah terpasang di PATH dengan benar, Anda akan melihat versi Python yang terinstal (misal: `Python 3.9.7`). Jika tidak, pastikan Anda telah memasukkan path yang benar dan buka CMD/PowerShell yang baru. 

3.  **Memilih IDE (Integrated Development Environment) / Editor Kode:**
    IDE akan sangat membantu Anda menulis, menjalankan, dan melakukan debug kode.

      * **Visual Studio Code (VS Code):** Sangat populer, ringan, dan serbaguna. Banyak ekstensi untuk Python.
          * Unduh: [https://code.visualstudio.com/](https://code.visualstudio.com/)
          * Pastikan menginstal ekstensi Python dari marketplace VS Code.
      * **PyCharm (Community Edition):** IDE khusus Python yang sangat kuat dan kaya fitur.
          * Unduh: [https://www.jetbrains.com/pycharm/download/](https://www.jetbrains.com/pycharm/download/)
      * **Jupyter Notebook / JupyterLab (Jika menggunakan Anaconda):** Ideal untuk eksperimen kode, analisis data, dan pembelajaran interaktif, karena bisa menjalankan kode per blok.

**Langkah-langkah Praktik (di kelas/laboratorium):**

1.  Verifikasi instalasi Python di Command Prompt/Terminal dengan mengetik: `python --version` atau `python3 --version`.
2.  Buka IDE pilihan Anda (VS Code, PyCharm, atau Jupyter Notebook).
3.  Buat file Python baru (misal: `pertemuan1.py`).
4.  Coba tulis dan jalankan kode-kode penyegaran Python yang sudah dibahas di atas. Pastikan semuanya berjalan tanpa *error*.

-----

## E. Studi Kasus Sederhana (Pre-OOP)

Mari kita pikirkan sebuah masalah sederhana yang akan kita selesaikan dengan pendekatan prosedural dulu, lalu kita bandingkan di pertemuan berikutnya dengan pendekatan PBO.

**Masalah:** Kita ingin membuat program untuk mengelola informasi tentang beberapa buku di perpustakaan sederhana.

**Informasi yang ingin kita simpan untuk setiap buku:**

  * Judul
  * Penulis
  * Tahun Terbit
  * Status (Tersedia/Dipinjam)

**Aksi yang bisa dilakukan:**

  * Menampilkan detail buku
  * Mengubah status buku menjadi 'Dipinjam'
  * Mengubah status buku menjadi 'Tersedia'

**Pendekatan Prosedural (Menggunakan List/Dictionary):**

```python
# Data buku disimpan dalam dictionary, lalu dikumpulkan dalam list
buku1 = {
    "judul": "Harry Potter dan Batu Bertuah",
    "penulis": "J.K. Rowling",
    "tahun_terbit": 1997,
    "status": "Tersedia"
}

buku2 = {
    "judul": "Filosofi Teras",
    "penulis": "Henry Manampiring",
    "tahun_terbit": 2019,
    "status": "Tersedia"
}

# Fungsi untuk menampilkan detail buku
def tampilkan_detail_buku(buku):
    print("\n--- Detail Buku ---")
    print(f"Judul: {buku['judul']}")
    print(f"Penulis: {buku['penulis']}")
    print(f"Tahun Terbit: {buku['tahun_terbit']}")
    print(f"Status: {buku['status']}")
    print("-------------------")

# Fungsi untuk meminjam buku
def pinjam_buku(buku):
    if buku['status'] == "Tersedia":
        buku['status'] = "Dipinjam"
        print(f"'{buku['judul']}' berhasil dipinjam.")
    else:
        print(f"Maaf, '{buku['judul']}' sedang {buku['status']}.")

# Fungsi untuk mengembalikan buku
def kembalikan_buku(buku):
    if buku['status'] == "Dipinjam":
        buku['status'] = "Tersedia"
        print(f"'{buku['judul']}' berhasil dikembalikan.")
    else:
        print(f"Buku '{buku['judul']}' tidak dalam status dipinjam.")

# Penggunaan program
print("Kondisi Awal:")
tampilkan_detail_buku(buku1)
tampilkan_detail_buku(buku2)

print("\nAksi:")
pinjam_buku(buku1)
pinjam_buku(buku2) # Coba pinjam buku yang sudah dipinjam (setelah aksi pertama)

print("\nKondisi Setelah Aksi:")
tampilkan_detail_buku(buku1)
tampilkan_detail_buku(buku2)

kembalikan_buku(buku1)

print("\nKondisi Setelah Pengembalian:")
tampilkan_detail_buku(buku1)
```

**Penjelasan:**

  * Perhatikan bagaimana data buku (`buku1`, `buku2`) terpisah dari fungsi-fungsi (`tampilkan_detail_buku`, `pinjam_buku`, `kembalikan_buku`).
  * Jika kita punya 1000 buku, bagaimana cara mengelola datanya? Bagaimana kalau kita ingin menambah informasi lain, misalnya ISBN atau jumlah halaman? Kita harus memodifikasi banyak bagian kode.
  * Ini adalah titik awal kita. Di pertemuan berikutnya, kita akan melihat bagaimana PBO memberikan solusi yang lebih elegan dan terstruktur untuk masalah seperti ini.

-----

## F. Tugas

1.  **Instalasi & Konfigurasi:** Pastikan Python dan IDE pilihan Anda (VS Code/PyCharm/Anaconda) sudah terinstal dan berfungsi dengan baik di laptop masing-masing.
2.  **Latihan Dasar Python:** Buatlah sebuah program Python sederhana yang mengaplikasikan konsep dasar yang sudah dipelajari (variabel, tipe data, operator, `if-else`, `for`/`while` loop, fungsi). Program bisa berupa kalkulator sederhana, konversi suhu, atau game tebak angka.

-----