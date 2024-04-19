---
title: Membuat Blog Gratis dengan GitHub Pages dan Jekyll
date: 2024-04-09 11:00:00 +0700
categories: [Blog, Tutorial]
tags: [github pages, jekyll] # TAG names should always be lowercase
---

## Apa itu GitHub Pages?
Ada banyak penyedia layanan untuk meng-*host* situs web, salah satunya adalah GitHub Pages. **GitHub Pages adalah layanan hosting situs web statis** yang disediakan oleh GitHub (sebuah platform berbagi kode program) untuk para pengembang. GitHub Pages memungkinkan kita untuk meng-*host* file statis seperti HTML, CSS, JavaScript, gambar, dll. GitHub Pages juga memberikan subdomain dengan format .github.io untuk mengakses situs web yang kita buat, contohnya blog yang sedang kamu baca sekarang ([initial-as.github.io/blog](https://initial-as.github.io/blog)).
### Keuntungan Menggunakan GitHub Pages
-   **Gratis**: Kita bisa menggunakan GitHub Pages tanpa biaya.
-   **Mudah**: Kita hanya perlu mengunggah file statis ke repositori GitHub, dan GitHub Pages akan meng-*host*-nya secara otomatis.
-   ***Version Control***: Kode situs web kita akan diarsipkan menggunakan Git, sehingga kita dapat melacak perubahan dan mengelola versi dengan mudah.
-   **Subdomain**: Kita akan mendapatkan subdomain gratis dengan format  **nama-akun-github.github.io**.

## Situs Web Statis
Situs web statis terdiri dari satu atau lebih halaman web HTML yang selalu dimuat dengan cara yang sama. Berbeda dengan situs web dinamis, yang mengubah tampilan berdasarkan input data yang berubah (seperti lokasi pengguna, waktu, atau tindakan pengguna), halaman web statis adalah file HTML sederhana yang dapat dimuat dengan cepat.

***Static Site Generator* (SSG)** atau **generator situs web statis** adalah alat yang digunakan untuk menghasilkan situs web HTML statis berdasarkan data mentah dan *template*. SSG menghasilkan halaman web statis sebelum halaman web diluncurkan, konten diproses sebelumnya dan disajikan sebagai file HTML biasa.

### Sejarah Singkat *Static Site Generator*
1.  **Awal Mula Situs Statis**:
    Pada awalnya, situs web sepenuhnya statis dibangun dengan HTML sederhana. Pendekatan ini berfungsi dengan baik karena website pertama tidak memerlukan lebih dari server file statis yang sederhana. Namun, seiring perkembangan web, kebutuhan berubah.

2.  **Era Bahasa *Server-Side***: Seiring web berkembang, orang mulai menggunakan bahasa server-side untuk menghasilkan HTML secara dinamis. Bahasa seperti PHP, Ruby, dan Perl digunakan untuk menghasilkan konten yang lebih kompleks. Inilah awal mula penggunaan situs web dinamis.

3.  **Munculnya *Content Management Systems* (CMS)**: Tidak semua penulis adalah programmer. Oleh karena itu, orang-orang menciptakan CMS untuk memudahkan pemasaran dan manajemen konten tanpa perlu menyentuh kode. CMS pertama adalah sistem CMS perusahaan seperti FileNet dan Documentum. Namun, pada tahun 2003, WordPress muncul sebagai CMS open-source yang cepat menjadi yang paling populer di web.

4.  **Jekyll dan SSG Generasi Pertama**: Pada saat itu, beberapa orang merasa CMS seperti WordPress terlalu rumit. Saat itulah  **Jekyll**  muncul, Tom Preston-Werner merilisnya pada tahun 2008[^fn-nth-1]. Jekyll memperkenalkan konsep  ***static site generator*** dan memulai tren pengembangan web dengan kecenderungan pada situs web statis[^fn-nth-2]. Berbeda dengan WordPress, Jekyll membangun HTML pada saat  _build-time_  daripada  _runtime_, yang lebih sederhana dan lebih efisien untuk dijalankan di server. GitHub juga mengadopsi Jekyll untuk GitHub Pages, yang semakin meningkatkan popularitasnya.

5.  **Evolusi SSG**: Setelah Jekyll, banyak SSG lainnya muncul, membantu kategori  _static site generator_  berkembang pesat dalam pengembangan web. Terutama dengan munculnya konsep  **Jamstack**, SSG semakin relevan dan bermanfaat untuk membangun situs besar tanpa mengorbankan performa.[^fn-nth-3][^fn-nth-4]

### Situs Web Statis vs Dinamis
- Situs web statis lebih sederhana dan cepat karena kontennya tetap dan tidak berubah, kecuali halaman itu sendiri diubah. Ia cocok untuk diterapkan pada situs web sederhana dengan konten yang tidak perlu sering diperbarui.
- Sebaliknya, situs web dinamis memungkinkan lebih banyak fleksibilitas dan interaktivitas. Ia dapat mengambil konten dari database, merespons masukan pengguna, dan menghasilkan halaman yang disesuaikan dengan cepat. Hal ini menjadikannya ideal untuk situs web dengan konten yang berubah atau interaktif, seperti situs e-commerce, media sosial, dan aplikasi web interaktif lainnya.

### Kelebihan Situs Web Statis
Situs web statis memiliki beberapa kelebihan yang menjadikannya pilihan yang efektif untuk beberapa jenis situs web, di antaranya:
1.  **Keamanan yang Terjamin**: Website statis memiliki keamanan yang lebih baik karena hanya menampilkan konten yang sudah ada dalam file HTML, tidak ada risiko kerentanan yang terkait dengan database atau server backend.
2.  **Kecepatan Akses yang Lebih Baik**:  Website statis memiliki file HTML yang ringan dan siap digunakan. Pengunjung dapat mengakses konten dengan cepat tanpa menunggu proses kode dijalankan di peladen (*server*).


## Membuat GitHub Pages dengan Jekyll

Merujuk kepada situs resmi Jekyll [jekyllrb.com](https://jekyllrb.com/docs/), berikut adalah prasyarat untuk menggunakan Jekyll:
-   Ruby versi  2.5.0 atau lebih
-   RubyGems
-   GCC dan Make

Dalam tutorial ini, saya menggunakan **Windows 11** versi 23H2. Untuk mempermudah proses instalasi Jekyll di Windows, kita akan menggunakan RubyInstaller for Windows. Program ini mempermudah kita untuk menginstal bahasa pemrograman Ruby, lingkungan eksekusi, dokumentasi penting, dan banyak lagi.

### Instalasi Jekyll
1. Unduh dan *install* versi Ruby+Devkit dari halaman [download RubyInstaller](https://rubyinstaller.org/downloads/). Gunakan opsi bawaan untuk instalasi.
2. Dari opsi yang diberikan, pilih ***MSYS2 and MINGW development tool chain*** dengan cara mengetik angka 3, lalu tekan <kbd>enter</kbd>.<br>![](/assets/img/posts/2024-04-09/instalasi-RubyInstaller-1.png)<br>![](/assets/img/posts/2024-04-09/instalasi-RubyInstaller-2.png)
3. Setelah proses instalasi selesai, klik tombol start pada Windows, lalu jalankan **Start Command Prompt with Ruby**. Ketik dan jalankan perintah `ridk install` pada jendela Command Prompt yang muncul, hal ini diperlukan untuk instalasi gems berikut dengan ekstensi bawaannya. Kamu bisa menemukan informasi lebih lanjut terkait hal ini di [dokumentasi RubyInstaller](https://github.com/oneclick/rubyinstaller2#using-the-installer-on-a-target-system). 
4. Setelah proses instalasi selesai, tekan <kbd>enter</kbd>, lalu jalankan perintah `ridk enable`.
5. Selanjutnya kita akan menginstal Jekyll dan Bundler dengan perintah `gem install jekyll bundler`
6. Langkah terakhir pada tahap ini adalah memastikan Jekyll sudah terinstal dengan benar menggunakan perintah `jekyll -v`. Jika muncul versi Jekyll, artinya proses instalasi Jekyll sudah selesai. Di tahap selanjutnya kita akan membuat GitHub Pages.

### Membuat GitHub Pages
1. Masuk ke [GitHub](https://github.com) lalu buka repositori [Chirpy Starter](https://github.com/cotes2020/chirpy-starter), klik tombol **<kbd>Use this template</kbd>** > **<kbd>Create a new repository</kbd>**, lalu beri nama repositori tersebut `USERNAME.github.io`, dimana `USERNAME` diganti dengan *username* GitHub kamu.
2. *Clone* repositori tersebut ke komputermu. Caranya buka **File Explorer**, lalu arahkan ke direktori web yang akan dibuat, kemudian jalankan perintah berikut:
```console
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
```
3. Selanjutnya kita perlu mempersiapkan berkas JavaScript, untuk itu kita harus menginstal [NodeJS](https://nodejs.org/).
4. Buka **Command Prompt** di direktori web kita lalu jalankan perintah `bundle`.
5. Sebelum memasukkan web yang telah kita buat ke GitHub Pages, kita bisa melihat pratinjau di _server_ lokal dengan menjalankan perintah ```bundle exec jekyll s```. Jika semuanya berjalan lancar, web yang telah kita buat bisa diakses melalui URL `localhost:4000`.

### *Deploy* menggunakan GitHub Actions
1. Bagi yang menggunakan sistem operasi Windows (abaikan langkah ini jika kamu menggunakan Linux), buka _root_ situs di Command Prompt dan jalankan perintah[^fn-nth-5]:
```console
bundle lock --add-platform x86_64-linux
```
2. Selanjutnya buka repositori GitHub kamu, pilih tab **Settings**. Kemudian klik **Pages** di menu navigasi sebelah kiri. Pada bagian **Source**, pilih [**GitHub Actions**](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow) dari opsi *dropdown*.<br>![](/assets/img/posts/2024-04-09/github-actions.png)
3. Sebelum melakukan _deployment_, periksa berkas `_config.yml`{: .filepath} dan pastikan `url` sudah dikonfigurasi dengan benar. Kamu juga bisa mengubah `avatar` (foto profile), `timezone` (zona waktu), `lang`(bahasa), ataupun pengaturan lainnnya di file tersebut.
4. _Push commits_ apapun ke GitHub untuk memicu terjadinya _Actions_. Setelah itu kita bisa melihat alur _Build and Deploy_ yang sedang berjalan pada tab _Actions_ di repositori (jika terjadi masalah, kamu bisa memeriksa penyebabnya di sini). Setelah proses _build_ selesai, situs akan di-_deploy_ secara otomatis.

## Referensi
[^fn-nth-1]: [Blogging Like a Hacker](https://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)
[^fn-nth-2]: [Static Website Generators Reviewed: Jekyll, Middleman, Roots, Hugo](https://www.smashingmagazine.com/2015/11/static-website-generators-jekyll-middleman-roots-hugo-review/)
[^fn-nth-3]: [State of the Web Static Site Generators](https://dev.to/asyncbanana/state-of-the-web-static-site-generators-g6f)
[^fn-nth-4]: [Mengenal Apa itu Static Site Generator](https://www.codepolitan.com/blog/mengenal-apa-itu-ssg-static-site-generator/)
[^fn-nth-5]: [Getting Started on Chirpy](https://chirpy.cotes.page/posts/getting-started/#deploy-by-using-github-actions)
