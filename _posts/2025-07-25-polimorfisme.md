---
title: "PBO 6: Polimorfisme"
date: 2025-07-25 09:00:00 +0700
categories: [Materi Kuliah, Pemrograman Berorientasi Objek (PBO)]
tags: [kuliah, pbo] # TAG names should always be lowercase
toc: true
---
## Tujuan Pembelajaran:

Pada akhir pertemuan ini, mahasiswa diharapkan mampu:

1.  Menjelaskan konsep **polimorfisme** dalam Pemrograman Berorientasi Objek.
2.  Memahami bagaimana polimorfisme diimplementasikan di Python melalui *method overriding*.
3.  Memahami konsep **Duck Typing** di Python sebagai bentuk polimorfisme yang fleksibel.
4.  Mengaplikasikan polimorfisme untuk membuat kode yang lebih fleksibel, *reusable*, dan mudah diperluas.
5.  Menerapkan konsep polimorfisme pada studi kasus yang relevan.

-----

## A. Apa Itu Polimorfisme?

Istilah "polimorfisme" berasal dari bahasa Yunani: "poly" (banyak) dan "morph" (bentuk). Jadi, **polimorfisme** berarti "banyak bentuk".

Dalam konteks PBO, polimorfisme adalah kemampuan objek dari kelas yang berbeda untuk merespons panggilan metode yang sama dengan cara yang berbeda, sesuai dengan implementasi masing-masing kelas.

**Analogi "Tombol Saklar Universal":**

Bayangkan Anda memiliki sebuah saklar listrik universal. Saklar ini bisa menyalakan berbagai perangkat:

  * Jika Anda menekan saklar saat terhubung ke **lampu**, lampu akan **menyala**.
  * Jika Anda menekan saklar saat terhubung ke **kipas angin**, kipas angin akan **berputar**.
  * Jika Anda menekan saklar saat terhubung ke **mesin cuci**, mesin cuci akan **bekerja**.

Setiap perangkat (objek) merespons aksi "menekan saklar" (panggilan metode) dengan perilakunya sendiri yang spesifik, meskipun aksi awalnya sama. Inilah polimorfisme: satu perintah, banyak kemungkinan hasil tergantung pada objek yang menerima perintah tersebut.

**Manfaat Polimorfisme:**

1.  **Fleksibilitas Kode:** Anda dapat menulis kode yang bekerja dengan objek dari berbagai kelas, selama objek-objek tersebut memiliki metode dengan nama yang sama. Ini membuat kode lebih generik.
2.  **Ekstensibilitas:** Sangat mudah untuk menambahkan kelas baru dengan perilaku yang berbeda tanpa harus mengubah kode yang sudah ada. Cukup pastikan kelas baru mengimplementasikan metode yang relevan.
3.  **Kode Lebih Bersih dan Terorganisir:** Mengurangi kebutuhan akan banyak pernyataan `if-elif-else` untuk memeriksa tipe objek sebelum melakukan aksi.
4.  **Reusabilitas:** Komponen yang dirancang secara polimorfik dapat digunakan kembali di berbagai konteks.

-----

## B. Polimorfisme Melalui *Method Overriding*

Kita sudah sedikit melihat ini di pertemuan Pewarisan. Ketika kelas anak mengimplementasikan kembali metode yang sudah ada di kelas induk, itu disebut *method overriding*. Ini adalah salah satu bentuk utama polimorfisme.

**Contoh: Hewan Bersuara**

```python
# Kelas Induk
class Hewan:
    def __init__(self, nama):
        self.nama = nama

    def bersuara(self): # Metode umum
        print(f"{self.nama} mengeluarkan suara yang umum.")

# Kelas Anak 1
class Kucing(Hewan):
    def bersuara(self): # Override metode bersuara
        print(f"{self.nama} mengeong.")

# Kelas Anak 2
class Anjing(Hewan):
    def bersuara(self): # Override metode bersuara
        print(f"{self.nama} menggonggong.")

# Kelas Anak 3 (contoh baru)
class Sapi(Hewan):
    def bersuara(self): # Override metode bersuara
        print(f"{self.nama} melenguh.")

# --- Penggunaan Polimorfisme ---

# Buat list objek dari berbagai kelas Hewan
daftar_hewan = [
    Kucing("Kitty"),
    Anjing("Buddy"),
    Sapi("MooMoo"),
    Hewan("Hewan Misterius") # Objek dari kelas induk
]

print("--- Semua Hewan Bersuara ---")
for hewan in daftar_hewan:
    # Memanggil metode bersuara() yang sama pada objek yang berbeda
    # Python secara otomatis memanggil implementasi yang benar
    hewan.bersuara()
# Output:
# Kitty mengeong.
# Buddy menggonggong.
# MooMoo melenguh.
# Hewan Misterius mengeluarkan suara yang umum.

```

Dalam contoh di atas, kita memanggil `hewan.bersuara()` dalam loop, dan meskipun variabel `hewan` pada setiap iterasi mungkin adalah objek `Kucing`, `Anjing`, `Sapi`, atau `Hewan` itu sendiri, panggilan `bersuara()` selalu melakukan tindakan yang *benar* untuk tipe objek spesifik tersebut. Inilah polimorfisme dalam aksi.

-----

## C. Polimorfisme dengan Fungsi (Global)

Polimorfisme tidak hanya terbatas pada metode di dalam kelas. Anda juga bisa menerapkannya dengan fungsi di luar kelas yang bisa beroperasi pada objek dari tipe berbeda.

```python
# Kelas-kelas yang sama dari contoh sebelumnya
# ... (Kelas Hewan, Kucing, Anjing, Sapi ada di sini) ...

# Fungsi global yang menerima objek dan memanggil metode bersuara
def panggil_suara(objek_hewan):
    objek_hewan.bersuara()

print("\n--- Panggil Suara via Fungsi Global ---")
kucing_saya = Kucing("Si Meong")
anjing_teman = Anjing("Si Gukguk")
sapi_petani = Sapi("Si Mooo")

panggil_suara(kucing_saya)  # Output: Si Meong mengeong.
panggil_suara(anjing_teman) # Output: Si Gukguk menggonggong.
panggil_suara(sapi_petani)  # Output: Si Mooo melenguh.
```

Fungsi `panggil_suara()` tidak peduli apakah itu objek `Kucing`, `Anjing`, atau `Sapi`. Selama objek tersebut memiliki metode `bersuara()`, fungsi ini akan bekerja.

-----

## D. Duck Typing di Python

Python memiliki konsep polimorfisme yang sangat kuat dan fleksibel yang dikenal sebagai **Duck Typing**.

  * **Filosofi:** "Jika sesuatu berjalan seperti bebek, berenang seperti bebek, dan bersuara seperti bebek, maka itu adalah bebek."
  * **Artinya dalam Python:** Python tidak peduli *tipe* objek apa itu (apakah itu `Kucing`, `Anjing`, atau `Pesawat`). Yang Python pedulikan adalah apakah objek tersebut memiliki *metode atau atribut yang dibutuhkan* oleh operasi yang sedang dilakukan. Jika objek memiliki metode yang diperlukan, maka ia akan bekerja.

Ini berbeda dengan bahasa yang *statically typed* (seperti Java atau C++) di mana Anda harus secara eksplisit menyatakan bahwa sebuah objek adalah turunan dari kelas tertentu atau mengimplementasikan sebuah *interface* agar polimorfisme berfungsi. Python tidak memerlukan deklarasi eksplisit semacam itu, membuat kode lebih ringkas dan fleksibel.

**Contoh Duck Typing:**

```python
class Bebek:
    def bersuara(self):
        print("Kwek kwek!")
    def bergerak(self):
        print("Berenang...")

class Ayam:
    def bersuara(self):
        print("Kokok petok!")
    def bergerak(self):
        print("Berjalan...")

class Robot: # Robot bukan hewan, tapi punya metode yang sama
    def bersuara(self):
        print("Beep boop!")
    def bergerak(self):
        print("Bergerak dengan roda.")

def lakukan_aksi_hewan(objek):
    # Fungsi ini tidak peduli tipe objeknya, asalkan punya metode bersuara() dan bergerak()
    print("--- Lakukan Aksi ---")
    objek.bersuara()
    objek.bergerak()
    print("--------------------")

bebek = Bebek()
ayam = Ayam()
robot = Robot()

lakukan_aksi_hewan(bebek)
lakukan_aksi_hewan(ayam)
lakukan_aksi_hewan(robot) # Robot bukan hewan, tapi ia "berperilaku" seperti hewan di sini
```

**Diskusi Duck Typing:**

  * Fungsi `lakukan_aksi_hewan` bekerja dengan `Bebek`, `Ayam`, dan bahkan `Robot`, meskipun `Robot` tidak ada dalam hierarki pewarisan yang sama dengan `Bebek` dan `Ayam`.
  * Ini dimungkinkan karena semua objek tersebut memiliki metode `bersuara()` dan `bergerak()`. Python hanya mencoba memanggil metode tersebut; jika ada, ia akan berhasil.
  * Duck Typing memberikan fleksibilitas luar biasa, tetapi juga membutuhkan programmer untuk berhati-hati agar objek yang diteruskan benar-benar memiliki metode yang diharapkan.

-----

## E. Studi Kasus: Sistem Manajemen Produk dengan Polimorfisme

Kita akan melanjutkan dari tugas sebelumnya dengan kelas `Produk`, `ProdukElektronik`, dan `ProdukPakaian`. Kita akan menggunakan polimorfisme untuk mencetak informasi harga jual dengan pajak secara fleksibel.

**Tujuan:** Kita ingin bisa menghitung dan menampilkan harga jual untuk berbagai jenis produk (Produk umum, ProdukElektronik, ProdukPakaian) menggunakan satu mekanisme yang sama, meskipun perhitungan atau tampilan detailnya bisa sedikit berbeda.

```python
import datetime

# --- Kelas Produk (dari pertemuan sebelumnya, disederhanakan untuk fokus) ---
class Produk:
    def __init__(self, nama_produk, harga, stok):
        self._nama_produk = nama_produk
        self._harga = harga # Asumsikan sudah divalidasi dari pertemuan 4
        self._stok = stok   # Asumsikan sudah divalidasi dari pertemuan 4

    @property
    def nama_produk(self):
        return self._nama_produk

    @property
    def harga(self):
        return self._harga

    @property
    def stok(self):
        return self._stok

    def hitung_harga_jual(self, pajak_persen=0.10): # Metode ini akan di-override
        return self._harga * (1 + pajak_persen)

    def tampilkan_detail(self): # Metode ini akan di-override
        print(f"Produk: {self.nama_produk}, Harga: Rp{self.harga:,}, Stok: {self.stok}")

# --- Kelas ProdukElektronik (Child dari Produk) ---
class ProdukElektronik(Produk):
    def __init__(self, nama_produk, harga, stok, garansi_bulan):
        super().__init__(nama_produk, harga, stok)
        self.garansi_bulan = garansi_bulan

    def info_garansi(self):
        print(f"Produk ini memiliki garansi selama {self.garansi_bulan} bulan.")

    def hitung_harga_jual(self, pajak_persen=0.10): # Override: misal ada diskon khusus
        # Diskon 5% untuk produk elektronik
        harga_dasar_setelah_pajak = super().hitung_harga_jual(pajak_persen)
        return harga_dasar_setelah_pajak * 0.95 # Diskon 5%

    def tampilkan_detail(self): # Override
        super().tampilkan_detail()
        print(f"  > Garansi: {self.garansi_bulan} bulan.")


# --- Kelas ProdukPakaian (Child dari Produk) ---
class ProdukPakaian(Produk):
    def __init__(self, nama_produk, harga, stok, ukuran, warna):
        super().__init__(nama_produk, harga, stok)
        self.ukuran = ukuran
        self.warna = warna

    def info_pakaian(self):
        print(f"Ukuran: {self.ukuran}, Warna: {self.warna}.")

    def tampilkan_detail(self): # Override
        super().tampilkan_detail()
        print(f"  > Ukuran: {self.ukuran}, Warna: {self.warna}.")

# --- Penggunaan Polimorfisme ---

# Membuat objek dari berbagai jenis produk
produk_umum = Produk("Tas Belanja", 50000, 100)
laptop = ProdukElektronik("Laptop Asus", 10000000, 10, 12)
kemeja = ProdukPakaian("Kemeja Flanel", 250000, 50, "M", "Merah")
smartphone = ProdukElektronik("Samsung Galaxy", 7000000, 20, 24)

# Menyimpan semua produk dalam satu list, meskipun tipenya berbeda
daftar_produk = [produk_umum, laptop, kemeja, smartphone]

print("--- Menampilkan Detail dan Harga Jual Semua Produk (Polimorfisme) ---")
for produk in daftar_produk:
    produk.tampilkan_detail() # Panggilan metode yang sama, hasil berbeda
    harga_jual = produk.hitung_harga_jual() # Panggilan metode yang sama, hasil berbeda
    print(f"  > Harga Jual (termasuk pajak & diskon jika ada): Rp{harga_jual:,.2f}\n")

# Output akan menunjukkan bahwa tampilkan_detail() dan hitung_harga_jual()
# memberikan output yang berbeda sesuai dengan tipe objeknya (Produk, Elektronik, Pakaian)

# Contoh Duck Typing dengan fungsi yang memeriksa metode
def cetak_laporan_stok(objek_item):
    # Fungsi ini tidak peduli apa tipe objek_item, asalkan ia punya 'nama_produk' dan 'stok'
    print(f"Laporan Stok: '{objek_item.nama_produk}' tersisa {objek_item.stok} unit.")

print("--- Laporan Stok Menggunakan Duck Typing ---")
cetak_laporan_stok(laptop)
cetak_laporan_stok(kemeja)
cetak_laporan_stok(produk_umum)

# Bahkan objek yang tidak berhubungan bisa bekerja jika memenuhi "Duck Typing"
class KotakKosong:
    def __init__(self, nama, jumlah):
        self.nama_produk = nama
        self.stok = jumlah

cetak_laporan_stok(KotakKosong("Kotak Kardus", 500))
```

**Diskusi:**

  * Ketika kita mengiterasi `daftar_produk`, setiap objek (`produk_umum`, `laptop`, `kemeja`, `smartphone`) merespons panggilan `tampilkan_detail()` dan `hitung_harga_jual()` dengan cara yang spesifik untuk kelasnya. Ini adalah inti dari polimorfisme.
  * Perhatikan bahwa `hitung_harga_jual` di `ProdukElektronik` di-override untuk memberikan diskon khusus, sementara `ProdukPakaian` menggunakan implementasi default dari kelas induk `Produk`.
  * Contoh `cetak_laporan_stok` menunjukkan Duck Typing: fungsi tersebut hanya membutuhkan atribut `nama_produk` dan `stok`, tanpa peduli asal kelas objek. Ini membuat kode sangat fleksibel.

-----