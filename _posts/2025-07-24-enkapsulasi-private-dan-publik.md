---
title: "PBO 4: Enkapsulasi: Private dan Public"
date: 2025-07-24 08:00:00 +0700
categories: [Materi Kuliah, Pemrograman Berorientasi Objek (PBO)]
tags: [kuliah, pbo] # TAG names should always be lowercase
toc: true
---
## Tujuan Pembelajaran:

Pada akhir pertemuan ini, mahasiswa diharapkan mampu:

1.  Menjelaskan konsep **enkapsulasi** dan mengapa hal itu penting dalam Pemrograman Berorientasi Objek.
2.  Memahami bagaimana Python menerapkan konsep *private* dan *public* pada atribut dan metode.
3.  Mengimplementasikan **getter** dan **setter** menggunakan konvensi dan `@property` Python untuk mengontrol akses data.
4.  Menerapkan prinsip enkapsulasi pada studi kasus yang relevan.

-----

## A. Apa Itu Enkapsulasi?

Bayangkan sebuah kapsul obat. Di dalamnya, ada berbagai bahan aktif yang penting, tetapi Anda tidak perlu tahu komposisi pastinya atau bagaimana mereka bekerja sama. Anda cukup tahu bahwa minum kapsul itu akan membantu Anda sembuh. Anda hanya berinteraksi dengan "permukaan luar" kapsul.

Nah, **enkapsulasi** dalam PBO memiliki filosofi yang mirip:

  * **Penggabungan Data dan Perilaku:** Enkapsulasi berarti membungkus (menggabungkan) **data (atribut)** dan **kode (metode)** yang beroperasi pada data tersebut ke dalam satu unit tunggal, yaitu **objek**. Ini seperti yang sudah kita lakukan di pertemuan sebelumnya dengan kelas `Buku` atau `Mahasiswa`. Data buku (judul, penulis, status) digabungkan dengan perilaku buku (pinjam, kembalikan) dalam satu objek `Buku`.

  * **Penyembunyian Informasi (Information Hiding):** Ini adalah aspek terpenting dari enkapsulasi. Artinya, menyembunyikan detail implementasi internal suatu objek dari dunia luar. Pengguna objek tidak perlu tahu *bagaimana* data disimpan atau *bagaimana* metode bekerja di baliknya. Mereka hanya perlu tahu *apa* yang bisa dilakukan objek tersebut (melalui antarmuka publiknya).

**Mengapa Enkapsulasi Penting?**

1.  **Proteksi Data (Data Protection):** Mencegah akses langsung dan modifikasi yang tidak diinginkan terhadap data internal objek. Ini seperti melindungi mesin mobil agar tidak semua orang bisa langsung mengutak-atiknya.
2.  **Modularitas:** Setiap objek menjadi unit yang mandiri. Perubahan pada implementasi internal suatu objek tidak akan memengaruhi bagian lain dari program, selama antarmuka publiknya tetap sama.
3.  **Kemudahan Pemeliharaan dan Debugging:** Jika ada masalah, kita tahu bahwa masalah itu kemungkinan besar ada di dalam objek tersebut, sehingga lebih mudah untuk menemukan dan memperbaikinya.
4.  **Fleksibilitas:** Kita bisa mengubah bagaimana data disimpan atau diproses di dalam objek tanpa harus mengubah kode yang menggunakan objek tersebut, selama metode publiknya tetap sama.
5.  **Kontrol Akses:** Memungkinkan kita untuk menerapkan logika validasi atau aturan bisnis saat data diatur atau diakses. Misalnya, kita bisa memastikan usia tidak negatif, atau saldo bank tidak bisa menjadi minus tanpa persetujuan khusus.

-----

## B. Konsep *Private* dan *Public* di Python

Tidak seperti beberapa bahasa pemrograman lain (seperti Java atau C++) yang memiliki kata kunci eksplisit (`private`, `public`, `protected`), Python mengadopsi pendekatan yang sedikit berbeda dan lebih fleksibel untuk enkapsulasi, yang dikenal sebagai "**Konvensi Penamaan**" dan "Name Mangling".

### 1\. Anggota *Public*

  * **Definisi:** Atribut atau metode yang dapat diakses secara langsung dari luar kelas.
  * **Konvensi:** Tidak ada underscore di awal nama. Ini adalah default di Python.
  * **Contoh:** `self.nama`, `self.tampilkan_info()`.

### 2\. Anggota *Protected* (Konvensi Saja)

  * **Definisi:** Anggota yang dimaksudkan untuk tidak diakses secara langsung dari luar kelas, tetapi boleh diakses oleh kelas-kelas turunan (akan dibahas di Pewarisan).

  * **Konvensi:** Dimulai dengan **satu underscore tunggal (`_`)**.

  * **Contoh:** `_umur`, `_hitung_internal()`.

  * **Penting:** Ini hanyalah sebuah **konvensi**. Python tidak benar-benar mencegah Anda mengakses `_umur` dari luar kelas. Programmer lain diharapkan untuk menghormati konvensi ini dan tidak mengaksesnya secara langsung.

    ```python
    class Karyawan:
        def __init__(self, nama, gaji):
            self.nama_public = nama      # Atribut Public
            self._gaji_protected = gaji  # Atribut Protected (konvensi)

        def tampil_gaji(self):          # Metode Public
            print(f"Gaji {self.nama_public} (protected): {self._gaji_protected}")

    k = Karyawan("Budi", 5000000)
    print(k.nama_public) # Output: Budi (Akses langsung diperbolehkan)
    print(k._gaji_protected) # Output: 5000000 (Secara teknis bisa diakses, tapi tidak disarankan)
    ```

### 3\. Anggota *Private* (Name Mangling)

  * **Definisi:** Anggota yang secara teknis ingin "disembunyikan" dari akses langsung di luar kelas dan bahkan dari kelas turunan.

  * **Konvensi:** Dimulai dengan **dua underscore (`__`)** di awal.

  * **Contoh:** `__saldo`, `__proses_rahasia()`.

  * **Mekanisme Python (Name Mangling):** Ketika Anda menggunakan dua underscore di awal (`__nama_atribut`), Python melakukan "name mangling". Ini berarti Python akan secara otomatis mengubah nama atribut tersebut menjadi `_NamaKelas__nama_atribut` di balik layar. Jadi, `__saldo` dalam kelas `AkunBank` akan menjadi `_AkunBank__saldo`. Hal ini membuat akses langsung dari luar kelas menjadi lebih sulit (tapi tidak sepenuhnya mustahil, hanya butuh usaha lebih). Ini adalah bentuk enkapsulasi yang lebih kuat di Python.

    ```python
    class AkunBank:
        def __init__(self, nama, saldo_awal):
            self.pemilik = nama          # Public
            self.__saldo = saldo_awal   # Private (menggunakan name mangling)

        def setor(self, jumlah):
            if jumlah > 0:
                self.__saldo += jumlah
                print(f"Setor {jumlah}. Saldo baru: {self.__saldo}")
            else:
                print("Jumlah setor harus positif.")

        def tarik(self, jumlah):
            if 0 < jumlah <= self.__saldo:
                self.__saldo -= jumlah
                print(f"Tarik {jumlah}. Saldo baru: {self.__saldo}")
            else:
                print("Jumlah tarik tidak valid atau saldo tidak cukup.")

    my_account = AkunBank("Alice", 1000)
    my_account.setor(500)  # Output: Setor 500. Saldo baru: 1500
    my_account.tarik(200)  # Output: Tarik 200. Saldo baru: 1300

    # Coba akses atribut private secara langsung
    # print(my_account.__saldo) # Ini akan menghasilkan AttributeError!
    # Output: AttributeError: 'AkunBank' object has no attribute '__saldo'

    # Kita bisa mengaksesnya secara tidak langsung (melalui name mangling)
    print(my_account._AkunBank__saldo) # Output: 1300 (Tidak disarankan untuk diakses langsung)
    ```

    **Catatan Penting:** Meskipun Python tidak memiliki kata kunci `private` yang "benar-benar" melarang akses, konvensi `_` dan `__` sangat penting dalam komunitas Python untuk menunjukkan maksud programmer. **Hormati konvensi ini\!** Jika sebuah atribut atau metode diawali dengan `_` atau `__`, itu berarti Anda tidak boleh mengaksesnya atau memodifikasinya secara langsung dari luar kelas, melainkan melalui metode publik yang disediakan.

-----

## C. Getter dan Setter (Properti dengan `@property`)

Meskipun kita bisa mengakses atribut *public* secara langsung, seringkali kita ingin memiliki kontrol lebih saat atribut diakses (di-*get*) atau diubah (di-*set*). Di sinilah konsep **Getter** dan **Setter** berperan.

  * **Getter (Accessor):** Metode yang digunakan untuk mendapatkan (membaca) nilai dari sebuah atribut.
  * **Setter (Mutator):** Metode yang digunakan untuk mengatur (mengubah) nilai dari sebuah atribut. Biasanya melibatkan validasi.

Di Python, kita dapat mengimplementasikan getter dan setter menggunakan properti dengan dekorator `@property`. Ini adalah cara yang sangat "Pythonic" (sesuai gaya Python) dan elegan untuk enkapsulasi.

### Contoh: Kelas `Pegawai` dengan Getter dan Setter

Mari kita buat kelas `Pegawai` di mana kita ingin memastikan `gaji` selalu positif dan `email` memiliki format yang valid.

```python
class Pegawai:
    def __init__(self, nama, email, gaji):
        self._nama = nama  # Atribut 'protected' (konvensi)
        self._email = email
        self._gaji = gaji

    # --- Getter untuk Nama (bisa diakses langsung, tapi ini contoh) ---
    @property
    def nama(self):
        print("Mengakses nama...")
        return self._nama

    # --- Getter & Setter untuk Email ---
    @property
    def email(self):
        print("Mengakses email...")
        return self._email

    @email.setter
    def email(self, new_email):
        print("Mengatur email...")
        if "@" in new_email and "." in new_email:
            self._email = new_email
            print(f"Email berhasil diubah menjadi: {self._email}")
        else:
            print("Error: Format email tidak valid.")

    # --- Getter & Setter untuk Gaji ---
    @property
    def gaji(self):
        print("Mengakses gaji...")
        return self._gaji

    @gaji.setter
    def gaji(self, new_gaji):
        print("Mengatur gaji...")
        if new_gaji >= 0:
            self._gaji = new_gaji
            print(f"Gaji berhasil diubah menjadi: {self._gaji}")
        else:
            print("Error: Gaji tidak boleh negatif.")

# --- Penggunaan Kelas Pegawai ---
pegawai1 = Pegawai("Dian", "dian@example.com", 7000000)

print(f"Nama Pegawai: {pegawai1.nama}") # Memanggil getter 'nama'

print(f"Email Awal: {pegawai1.email}")  # Memanggil getter 'email'
pegawai1.email = "dian.baru@company.com" # Memanggil setter 'email'
pegawai1.email = "email_invalid"          # Memanggil setter 'email' dengan data tidak valid

print(f"Gaji Awal: {pegawai1.gaji}")    # Memanggil getter 'gaji'
pegawai1.gaji = 7500000                 # Memanggil setter 'gaji'
pegawai1.gaji = -100000                 # Memanggil setter 'gaji' dengan data tidak valid

# Perhatikan bagaimana kita memanggilnya seperti atribut biasa (pegawai1.gaji),
# tetapi di belakang layar, Python memanggil metode getter atau setter yang sesuai.
```

**Penjelasan `@property`:**

  * **`@property` (getter):** Diletakkan di atas metode yang berfungsi sebagai getter. Metode ini tidak menerima parameter selain `self` dan harus mengembalikan nilai atribut. Nama metode ini akan menjadi nama properti yang bisa diakses.
  * **`@nama_properti.setter`:** Diletakkan di atas metode yang berfungsi sebagai setter. Metode ini harus memiliki nama yang sama dengan getter (`nama_properti`) dan menerima satu parameter tambahan (nilai baru) selain `self`.

Pendekatan `@property` ini sangat bagus karena:

1.  **Sintaks Bersih:** Dari luar, Anda berinteraksi dengan `pegawai1.gaji` seperti atribut biasa, bukan `pegawai1.get_gaji()` atau `pegawai1.set_gaji(nilai)`.
2.  **Kontrol Penuh:** Meskipun terlihat seperti akses langsung, sebenarnya Anda memiliki logika validasi di balik layar.
3.  **Fleksibilitas Evolusi:** Anda bisa memulai dengan atribut *public* biasa, dan jika nanti Anda membutuhkan validasi, Anda bisa dengan mudah mengubahnya menjadi properti dengan `@property` tanpa mengubah kode klien yang menggunakan atribut tersebut.

-----

## D. Studi Kasus: Meningkatkan Kelas `Buku` dengan Enkapsulasi

Mari kita terapkan konsep enkapsulasi pada kelas `Buku` kita. Kita ingin memastikan beberapa hal:

  * `tahun_terbit` hanya bisa diatur sekali saat inisialisasi dan tidak bisa diubah sesudahnya.
  * `status` buku hanya bisa diubah melalui metode `pinjam()` dan `kembalikan()`.

<!-- end list -->

```python
import datetime

class Buku:
    daftar_semua_buku = []
    jumlah_buku_terdaftar = 0

    def __init__(self, judul, penulis, tahun_terbit):
        # Menggunakan _ di awal untuk menunjukkan ini adalah atribut internal
        # yang akan diakses melalui property (jika perlu)
        self._judul = judul
        self._penulis = penulis
        # Tahun terbit ini akan kita jadikan 'read-only' dari luar
        if not Buku._validasi_tahun_internal(tahun_terbit):
            raise ValueError("Tahun terbit tidak valid! Harus antara 1500 dan tahun sekarang.")
        self.__tahun_terbit = tahun_terbit # Atribut private karena tidak boleh diubah

        self.__status = "Tersedia" # Atribut private, hanya bisa diubah via metode pinjam/kembalikan
        Buku.jumlah_buku_terdaftar += 1
        Buku.daftar_semua_buku.append(self)

    # --- Properti Getter untuk Judul (Contoh, bisa juga langsung public) ---
    @property
    def judul(self):
        return self._judul

    # --- Properti Getter untuk Penulis ---
    @property
    def penulis(self):
        return self._penulis

    # --- Properti Getter (read-only) untuk Tahun Terbit ---
    @property
    def tahun_terbit(self):
        return self.__tahun_terbit # Mengakses atribut private

    # --- Properti Getter (read-only) untuk Status ---
    @property
    def status(self):
        return self.__status # Mengakses atribut private

    # --- Metode untuk mengubah status (enkapsulasi perilaku) ---
    def pinjam(self):
        if self.__status == "Tersedia":
            self.__status = "Dipinjam"
            print(f"Buku '{self._judul}' berhasil dipinjam.")
        else:
            print(f"Maaf, buku '{self._judul}' sedang '{self.__status}'. Tidak bisa dipinjam.")

    def kembalikan(self):
        if self.__status == "Dipinjam":
            self.__status = "Tersedia"
            print(f"Buku '{self._judul}' berhasil dikembalikan.")
        else:
            print(f"Buku '{self._judul}' tidak dalam status dipinjam.")

    def tampilkan_detail(self):
        print(f"\n--- Detail Buku ({self.judul}) ---")
        print(f"Judul: {self.judul}") # Memanggil properti
        print(f"Penulis: {self.penulis}") # Memanggil properti
        print(f"Tahun Terbit: {self.tahun_terbit}") # Memanggil properti
        print(f"Status: {self.status}") # Memanggil properti
        print("-------------------")

    @classmethod
    def tampilkan_total_buku(cls):
        print(f"\nTotal buku yang terdaftar di sistem: {cls.jumlah_buku_terdaftar} buku.")

    @staticmethod
    def _validasi_tahun_internal(tahun): # Metode statis ini dibuat 'protected'
        tahun_sekarang = datetime.datetime.now().year
        return 1500 <= tahun <= tahun_sekarang

# --- Penggunaan Kelas Buku dengan Enkapsulasi ---
try:
    b1 = Buku("Harry Potter", "J.K. Rowling", 1997)
    b2 = Buku("Filosofi Teras", "Henry Manampiring", 2019)
    # b_invalid = Buku("Buku Masa Depan", "X", 2030) # Ini akan memicu ValueError
except ValueError as e:
    print(f"Error saat membuat buku: {e}")

b1.tampilkan_detail()
b2.tampilkan_detail()

# Coba mengubah status secara langsung (tidak disarankan)
# b1.__status = "Hilang" # Ini tidak akan bekerja seperti yang diharapkan karena name mangling

# Mengakses properti (seperti atribut biasa)
print(f"Judul buku 1: {b1.judul}")
print(f"Tahun terbit buku 1: {b1.tahun_terbit}")

# Coba mengubah tahun terbit (tidak bisa karena hanya getter)
# b1.tahun_terbit = 2000 # Ini akan menghasilkan AttributeError

# Mengubah status melalui metode yang dienkapsulasi
b1.pinjam()
b1.tampilkan_detail()
b1.kembalikan()
b1.tampilkan_detail()

Buku.tampilkan_total_buku()
```

**Penjelasan:**

  * Perhatikan penggunaan `self.__tahun_terbit` dan `self.__status` untuk atribut yang ingin kita jadikan *private*.
  * Kita menyediakan properti `tahun_terbit` dan `status` hanya dengan **getter**, tanpa setter. Ini membuatnya menjadi properti **read-only** dari luar kelas. Pengguna bisa membaca nilainya, tetapi tidak bisa mengubahnya secara langsung.
  * Perubahan `status` hanya dapat terjadi melalui metode `pinjam()` dan `kembalikan()`, yang berarti logika bisnis (misalnya, memastikan buku tersedia sebelum dipinjam) terkunci di dalam metode tersebut, tidak bisa diakali dari luar.
  * Metode `_validasi_tahun_internal` diberi awalan `_` untuk menunjukkan bahwa ini adalah metode internal kelas yang tidak dimaksudkan untuk dipanggil langsung dari luar.

-----

### E. Tugas

1.  **Refactor Kelas `Produk` dengan Enkapsulasi:**

      * Ambil kelas `Produk` dari tugas pertemuan 3.
      * Terapkan enkapsulasi pada atribut `harga` dan `stok` menggunakan `@property` (getter dan setter).
      * Pastikan `harga` tidak bisa negatif.
      * Pastikan `stok` tidak bisa menjadi negatif saat `kurangi_stok()` dipanggil (gunakan logika validasi di setter `stok` atau di metode `kurangi_stok`).
      * Jadikan `nama_produk` sebagai properti *read-only* (hanya getter, tanpa setter).
      * Pastikan semua akses dan modifikasi data dilakukan melalui properti atau metode yang sesuai.
      * Tuliskan skenario penggunaan yang menunjukkan bagaimana Anda mengakses dan memodifikasi data, serta bagaimana validasi bekerja saat ada input yang tidak valid.

-----