---
title: "PBO 5: Pewarisan (Inheritance)"
date: 2025-07-25 08:00:00 +0700
categories: [Materi Kuliah, Pemrograman Berorientasi Objek (PBO)]
tags: [kuliah, pbo] # TAG names should always be lowercase
toc: true
---
## Tujuan Pembelajaran:

Pada akhir pertemuan ini, mahasiswa diharapkan mampu:

1.  Menjelaskan konsep **pewarisan (inheritance)** dan manfaatnya dalam PBO.
2.  Mengidentifikasi hubungan **"adalah sebuah" (is-a relationship)** antara kelas *parent* dan *child*.
3.  Mengimplementasikan pewarisan di Python menggunakan kelas *parent* dan *child*.
4.  Memahami bagaimana **metode di-override (overriding)** di kelas *child*.
5.  Menggunakan fungsi `super()` untuk memanggil *constructor* atau metode dari kelas *parent*.
6.  Membedakan antara pewarisan tunggal dan pewarisan berganda.
7.  Menerapkan konsep pewarisan pada studi kasus yang relevan.

-----

## A. Apa Itu Pewarisan (Inheritance)?

Dalam silsilah keluarga, Anda mungkin mewarisi beberapa karakteristik (seperti warna rambut atau mata) dari orang tua Anda. Anda adalah versi yang lebih spesifik dari "manusia" yang mewarisi sifat-sifat umum manusia, tetapi Anda juga memiliki sifat unik Anda sendiri.

Dalam PBO, **pewarisan (inheritance)** adalah mekanisme di mana sebuah kelas (disebut **kelas anak / *child class* / *subclass***) dapat mewarisi atribut dan metode dari kelas lain (disebut **kelas induk / *parent class* / *superclass* / *base class***).

  * **Kelas Induk (Parent/Superclass):** Kelas yang menjadi dasar, berisi karakteristik dan perilaku umum yang akan diwarisi.
  * **Kelas Anak (Child/Subclass):** Kelas yang mewarisi dari kelas induk. Ia mendapatkan semua atribut dan metode dari kelas induk, dan bisa menambahkan atribut/metode baru atau memodifikasi (override) yang sudah ada.

**Manfaat Pewarisan:**

1.  **Reusabilitas Kode (Code Reusability):** Anda tidak perlu menulis ulang kode yang sama berkali-kali. Cukup definisikan sekali di kelas induk, dan semua kelas anak bisa menggunakannya.
2.  **Organisasi Kode:** Membangun hierarki kelas membantu mengatur kode secara logis, mencerminkan hubungan "adalah sebuah" di dunia nyata.
3.  **Ekstensibilitas (Extensibility):** Mudah untuk menambahkan fungsionalitas baru dengan membuat kelas anak baru tanpa mengubah kelas induk yang sudah ada.
4.  **Mengurangi Redundansi:** Mengurangi pengulangan kode yang tidak perlu.

### Hubungan "Adalah Sebuah" (Is-A Relationship)

Pewarisan paling cocok ketika ada hubungan "adalah sebuah" antara kelas-kelas.

  * Seekor `Kucing` **adalah sebuah** `Hewan`.
  * Sebuah `Mobil` **adalah sebuah** `Kendaraan`.
  * Seorang `Dosen` **adalah seorang** `Pegawai`.

Ini berarti kelas `Kucing` dapat mewarisi dari `Hewan`, `Mobil` dari `Kendaraan`, dan `Dosen` dari `Pegawai`.

-----

## B. Implementasi Pewarisan di Python

Untuk membuat sebuah kelas anak yang mewarisi dari kelas induk di Python, kita cukup meletakkan nama kelas induk di dalam tanda kurung setelah nama kelas anak saat definisinya.

### Contoh Dasar: `Hewan` (Parent) dan `Kucing`, `Anjing` (Child)

```python
# Kelas Induk (Parent Class)
class Hewan:
    def __init__(self, nama):
        self.nama = nama
        print(f"Objek Hewan '{self.nama}' telah dibuat.")

    def bersuara(self):
        print(f"{self.nama} mengeluarkan suara yang umum.")

    def tidur(self):
        print(f"{self.nama} sedang tidur.")

# Kelas Anak (Child Class) - Kucing mewarisi dari Hewan
class Kucing(Hewan): # Kucing "adalah sebuah" Hewan
    def __init__(self, nama, ras):
        # Memanggil constructor kelas induk
        super().__init__(nama) # Penting! Menginisialisasi bagian Hewan dari objek Kucing
        self.ras = ras
        print(f"Objek Kucing '{self.nama}' (ras: {self.ras}) telah dibuat.")

    # Metode baru yang spesifik untuk Kucing
    def memanjat(self):
        print(f"{self.nama} si kucing sedang memanjat pohon.")

    # Meng-override (menimpa) metode bersuara dari kelas induk
    def bersuara(self):
        print(f"{self.nama} mengeong.")

# Kelas Anak (Child Class) - Anjing mewarisi dari Hewan
class Anjing(Hewan): # Anjing "adalah sebuah" Hewan
    def __init__(self, nama, jenis):
        super().__init__(nama) # Memanggil constructor kelas induk
        self.jenis = jenis
        print(f"Objek Anjing '{self.nama}' (jenis: {self.jenis}) telah dibuat.")

    # Metode baru yang spesifik untuk Anjing
    def menggonggong(self):
        print(f"{self.nama} menggonggong: Guk! Guk!")

    # Meng-override metode bersuara dari kelas induk
    def bersuara(self):
        print(f"{self.nama} mengaung.")


# --- Penggunaan Objek ---
print("--- Membuat Objek ---")
hewan_umum = Hewan("Binatang")
kucing_saya = Kucing("Kitty", "Persia")
anjing_teman = Anjing("Buddy", "Golden Retriever")

print("\n--- Memanggil Metode ---")
hewan_umum.bersuara()  # Output: Binatang mengeluarkan suara yang umum.
kucing_saya.bersuara() # Output: Kitty mengeong. (Metode di-override)
anjing_teman.bersuara() # Output: Buddy mengaung. (Metode di-override)

kucing_saya.tidur()    # Mewarisi metode tidur dari Hewan
anjing_teman.tidur()   # Mewarisi metode tidur dari Hewan

kucing_saya.memanjat() # Metode spesifik Kucing
anjing_teman.menggonggong() # Metode spesifik Anjing

# print(hewan_umum.ras) # Error! Hewan umum tidak punya atribut 'ras'
```

-----

## C. Constructor di Pewarisan: `super().__init__()`

Ketika Anda mendefinisikan metode `__init__` di kelas anak, metode itu akan **menimpa** `__init__` dari kelas induk. Ini berarti `__init__` dari kelas induk tidak akan dipanggil secara otomatis.

Namun, seringkali kita ingin kelas anak tetap melakukan inisialisasi yang dilakukan oleh kelas induk (misalnya, menginisialisasi atribut umum). Di sinilah fungsi `super()` berperan.

  * **`super()`:** Digunakan untuk memberikan akses ke metode kelas induk dari dalam kelas anak.
  * **`super().__init__(...)`:** Memanggil *constructor* dari kelas induk. Anda harus meneruskan argumen yang diperlukan oleh *constructor* kelas induk. Ini memastikan bahwa bagian dari objek yang terkait dengan kelas induk juga terinisialisasi dengan benar.

**Mengapa Penting Memanggil `super().__init__()`?**

Jika Anda tidak memanggil `super().__init__()`, atribut yang didefinisikan di *constructor* kelas induk (misalnya `self.nama` di kelas `Hewan`) tidak akan terinisialisasi di objek kelas anak. Ini bisa menyebabkan `AttributeError` ketika Anda mencoba mengakses atribut tersebut.

Perhatikan lagi contoh `Kucing` dan `Anjing` di atas yang memanggil `super().__init__(nama)`. Ini memastikan `self.nama` diinisialisasi oleh `Hewan.__init__` sebelum `Kucing.__init__` atau `Anjing.__init__` menambahkan atribut spesifik mereka.

-----

## D. Overriding Metode

**Overriding Metode** terjadi ketika sebuah kelas anak menyediakan implementasi sendiri untuk metode yang sudah didefinisikan di kelas induknya.

  * **Tujuan:** Untuk memberikan perilaku yang lebih spesifik atau berbeda untuk kelas anak, sambil tetap mempertahankan nama metode yang sama.
  * **Contoh:** Kelas `Hewan` memiliki metode `bersuara()`. `Kucing` dan `Anjing` memiliki cara bersuara yang spesifik (mengeong, menggonggong). Jadi, mereka meng-override metode `bersuara()` untuk memberikan perilaku yang sesuai dengan jenis hewan tersebut.

Anda bisa lihat bagaimana `bersuara()` di `Kucing` dan `Anjing` memiliki implementasi yang berbeda dari `bersuara()` di `Hewan`. Ketika Anda memanggil `kucing_saya.bersuara()`, Python akan menjalankan metode `bersuara()` yang ada di kelas `Kucing` (karena ia lebih spesifik).

-----

## E. Pewarisan Tunggal vs. Pewarisan Berganda (Multiple Inheritance)

### 1\. Pewarisan Tunggal (Single Inheritance)

  * Sebuah kelas anak hanya mewarisi dari **satu** kelas induk. Ini adalah bentuk pewarisan yang paling umum dan sering digunakan.
  * Contoh: `Kucing(Hewan)`, `Anjing(Hewan)`.

### 2\. Pewarisan Berganda (Multiple Inheritance)

  * Sebuah kelas anak mewarisi dari **beberapa** kelas induk.
  * Python mendukung pewarisan berganda, tetapi bisa menjadi kompleks dan sulit dikelola jika tidak digunakan dengan hati-hati (masalah "Diamond Problem" / Method Resolution Order - MRO).
  * **Kapan Digunakan:** Ketika sebuah entitas menggabungkan karakteristik dari beberapa entitas lain yang tidak dapat direpresentasikan dalam hierarki tunggal yang jelas. Misalnya, sebuah `HybridCar` mungkin mewarisi dari `ElectricCar` dan `GasolineCar`.

<!-- end list -->

```python
# Contoh Pewarisan Berganda (Hanya konsep, perlu hati-hati dalam implementasi nyata)
class Pelari:
    def lari(self):
        print("Sedang berlari.")

class Perenang:
    def renang(self):
        print("Sedang berenang.")

class AtletTriathlon(Pelari, Perenang): # Mewarisi dari Pelari DAN Perenang
    def triathlon(self):
        print("Melakukan triathlon: lari, renang, bersepeda.")

atlet = AtletTriathlon()
atlet.lari()
atlet.renang()
atlet.triathlon()
```

**Catatan:** Meskipun Python mendukung pewarisan berganda, seringkali disarankan untuk menggunakan komposisi (memiliki objek dari kelas lain sebagai atribut) daripada pewarisan berganda untuk mengurangi kompleksitas, kecuali jika hubungan "adalah sebuah" sangat jelas dari beberapa induk.

-----

## F. Studi Kasus: Sistem Karyawan dengan Pewarisan

Mari kita kembangkan sistem karyawan kita menggunakan pewarisan. Kita akan memiliki kelas induk `Karyawan` dan kelas anak `Manajer` dan `Programmer`.

**Hierarki:**

  * `Karyawan` (Parent)
      * `Manajer` (Child)
      * `Programmer` (Child)

**Atribut Umum Karyawan:** `nama`, `id_karyawan`, `gaji`
**Metode Umum Karyawan:** `tampilkan_info()`

**Atribut Spesifik Manajer:** `jumlah_tim`
**Metode Spesifik Manajer:** `kelola_tim()`

**Atribut Spesifik Programmer:** `bahasa_utama`
**Metode Spesifik Programmer:** `tulis_kode()`

```python
class Karyawan:
    total_karyawan = 0

    def __init__(self, nama, id_karyawan, gaji):
        self._nama = nama
        self._id_karyawan = id_karyawan
        self._gaji = gaji
        Karyawan.total_karyawan += 1
        print(f"Karyawan '{self._nama}' dibuat.")

    @property
    def nama(self):
        return self._nama

    @property
    def id_karyawan(self):
        return self._id_karyawan

    @property
    def gaji(self):
        return self._gaji

    @gaji.setter
    def gaji(self, nilai_baru):
        if nilai_baru >= 0:
            self._gaji = nilai_baru
        else:
            print("Gaji tidak boleh negatif.")

    def tampilkan_info(self): # Metode umum
        print(f"\n--- Info Karyawan ---")
        print(f"Nama: {self.nama}")
        print(f"ID Karyawan: {self.id_karyawan}")
        print(f"Gaji: Rp {self.gaji:,}") # Format angka dengan koma
        print("---------------------")

class Manajer(Karyawan):
    def __init__(self, nama, id_karyawan, gaji, jumlah_tim):
        super().__init__(nama, id_karyawan, gaji) # Panggil constructor Karyawan
        self.jumlah_tim = jumlah_tim
        print(f"Manajer '{self.nama}' dibuat.")

    def kelola_tim(self): # Metode spesifik Manajer
        print(f"Manajer {self.nama} sedang mengelola {self.jumlah_tim} tim.")

    def tampilkan_info(self): # Override metode tampilkan_info dari Karyawan
        super().tampilkan_info() # Panggil metode tampilkan_info dari Karyawan
        print(f"Peran: Manajer")
        print(f"Jumlah Tim: {self.jumlah_tim}")
        print("---------------------")


class Programmer(Karyawan):
    def __init__(self, nama, id_karyawan, gaji, bahasa_utama):
        super().__init__(nama, id_karyawan, gaji) # Panggil constructor Karyawan
        self.bahasa_utama = bahasa_utama
        print(f"Programmer '{self.nama}' dibuat.")

    def tulis_kode(self): # Metode spesifik Programmer
        print(f"Programmer {self.nama} sedang menulis kode menggunakan {self.bahasa_utama}.")

    def tampilkan_info(self): # Override metode tampilkan_info dari Karyawan
        super().tampilkan_info() # Panggil metode tampilkan_info dari Karyawan
        print(f"Peran: Programmer")
        print(f"Bahasa Utama: {self.bahasa_utama}")
        print("---------------------")

# --- Penggunaan ---
m_andi = Manajer("Andi", "M001", 10000000, 3)
p_budi = Programmer("Budi", "P001", 7500000, "Python")
k_cici = Karyawan("Cici", "K001", 5000000)

print(f"\nTotal karyawan di perusahaan: {Karyawan.total_karyawan}")

m_andi.tampilkan_info()
p_budi.tampilkan_info()
k_cici.tampilkan_info()

m_andi.kelola_tim()
p_budi.tulis_kode()

# Contoh akses atribut yang diwarisi
print(f"\nGaji Budi: Rp {p_budi.gaji:,}")
p_budi.gaji = 8000000 # Menggunakan setter yang diwarisi
print(f"Gaji Budi setelah naik: Rp {p_budi.gaji:,}")

# Contoh metode yang di-override
p_budi.tampilkan_info()
```

**Penjelasan:**

  * Perhatikan bagaimana `Manajer` dan `Programmer` tidak perlu mendefinisikan ulang `nama`, `id_karyawan`, dan `gaji`, karena mereka mewarisi dari `Karyawan`.
  * Metode `tampilkan_info()` di-override di kelas anak untuk menambahkan informasi spesifik mereka, tetapi mereka tetap memanggil `super().tampilkan_info()` untuk menampilkan informasi umum dari kelas `Karyawan`. Ini adalah praktik terbaik.
  * Kita bisa memanggil metode spesifik (`kelola_tim`, `tulis_kode`) hanya pada objek dari kelas yang sesuai.

-----

### G. Tugas

1.  **Latihan Pewarisan & Enkapsulasi: Sistem Produk Toko Online**
    * Ambil kembali kelas `Produk` dari tugas pertemuan 4 Anda, yang sudah menerapkan enkapsulasi (getter/setter untuk `harga`, `stok`, dan `nama_produk` *read-only*).
    * Buatlah dua kelas anak baru yang mewarisi dari `Produk`:
        * `ProdukElektronik`:
            * Memiliki atribut tambahan: `garansi_bulan` (integer).
            * *Constructor*nya harus memanggil *constructor* `Produk` menggunakan `super()`.
            * Memiliki metode baru: `info_garansi()` yang mencetak informasi garansi produk elektronik tersebut.
            * *Override* metode `tampilkan_detail()` (jika ada, atau buat jika belum ada di `Produk`) untuk menambahkan informasi garansi.
        * `ProdukPakaian`:
            * Memiliki atribut tambahan: `ukuran` (misal: "S", "M", "L", "XL") dan `warna`.
            * *Constructor*nya harus memanggil *constructor* `Produk` menggunakan `super()`.
            * Memiliki metode baru: `info_pakaian()` yang mencetak ukuran dan warna pakaian.
            * *Override* metode `tampilkan_detail()` untuk menambahkan informasi ukuran dan warna.
    * Buat minimal dua objek dari masing-masing kelas anak (`ProdukElektronik` dan `ProdukPakaian`).
    * Tampilkan detail lengkap dari setiap objek menggunakan metode `tampilkan_detail()` yang sudah di-override.
    * Coba panggil metode spesifik dari masing-masing kelas anak (misal: `produk_elektronik.info_garansi()`, `produk_pakaian.info_pakaian()`).
    * Demonstrasikan bagaimana enkapsulasi masih berfungsi (misalnya, coba ubah harga atau stok melalui properti/metode yang diwarisi, dan perhatikan validasinya).

-----