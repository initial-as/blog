---
title: "PBO 3: Atribut dan Metode"
date: 2025-07-22 14:00:00 +0700
categories: [Materi Kuliah, Pemrograman Berorientasi Objek (PBO)]
tags: [kuliah, pbo] # TAG names should always be lowercase
toc: true
---
## Tujuan Pembelajaran:

Pada akhir pertemuan ini, mahasiswa diharapkan mampu:

1.  Membedakan antara **atribut instansi** dan **atribut kelas**.
2.  Memahami bagaimana atribut diinisialisasi dan diakses.
3.  Membedakan antara **metode instansi**, **metode kelas (`@classmethod`)**, dan **metode statis (`@staticmethod`)**.
4.  Menentukan kapan harus menggunakan masing-masing jenis metode berdasarkan kebutuhan program.
5.  Menerapkan berbagai jenis atribut dan metode pada studi kasus.

-----

## A. Atribut: Data dalam Objek

Atribut adalah data yang disimpan dalam sebuah kelas atau objek. Di Python, ada dua jenis atribut utama yang perlu Anda pahami:

### 1\. Atribut Instansi (Instance Attributes)

  * **Definisi:** Atribut yang **unik untuk setiap objek (instansi)** dari sebuah kelas. Setiap objek memiliki salinan atributnya sendiri, dan perubahan pada atribut ini hanya memengaruhi objek tersebut, bukan objek lain dari kelas yang sama.

  * **Inisialisasi:** Biasanya diinisialisasi di dalam metode `__init__` menggunakan `self.nama_atribut = nilai`.

  * **Akses:** Diakses melalui objek menggunakan notasi titik: `objek.nama_atribut`.

  * **Analogi:** Bayangkan kelas `Mahasiswa`. Setiap mahasiswa punya **nama** dan **NIM** yang berbeda. Nama dan NIM adalah atribut instansi karena nilainya unik untuk setiap mahasiswa.

    ```python
    class Mahasiswa:
        def __init__(self, nama, nim):
            self.nama = nama  # Atribut instansi
            self.nim = nim    # Atribut instansi
            self.ipk = 0.0    # Atribut instansi dengan nilai default

    # Membuat objek mahasiswa
    mhs1 = Mahasiswa("Budi Santoso", "12345")
    mhs2 = Mahasiswa("Siti Aminah", "67890")

    # Mengakses atribut instansi
    print(f"Nama Mahasiswa 1: {mhs1.nama}, NIM: {mhs1.nim}") # Budi Santoso, 12345
    print(f"Nama Mahasiswa 2: {mhs2.nama}, NIM: {mhs2.nim}") # Siti Aminah, 67890

    # Mengubah atribut instansi
    mhs1.ipk = 3.75
    print(f"IPK Budi: {mhs1.ipk}") # 3.75
    print(f"IPK Siti: {mhs2.ipk}") # 0.0 (tidak berubah)
    ```

### 2\. Atribut Kelas (Class Attributes)

  * **Definisi:** Atribut yang **dibagi oleh semua objek** dari sebuah kelas. Atribut ini dimiliki oleh kelas itu sendiri, bukan oleh objek individual. Jika atribut kelas diubah, perubahan tersebut akan terlihat pada semua objek yang mengacu pada kelas tersebut.

  * **Inisialisasi:** Didefinisikan langsung di dalam blok kelas, tetapi di luar metode apapun.

  * **Akses:** Dapat diakses melalui nama kelas (`NamaKelas.nama_atribut_kelas`) atau melalui objek (`objek.nama_atribut_kelas`), namun disarankan melalui nama kelas untuk kejelasan.

  * **Analogi:** Dalam kelas `Mahasiswa`, `jumlah_mahasiswa_terdaftar` bisa menjadi atribut kelas. Semua mahasiswa berbagi informasi tentang berapa total mahasiswa yang terdaftar. Atau `nama_universitas` yang sama untuk semua mahasiswa.

    ```python
    class Mahasiswa:
        # Atribut Kelas
        nama_universitas = "UIN Ar-Raniry"
        jumlah_mahasiswa_terdaftar = 0 # Akan kita update nanti melalui metode

        def __init__(self, nama, nim):
            self.nama = nama
            self.nim = nim
            self.ipk = 0.0
            Mahasiswa.jumlah_mahasiswa_terdaftar += 1 # Setiap objek dibuat, tambahkan jumlah

        def tampilkan_info(self):
            print(f"Nama: {self.nama}, NIM: {self.nim}")
            print(f"Universitas: {Mahasiswa.nama_universitas}") # Akses atribut kelas
            print(f"IPK: {self.ipk}")

    mhs1 = Mahasiswa("Budi Santoso", "12345")
    mhs2 = Mahasiswa("Siti Aminah", "67890")
    mhs3 = Mahasiswa("Andi Pratama", "11223")

    print(f"\nJumlah Mahasiswa Terdaftar: {Mahasiswa.jumlah_mahasiswa_terdaftar}") # Output: 3

    # Mengubah atribut kelas (akan mempengaruhi semua objek)
    Mahasiswa.nama_universitas = "UIN Ar-Raniry Banda Aceh"

    mhs1.tampilkan_info()
    mhs2.tampilkan_info()

    # Perhatikan bahwa nama_universitas berubah untuk semua objek karena kita mengubah atribut kelas
    ```

    **Kapan menggunakan yang mana?**

      * Gunakan **atribut instansi** untuk data yang unik per objek (misalnya, nama, usia, saldo).
      * Gunakan **atribut kelas** untuk data yang umum atau konstanta yang dibagi oleh semua objek dari kelas tersebut (misalnya, nama\_institusi, nilai\_default\_konstanta, counter objek).

-----

## B. Metode: Perilaku dalam Objek

Metode adalah fungsi yang didefinisikan di dalam kelas dan beroperasi pada data (atribut) dari kelas atau objek. Ada tiga jenis metode di Python:

### 1\. Metode Instansi (Instance Methods)

  * **Definisi:** Metode yang paling umum. Mereka beroperasi pada **data spesifik dari sebuah objek (instansi)**. Mereka membutuhkan akses ke atribut instansi.

  * **Parameter Pertama:** Selalu menerima `self` sebagai parameter pertama, yang mereferensikan objek itu sendiri.

  * **Kapan Digunakan:** Untuk operasi yang melibatkan atau mengubah atribut instansi dari sebuah objek. Hampir semua metode yang Anda buat akan menjadi metode instansi.

  * **Analogi:** Metode `nyalakan_mesin()` pada objek `mobil_saya` mempengaruhi `mesin_hidup` milik `mobil_saya`, bukan `mobil_teman`.

    ```python
    class Kucing:
        def __init__(self, nama, warna):
            self.nama = nama
            self.warna = warna
            self.lapar = True

        def makan(self, makanan): # Metode instansi
            if self.lapar:
                print(f"{self.nama} ({self.warna}) sedang makan {makanan}.")
                self.lapar = False
            else:
                print(f"{self.nama} tidak lapar.")

        def info(self): # Metode instansi
            print(f"{self.nama} adalah kucing berwarna {self.warna}. Lapar: {self.lapar}")

    kucing_saya = Kucing("Kitty", "Oren")
    kucing_tetangga = Kucing("Tom", "Abu-abu")

    kucing_saya.info() # Kitty adalah kucing berwarna Oren. Lapar: True
    kucing_saya.makan("ikan") # Kitty (Oren) sedang makan ikan.
    kucing_saya.info() # Kitty adalah kucing berwarna Oren. Lapar: False

    kucing_tetangga.info() # Tom adalah kucing berwarna Abu-abu. Lapar: True
    ```

### 2\. Metode Kelas (Class Methods)

  * **Definisi:** Metode yang beroperasi pada **kelas itu sendiri**, bukan pada instansi objek tertentu. Mereka dapat mengakses dan memodifikasi atribut kelas.

  * **Dekorator:** Ditandai dengan dekorator `@classmethod` tepat di atas definisi metode.

  * **Parameter Pertama:** Menerima `cls` (secara konvensional) sebagai parameter pertama, yang mereferensikan kelas itu sendiri, bukan objek.

  * **Kapan Digunakan:**

      * Untuk membuat *constructor* alternatif (misalnya, membuat objek dari format data yang berbeda).
      * Untuk mengakses atau memodifikasi atribut kelas.
      * Untuk membuat metode yang berhubungan dengan fungsionalitas kelas secara keseluruhan.

  * **Analogi:** Sebuah metode di kelas `Mahasiswa` yang dapat menghitung rata-rata IPK dari semua mahasiswa yang pernah dibuat (jika IPK semua mahasiswa disimpan di atribut kelas), atau metode yang membuat objek mahasiswa dari string data tertentu.

    ```python
    class Karyawan:
        jumlah_karyawan = 0 # Atribut kelas

        def __init__(self, nama, gaji):
            self.nama = nama
            self.gaji = gaji
            Karyawan.jumlah_karyawan += 1

        @classmethod
        def tampilkan_total_karyawan(cls): # cls mereferensikan kelas Karyawan
            print(f"Total karyawan yang terdaftar: {cls.jumlah_karyawan}")

        @classmethod
        def dari_string(cls, data_string): # Contoh constructor alternatif
            nama, gaji = data_string.split('-')
            return cls(nama, int(gaji)) # Menggunakan cls() untuk membuat objek baru

    k1 = Karyawan("Alice", 50000)
    k2 = Karyawan("Bob", 60000)

    Karyawan.tampilkan_total_karyawan() # Output: Total karyawan yang terdaftar: 2

    data_baru = "Charlie-75000"
    k3 = Karyawan.dari_string(data_baru) # Membuat objek dari string
    print(f"Nama Karyawan 3: {k3.nama}, Gaji: {k3.gaji}")
    Karyawan.tampilkan_total_karyawan() # Output: Total karyawan yang terdaftar: 3
    ```

### 3\. Metode Statis (Static Methods)

  * **Definisi:** Metode yang tidak beroperasi pada instansi objek (`self`) maupun pada kelas (`cls`). Mereka adalah fungsi biasa yang secara logis terkait dengan kelas, tetapi tidak memerlukan akses ke data kelas atau instansi.

  * **Dekorator:** Ditandai dengan dekorator `@staticmethod` tepat di atas definisi metode.

  * **Parameter:** Tidak menerima `self` atau `cls` sebagai parameter pertama.

  * **Kapan Digunakan:** Untuk fungsi utilitas yang terkait dengan kelas, tetapi tidak memerlukan data objek atau kelas. Mereka berperilaku seperti fungsi independen yang kebetulan diletakkan di dalam kelas untuk organisasi kode.

  * **Analogi:** Sebuah metode di kelas `Matematika` (jika ada) yang menghitung `akar_kuadrat(angka)`. Fungsi ini tidak perlu tahu tentang objek `Matematika` tertentu atau atribut kelasnya.

    ```python
    class UtilitasMatematika:
        @staticmethod
        def tambah(a, b):
            return a + b

        @staticmethod
        def kali(a, b):
            return a * b

        @staticmethod
        def adalah_genap(angka):
            return angka % 2 == 0

    print(f"Hasil tambah 5 dan 3: {UtilitasMatematika.tambah(5, 3)}")       # Output: 8
    print(f"Apakah 10 genap? {UtilitasMatematika.adalah_genap(10)}") # Output: True

    # Bisa juga dipanggil dari objek, tapi tidak ada bedanya
    util = UtilitasMatematika()
    print(f"Hasil kali 4 dan 2: {util.kali(4, 2)}") # Output: 8
    ```

    **Kapan menggunakan yang mana? (Ringkasan Cepat)**

      * **Metode Instansi:** Butuh akses ke data **objek** (`self`).
      * **Metode Kelas:** Butuh akses ke data **kelas** (`cls`) atau ingin membuat *constructor* alternatif.
      * **Metode Statis:** Tidak butuh akses ke data **objek** maupun **kelas**. Hanya fungsi utilitas yang logis berada di dalam kelas.

-----

## C. Studi Kasus: Memperkaya Kelas `Buku`

Mari kita kembangkan kelas `Buku` dari pertemuan sebelumnya dengan menambahkan berbagai jenis atribut dan metode.

**Tambahan yang diinginkan:**

  * **Atribut Kelas:** `jumlah_buku_terdaftar` (untuk melacak total buku yang dibuat).
  * **Metode Kelas:** `cari_buku_berdasarkan_tahun(tahun_target)` (untuk mencari buku yang diterbitkan pada tahun tertentu dari daftar global buku).
  * **Metode Statis:** `validasi_tahun(tahun)` (untuk memeriksa apakah format tahun terbit valid).

<!-- end list -->

```python
class Buku:
    # Atribut Kelas
    daftar_semua_buku = [] # Atribut kelas untuk menyimpan semua objek Buku
    jumlah_buku_terdaftar = 0

    def __init__(self, judul, penulis, tahun_terbit):
        # Validasi tahun terbit menggunakan metode statis
        if not Buku.validasi_tahun(tahun_terbit):
            raise ValueError("Tahun terbit tidak valid! Harus antara 1500 dan tahun sekarang.")

        self.judul = judul
        self.penulis = penulis
        self.tahun_terbit = tahun_terbit
        self.status = "Tersedia"
        Buku.jumlah_buku_terdaftar += 1
        Buku.daftar_semua_buku.append(self) # Tambahkan objek buku ini ke daftar global

    def tampilkan_detail(self): # Metode Instansi
        print("\n--- Detail Buku ---")
        print(f"Judul: {self.judul}")
        print(f"Penulis: {self.penulis}")
        print(f"Tahun Terbit: {self.tahun_terbit}")
        print(f"Status: {self.status}")
        print("-------------------")

    def pinjam(self): # Metode Instansi
        if self.status == "Tersedia":
            self.status = "Dipinjam"
            print(f"Buku '{self.judul}' berhasil dipinjam.")
        else:
            print(f"Maaf, buku '{self.judul}' sedang '{self.status}'. Tidak bisa dipinjam.")

    def kembalikan(self): # Metode Instansi
        if self.status == "Dipinjam":
            self.status = "Tersedia"
            print(f"Buku '{self.judul}' berhasil dikembalikan.")
        else:
            print(f"Buku '{self.judul}' tidak dalam status dipinjam.")

    @classmethod
    def tampilkan_total_buku(cls): # Metode Kelas
        print(f"\nTotal buku yang terdaftar di sistem: {cls.jumlah_buku_terdaftar} buku.")

    @classmethod
    def cari_buku_berdasarkan_tahun(cls, tahun_target): # Metode Kelas
        print(f"\nMencari buku terbitan tahun {tahun_target}:")
        ditemukan = []
        for buku in cls.daftar_semua_buku:
            if buku.tahun_terbit == tahun_target:
                ditemukan.append(buku)
        if ditemukan:
            for buku in ditemukan:
                print(f"- '{buku.judul}' oleh {buku.penulis}")
        else:
            print(f"Tidak ada buku yang terbit pada tahun {tahun_target}.")
        return ditemukan

    @staticmethod
    def validasi_tahun(tahun): # Metode Statis
        import datetime
        tahun_sekarang = datetime.datetime.now().year
        return 1500 <= tahun <= tahun_sekarang # Tahun terbit minimal 1500 dan tidak boleh lebih dari tahun sekarang

# --- Penggunaan Kelas Buku yang Diperkaya ---

try:
    b1 = Buku("Harry Potter", "J.K. Rowling", 1997)
    b2 = Buku("Filosofi Teras", "Henry Manampiring", 2019)
    b3 = Buku("Laskar Pelangi", "Andrea Hirata", 2005)
    b4 = Buku("Dunia Sophie", "Jostein Gaarder", 1991)
    # b_invalid = Buku("Buku Masa Depan", "X", 2030) # Ini akan memicu ValueError
except ValueError as e:
    print(f"Error saat membuat buku: {e}")

b1.tampilkan_detail()
b2.tampilkan_detail()

Buku.tampilkan_total_buku() # Panggil metode kelas

# Mencari buku berdasarkan tahun menggunakan metode kelas
buku_2019 = Buku.cari_buku_berdasarkan_tahun(2019)
buku_2005 = Buku.cari_buku_berdasarkan_tahun(2005)
buku_2020 = Buku.cari_buku_berdasarkan_tahun(2020) # Tidak ada

# Contoh penggunaan metode statis secara langsung
print(f"\nApakah tahun 1999 valid? {Buku.validasi_tahun(1999)}")
print(f"Apakah tahun 2100 valid? {Buku.validasi_tahun(2100)}")
```

**Penjelasan:**

  * Perhatikan bagaimana `daftar_semua_buku` dan `jumlah_buku_terdaftar` adalah atribut yang dimiliki oleh **kelas `Buku`**, bukan oleh objek individual. Semua objek buku berbagi akses ke informasi ini.
  * Metode `tampilkan_total_buku()` dan `cari_buku_berdasarkan_tahun()` menggunakan `cls` untuk mengakses atribut kelas `daftar_semua_buku` dan `jumlah_buku_terdaftar`. Mereka tidak perlu tahu detail dari objek buku tertentu.
  * Metode `validasi_tahun()` adalah metode statis; ia tidak peduli objek buku mana yang memanggilnya, atau data kelasnya. Ia hanya melakukan validasi sederhana berdasarkan parameter yang diberikan.

Ini menunjukkan fleksibilitas dalam mendesain kelas dengan memilih jenis atribut dan metode yang tepat sesuai kebutuhan fungsionalitas.

-----

## D. Tugas

* Buatlah sebuah kelas bernama `Produk`.
* Kelas ini harus memiliki:
    * **Atribut Instansi:** `nama_produk`, `harga`, `stok`.
    * **Atribut Kelas:** `total_produk_terdaftar` (untuk melacak berapa total produk yang sudah dibuat), `pajak_persen` (misal: 10% atau 0.10).
    * **Metode Instansi:**
        * `__init__` (constructor) untuk `nama_produk`, `harga`, `stok`.
        * `hitung_harga_jual()`: Mengembalikan harga jual produk setelah ditambahkan pajak (`harga + (harga * pajak_persen)`).
        * `tambah_stok(jumlah)`: Menambah stok produk.
        * `kurangi_stok(jumlah)`: Mengurangi stok produk (tambahkan validasi agar stok tidak minus).
    * **Metode Kelas:**
        * `info_toko()`: Menampilkan `total_produk_terdaftar` dan `pajak_persen` saat ini.
        * `ubah_pajak(pajak_baru)`: Mengubah `pajak_persen` (atribut kelas).
    * **Metode Statis:**
        * `format_mata_uang(nilai)`: Mengembalikan string nilai dalam format mata uang (misal: "Rp 10.000").
* Buat minimal 3 objek `Produk` yang berbeda.
* Lakukan berbagai operasi (tampilkan info toko, hitung harga jual, tambah/kurangi stok, ubah pajak) untuk menunjukkan penggunaan semua jenis atribut dan metode.
-----