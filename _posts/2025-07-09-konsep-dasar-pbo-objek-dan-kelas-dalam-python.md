---
title: "PBO 2: Konsep Dasar PBO - Objek & Kelas dalam Python"
date: 2025-07-10 17:00:00 +0700
categories: [Materi Kuliah, Pemrograman Berorientasi Objek (PBO)]
tags: [kuliah, pbo] # TAG names should always be lowercase
toc: true
---
## Tujuan Pembelajaran:

Pada akhir pertemuan ini, mahasiswa diharapkan mampu:

1.  Menjelaskan hubungan antara **kelas** dan **objek**.
2.  Mendefinisikan sebuah **kelas** di Python dengan **atribut** dan **metode**.
3.  Membuat **objek (instansiasi)** dari sebuah kelas.
4.  Mengakses **atribut** dan memanggil **metode** dari sebuah objek.
5.  Memahami peran **`self`** dalam metode kelas.
6.  Menerapkan konsep objek dan kelas pada studi kasus pengelolaan buku.

-----

## A. Mengingat Kembali: Objek & Kelas

Di pertemuan sebelumnya, kita sudah sedikit menyinggung tentang **objek** dan **kelas**. Mari kita perdalam pemahaman ini dengan analogi:

**Analogi "Cetak Biru dan Rumah":**

Bayangkan sebuah **kelas** itu seperti **cetak biru (blueprint)** sebuah rumah. Cetak biru ini mendefinisikan semua fitur yang akan dimiliki rumah: berapa kamar tidur, berapa kamar mandi, di mana letak dapur, dan bagaimana desain umumnya.

  * **Cetakan biru itu sendiri bukanlah rumah.** Anda tidak bisa tinggal di dalamnya.
  * Namun, dari satu cetak biru yang sama, Anda bisa membangun **banyak rumah** yang serupa.

Setiap rumah yang Anda bangun dari cetak biru itu adalah sebuah **objek**.

  * Setiap **objek rumah** memiliki karakteristik yang didefinisikan dalam cetak biru (misalnya, jumlah kamar tidur), tetapi nilai karakteristiknya bisa berbeda (misalnya, satu rumah dicat warna biru, yang lain warna hijau).
  * Setiap **objek rumah** juga bisa melakukan hal yang sama (misalnya, pintu bisa dibuka, lampu bisa dinyalakan), karena perilakunya juga didefinisikan dalam cetak biru.

Jadi, dalam PBO:

  * **Kelas** = Cetak Biru (definisi, template, prototype)
  * **Objek** = Instansi Nyata (hal yang bisa Anda gunakan, yang punya data spesifik)

-----

## B. Mendefinisikan Kelas di Python

Di Python, kita mendefinisikan kelas menggunakan kata kunci `class`.

### Struktur Dasar Kelas:

```python
class NamaKelas: # Nama kelas biasanya diawali huruf kapital (PascalCase)
    # Atribut Kelas (opsional, dibahas nanti)
    # Metode (fungsi yang berada di dalam kelas)
    pass # 'pass' adalah placeholder jika kelas masih kosong
```

### Contoh: Kelas `Mobil`

Mari kita buat kelas `Mobil` yang kita analogikan tadi. Mobil punya **atribut** seperti merek, model, tahun, dan **metode** seperti `nyalakan_mesin()` dan `maju()`.

```python
class Mobil:
    def __init__(self, merek, model, tahun):
        # Ini adalah Constructor (__init__ method)
        # 'self' mereferensikan objek yang sedang dibuat
        self.merek = merek      # Atribut 'merek'
        self.model = model      # Atribut 'model'
        self.tahun = tahun      # Atribut 'tahun'
        self.mesin_hidup = False # Atribut status awal

    def nyalakan_mesin(self):
        # Metode untuk menyalakan mesin
        if not self.mesin_hidup:
            self.mesin_hidup = True
            print(f"Mesin {self.merek} {self.model} berhasil dinyalakan.")
        else:
            print(f"Mesin {self.merek} {self.model} sudah hidup.")

    def maju(self, kecepatan):
        # Metode untuk menjalankan mobil
        if self.mesin_hidup:
            print(f"Mobil {self.merek} {self.model} melaju dengan kecepatan {kecepatan} km/jam.")
        else:
            print(f"Mesin {self.merek} {self.model} belum hidup, tidak bisa melaju.")

    def matikan_mesin(self):
        # Metode untuk mematikan mesin
        if self.mesin_hidup:
            self.mesin_hidup = False
            print(f"Mesin {self.merek} {self.model} berhasil dimatikan.")
        else:
            print(f"Mesin {self.merek} {self.model} sudah mati.")

    def info_mobil(self):
        # Metode untuk menampilkan informasi mobil
        print(f"\n--- Info Mobil ---")
        print(f"Merek: {self.merek}")
        print(f"Model: {self.model}")
        print(f"Tahun: {self.tahun}")
        print(f"Mesin Hidup: {self.mesin_hidup}")
        print(f"------------------")

```

-----

## C. Constructor (`__init__`) dan `self`

### Constructor (`__init__` method)

  * **Apa itu?** Ini adalah metode khusus di Python yang secara otomatis dipanggil setiap kali Anda membuat **objek baru** dari sebuah kelas.

  * **Fungsi:** Tugas utamanya adalah **menginisialisasi atribut-atribut** dari objek yang baru dibuat.

  * **Nama Khusus:** Di Python, metode ini selalu bernama `__init__` (dua underscore di awal dan dua di akhir).

    ```python
    def __init__(self, parameter1, parameter2, ...):
        # Inisialisasi atribut
        self.nama_atribut1 = parameter1
        self.nama_atribut2 = parameter2
    ```

### Parameter Pertama: `self`

  * **Apa itu?** `self` adalah parameter pertama yang harus ada di setiap metode dalam sebuah kelas (termasuk `__init__`).
  * **Fungsi:** `self` secara konvensional (bukan paksaan, tapi sangat disarankan) merepresentasikan **objek itu sendiri** yang sedang dioperasikan. Melalui `self`, metode dapat mengakses atribut dan metode lain dari objek yang sama.
  * **Analogi:** Bayangkan Anda sedang membaca resep masakan. Setiap langkah resep (metode) akan selalu merujuk pada "bahan-bahan yang **Anda** miliki" (atribut objek). `self` adalah cara bagi metode untuk mengatakan "saya akan bekerja pada atribut objek ini".
  * Saat Anda memanggil sebuah metode pada objek (misalnya `mobil_saya.nyalakan_mesin()`), Python secara otomatis meneruskan objek `mobil_saya` sebagai argumen pertama untuk parameter `self`. Anda tidak perlu menuliskannya secara eksplisit saat memanggil metode.

-----

## D. Membuat Objek (Instansiasi)

Setelah mendefinisikan kelas, kita bisa membuat objek (atau meng-*instantiate*) dari kelas tersebut.

```python
# Membuat objek (instansiasi) dari kelas Mobil
mobil_saya = Mobil("Toyota", "Avanza", 2023) # Ini memanggil __init__
mobil_teman = Mobil("Honda", "CRV", 2022)   # Objek lain dari kelas Mobil
```

Setiap kali Anda menulis `Mobil(...)`, Anda sedang membuat sebuah **objek baru** yang unik, meskipun semuanya berasal dari "cetak biru" yang sama, yaitu kelas `Mobil`.

-----

## E. Mengakses Atribut dan Memanggil Metode

Setelah objek dibuat, kita bisa mengakses atributnya atau memanggil metodenya menggunakan **notasi titik (`.`)**.

```python
# Mengakses atribut
print(f"Merek mobil saya: {mobil_saya.merek}")
print(f"Model mobil teman: {mobil_teman.model}")

# Memanggil metode
mobil_saya.info_mobil() # Menampilkan info awal mobil_saya
mobil_teman.info_mobil() # Menampilkan info awal mobil_teman

print("\n--- Aksi Mobil Saya ---")
mobil_saya.nyalakan_mesin() # Mesin mobil_saya hidup
mobil_saya.maju(60)       # Mobil saya melaju
mobil_saya.nyalakan_mesin() # Coba nyalakan lagi (sudah hidup)
mobil_saya.matikan_mesin() # Matikan mesin
mobil_saya.maju(20)       # Coba melaju lagi (mesin mati)
mobil_saya.info_mobil() # Menampilkan info terbaru mobil_saya

print("\n--- Aksi Mobil Teman ---")
mobil_teman.maju(30)      # Coba melaju (mesin belum hidup)
mobil_teman.nyalakan_mesin()
mobil_teman.maju(80)
mobil_teman.info_mobil()
```

**Output dari kode di atas akan menunjukkan:**

```
Merek mobil saya: Toyota
Model mobil teman: CRV

--- Info Mobil ---
Merek: Toyota
Model: Avanza
Tahun: 2023
Mesin Hidup: False
------------------

--- Info Mobil ---
Merek: Honda
Model: CRV
Tahun: 2022
Mesin Hidup: False
------------------

--- Aksi Mobil Saya ---
Mesin Toyota Avanza berhasil dinyalakan.
Mobil Toyota Avanza melaju dengan kecepatan 60 km/jam.
Mesin Toyota Avanza sudah hidup.
Mesin Toyota Avanza berhasil dimatikan.
Mesin Toyota Avanza belum hidup, tidak bisa melaju.

--- Info Mobil ---
Merek: Toyota
Model: Avanza
Tahun: 2023
Mesin Hidup: False
------------------

--- Aksi Mobil Teman ---
Mesin Honda CRV belum hidup, tidak bisa melaju.
Mesin Honda CRV berhasil dinyalakan.
Mobil Honda CRV melaju dengan kecepatan 80 km/jam.

--- Info Mobil ---
Merek: Honda
Model: CRV
Tahun: 2022
Mesin Hidup: True
------------------
```

Perhatikan bagaimana `mobil_saya` dan `mobil_teman` adalah entitas yang terpisah dan memiliki **state** (nilai atribut seperti `mesin_hidup`) yang berbeda, meskipun berasal dari kelas `Mobil` yang sama. Mereka berinteraksi secara independen.

-----

## F. Studi Kasus: Mengelola Buku dengan Pendekatan PBO

Mari kita revisi studi kasus pengelolaan buku dari pertemuan pertama. Ingat, sebelumnya kita menggunakan `dictionary` dan fungsi terpisah. Sekarang, kita akan membuat kelas `Buku` untuk merepresentasikan setiap buku sebagai sebuah objek.

**Masalah:** Kita ingin membuat program untuk mengelola informasi tentang beberapa buku di perpustakaan sederhana.

**Informasi yang ingin kita simpan untuk setiap buku (Atribut):**

  * Judul
  * Penulis
  * Tahun Terbit
  * Status (Tersedia/Dipinjam)

**Aksi yang bisa dilakukan (Metode):**

  * Menampilkan detail buku
  * Mengubah status buku menjadi 'Dipinjam'
  * Mengubah status buku menjadi 'Tersedia'

<!-- end list -->

```python
# Definisi Kelas Buku
class Buku:
    def __init__(self, judul, penulis, tahun_terbit):
        # Constructor untuk menginisialisasi atribut objek Buku
        self.judul = judul
        self.penulis = penulis
        self.tahun_terbit = tahun_terbit
        self.status = "Tersedia" # Status awal buku adalah 'Tersedia'

    def tampilkan_detail(self):
        # Metode untuk menampilkan semua atribut buku
        print("\n--- Detail Buku ---")
        print(f"Judul: {self.judul}")
        print(f"Penulis: {self.penulis}")
        print(f"Tahun Terbit: {self.tahun_terbit}")
        print(f"Status: {self.status}")
        print("-------------------")

    def pinjam(self):
        # Metode untuk mengubah status buku menjadi 'Dipinjam'
        if self.status == "Tersedia":
            self.status = "Dipinjam"
            print(f"Buku '{self.judul}' berhasil dipinjam.")
        else:
            print(f"Maaf, buku '{self.judul}' sedang '{self.status}'. Tidak bisa dipinjam.")

    def kembalikan(self):
        # Metode untuk mengubah status buku menjadi 'Tersedia'
        if self.status == "Dipinjam":
            self.status = "Tersedia"
            print(f"Buku '{self.judul}' berhasil dikembalikan.")
        else:
            print(f"Buku '{self.judul}' tidak dalam status dipinjam.")

# --- Penggunaan Kelas Buku ---

# Membuat objek-objek Buku (instansiasi)
buku_harry_potter = Buku("Harry Potter dan Batu Bertuah", "J.K. Rowling", 1997)
buku_filosofi_teras = Buku("Filosofi Teras", "Henry Manampiring", 2019)
buku_laskar_pelangi = Buku("Laskar Pelangi", "Andrea Hirata", 2005)

# Menampilkan detail buku awal
print("Kondisi Awal Perpustakaan:")
buku_harry_potter.tampilkan_detail()
buku_filosofi_teras.tampilkan_detail()
buku_laskar_pelangi.tampilkan_detail()

# Melakukan aksi pada objek buku
print("\n--- Aksi Peminjaman dan Pengembalian ---")
buku_harry_potter.pinjam() # Pinjam Harry Potter
buku_filosofi_teras.pinjam()  # Pinjam Filosofi Teras
buku_harry_potter.pinjam() # Coba pinjam lagi (sudah dipinjam)

buku_filosofi_teras.tampilkan_detail() # Cek status Filosofi Teras
buku_laskar_pelangi.tampilkan_detail() # Cek status Laskar Pelangi (masih tersedia)

buku_harry_potter.kembalikan() # Kembalikan Harry Potter
buku_filosofi_teras.kembalikan() # Kembalikan Filosofi Teras

buku_harry_potter.tampilkan_detail() # Cek status Harry Potter setelah dikembalikan
buku_filosofi_teras.tampilkan_detail() # Cek status Filosofi Teras setelah dikembalikan
```

**Perbandingan dengan Pendekatan Prosedural (Pertemuan 1):**

  * **Data dan Perilaku Menyatu:** Sekarang, data (judul, penulis, status) dan perilaku (pinjam, kembalikan, tampilkan\_detail) untuk sebuah buku berada di dalam satu "wadah" yang sama: **objek `Buku`**. Anda tidak perlu lagi meneruskan `buku1` sebagai parameter ke fungsi `pinjam_buku` karena metode `pinjam()` sudah secara implisit mengetahui data buku yang mana yang akan dioperasikan melalui `self`.
  * **Modularitas:** Setiap objek `Buku` adalah entitas yang independen. Jika ada masalah dengan logika peminjaman, kita tahu harus melihat di mana: di dalam metode `pinjam()` dari kelas `Buku`.
  * **Kemudahan Pengelolaan:** Jika kita ingin menambahkan atribut baru (misalnya, `isbn` atau `jumlah_halaman`), kita hanya perlu menambahkannya di definisi kelas `Buku` dan metode terkait, tanpa perlu mengubah struktur `dictionary` atau fungsi terpisah di banyak tempat.

Itu adalah beberapa kelebihan yang dimiliki PBO\!

-----

## G. Tugas
* Buatlah sebuah kelas bernama `Mahasiswa`.
* Kelas ini harus memiliki atribut: `nama`, `nim`, `prodi`, dan `angkatan`.
* Kelas ini harus memiliki metode:
    * `__init__` (constructor) untuk menginisialisasi atribut-atribut di atas.
    * `tampilkan_info()`: Metode yang mencetak semua informasi mahasiswa dalam format yang rapi.
    * `ubah_prodi(prodi_baru)`: Metode yang dapat mengubah prodi mahasiswa.
* Buat minimal 3 objek `Mahasiswa` yang berbeda.
* Gunakan metode `tampilkan_info()` untuk setiap objek.
* Coba ubah prodi salah satu mahasiswa menggunakan `ubah_prodi()` dan tampilkan infonya lagi untuk memverifikasi perubahan.

-----