---
title: Dasar-dasar Jaringan Komputer
date: 2025-02-09 10:30:00 +0700
categories: [Materi Kuliah, Jaringan Komputer]
tags: [kuliah, jaringan komputer] # TAG names should always be lowercase
---

## **1. Pengenalan Jaringan Komputer**

### **Definisi Jaringan Komputer**
Jaringan komputer adalah sistem yang terdiri dari dua atau lebih perangkat komputasi (seperti komputer, server, printer, atau perangkat IoT) yang terhubung melalui media komunikasi (kabel atau nirkabel) untuk berbagi sumber daya, bertukar data, dan berkomunikasi.

### **Tujuan Jaringan Komputer**
1. **Resource Sharing**:  
   - Memungkinkan berbagi sumber daya seperti printer, file, dan aplikasi.  
   - Contoh: Beberapa komputer dalam kantor dapat menggunakan satu printer yang sama.
2. **Komunikasi Data**:  
   - Memungkinkan pertukaran informasi secara cepat dan efisien.  
   - Contoh: Email, pesan instan, dan video conferencing.
3. **Keandalan dan Redundansi**:  
   - Data dapat disimpan di beberapa lokasi untuk mencegah kehilangan data jika satu perangkat rusak.  
   - Contoh: Backup server.
4. **Skalabilitas**:  
   - Jaringan dapat dikembangkan dengan mudah dengan menambahkan perangkat baru.  
5. **Keamanan**:  
   - Jaringan memungkinkan implementasi kebijakan keamanan untuk melindungi data.

---

## **2. Jenis-jenis Jaringan**

### **Berdasarkan Skala**
1. **LAN (Local Area Network)**:  
   - Jaringan kecil yang mencakup area terbatas, seperti rumah, kantor, atau sekolah.  
   - Kecepatan tinggi (biasanya 1 Gbps atau lebih).  
   - Menggunakan teknologi seperti Ethernet atau Wi-Fi.

2. **MAN (Metropolitan Area Network)**:  
   - Jaringan yang mencakup area kota atau kampus.  
   - Contoh: Jaringan yang menghubungkan beberapa kantor cabang dalam satu kota.  
   - Menggunakan teknologi seperti fiber optic atau microwave.

3. **WAN (Wide Area Network)**:  
   - Jaringan yang mencakup area geografis luas, seperti negara atau benua.  
   - Contoh: Internet.  
   - Menggunakan teknologi seperti leased lines, MPLS, atau satelit.

4. **PAN (Personal Area Network)**:  
   - Jaringan pribadi dalam jarak dekat (beberapa meter).  
   - Contoh: Bluetooth antara smartphone dan headset.

### **Berdasarkan Fungsi**
1. **Client-Server**:  
   - Satu komputer (server) menyediakan layanan, dan komputer lain (client) mengakses layanan tersebut.  
   - Contoh: Web server menyediakan halaman website, dan browser (client) mengaksesnya.

2. **Peer-to-Peer (P2P)**:  
   - Semua perangkat memiliki peran yang sama, bisa berfungsi sebagai client dan server.  
   - Contoh: File sharing melalui aplikasi seperti BitTorrent.

---

## **3. Topologi Jaringan**

### **Definisi Topologi Jaringan**
Topologi jaringan adalah struktur atau tata letak perangkat dalam jaringan, baik secara fisik (bagaimana perangkat terhubung) maupun logis (bagaimana data mengalir).

### **Jenis-jenis Topologi**
1. **Topologi Bus**:  
   - Semua perangkat terhubung ke satu kabel utama (bus).  
   - Data dikirim ke semua perangkat, tetapi hanya perangkat tujuan yang memprosesnya.  
   - **Kelebihan**: Mudah diimplementasikan, biaya rendah.  
   - **Kekurangan**: Jika kabel utama rusak, seluruh jaringan terganggu.

2. **Topologi Star**:  
   - Semua perangkat terhubung ke satu hub/switch pusat.  
   - **Kelebihan**: Mudah dikelola, jika satu kabel rusak, jaringan lain tetap berfungsi.  
   - **Kekurangan**: Bergantung pada hub/switch pusat.

3. **Topologi Ring**:  
   - Perangkat terhubung dalam lingkaran, data mengalir satu arah.  
   - **Kelebihan**: Performa stabil untuk jaringan kecil.  
   - **Kekurangan**: Jika satu perangkat rusak, seluruh jaringan terganggu.

4. **Topologi Mesh**:  
   - Setiap perangkat terhubung langsung ke perangkat lain.  
   - **Kelebihan**: Redundansi tinggi, keandalan jaringan baik.  
   - **Kekurangan**: Biaya tinggi dan kompleksitas pengelolaan.

5. **Topologi Hybrid**:  
   - Kombinasi dari beberapa topologi.  
   - **Kelebihan**: Fleksibel dan dapat disesuaikan dengan kebutuhan.  
   - **Kekurangan**: Biaya dan kompleksitas tinggi.

---

## **4. Model Referensi OSI dan TCP/IP**

### **Model OSI (Open Systems Interconnection)**
Model OSI adalah kerangka kerja konseptual yang terdiri dari 7 lapisan untuk memahami dan mengimplementasikan protokol jaringan. Setiap lapisan memiliki fungsi spesifik:

1. **Physical Layer**:  
   - Bertanggung jawab atas transmisi data mentah melalui media fisik (kabel, sinyal nirkabel).  
   - Contoh: Ethernet, Wi-Fi.

2. **Data Link Layer**:  
   - Menyediakan pengiriman data yang andal melalui link fisik.  
   - Contoh: MAC address, switch.

3. **Network Layer**:  
   - Mengelola pengalamatan dan routing paket data.  
   - Contoh: IP address, router.

4. **Transport Layer**:  
   - Menyediakan pengiriman data end-to-end yang andal.  
   - Contoh: TCP (reliable), UDP (unreliable).

5. **Session Layer**:  
   - Mengelola sesi komunikasi antar aplikasi.  
   - Contoh: Session establishment, maintenance, dan termination.

6. **Presentation Layer**:  
   - Bertanggung jawab atas translasi, enkripsi, dan kompresi data.  
   - Contoh: SSL/TLS untuk enkripsi.

7. **Application Layer**:  
   - Menyediakan antarmuka antara aplikasi dan jaringan.  
   - Contoh: HTTP, FTP, SMTP.

### **Model TCP/IP**
Model TCP/IP adalah model yang lebih sederhana dan praktis, terdiri dari 4 lapisan:

1. **Network Access Layer**:  
   - Gabungan Physical dan Data Link Layer OSI.  
   - Contoh: Ethernet, Wi-Fi.

2. **Internet Layer**:  
   - Setara dengan Network Layer OSI.  
   - Contoh: IP, ICMP.

3. **Transport Layer**:  
   - Sama dengan Transport Layer OSI.  
   - Contoh: TCP, UDP.

4. **Application Layer**:  
   - Gabungan Session, Presentation, dan Application Layer OSI.  
   - Contoh: HTTP, FTP, DNS.

---

## **5. Komponen Dasar Jaringan Komputer**

### **Perangkat Keras**
1. **Router**:  
   - Menghubungkan jaringan yang berbeda dan mengarahkan paket data.  
2. **Switch**:  
   - Menghubungkan perangkat dalam jaringan LAN dan mengirim data ke tujuan yang spesifik.  
3. **Hub**:  
   - Menghubungkan perangkat dalam jaringan LAN, tetapi mengirim data ke semua perangkat (broadcast).  
4. **Access Point**:  
   - Memungkinkan perangkat nirkabel terhubung ke jaringan kabel.  
5. **Kabel Jaringan**:  
   - Twisted pair (UTP, STP), coaxial, fiber optic.

### **Perangkat Lunak**
1. **Sistem Operasi Jaringan**:  
   - Contoh: Windows Server, Linux.  
2. **Protokol Jaringan**:  
   - Contoh: TCP/IP, HTTP, FTP.  
3. **Aplikasi Jaringan**:  
   - Contoh: Web browser, email client.

### **Media Transmisi**
1. **Kabel (Wired)**:  
   - Contoh: Twisted pair, fiber optic.  
2. **Nirkabel (Wireless)**:  
   - Contoh: Wi-Fi, Bluetooth.

---

## **Sumber Referensi**
1. Andrew S. Tanenbaum, "Computer Networks", Pearson Education.  
2. Behrouz A. Forouzan, "Data Communications and Networking", McGraw-Hill.  
3. Cisco Networking Academy, "CCNA Routing and Switching".  
4. William Stallings, "Data and Computer Communications", Pearson Education.  
5. [OSI Model Explained](https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/).  
6. [TCP/IP Model](https://www.geeksforgeeks.org/tcp-ip-model/).  