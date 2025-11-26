# 💻 LAPORAN PROYEK: PENGEMBANGAN WEB SERVER DAN APLIKASI SEDERHANA

**Proyek:** MEMBUAT WEBSITE ANGGOTA KELOMPOK MENGUNAKAN WEB SERVER APACHE 

Proyek ini dibuat untuk memenuhi tugas mata pelajaran **Administrasi Sistem Jaringan (ASJ)**, yang merupakan salah satu elemen Capaian Pembelajaran Konsentrasi Keahlian Teknik Komputer dan Jaringan (**CP KKTKJ**) pada program TJKT. Proyek ini berfokus pada implementasi layanan Web Server, konfigurasi PHP, dan pengamanan koneksi menggunakan SSL/HTTPS.

---

### 1. 👥 Informasi Kelompok dan Spesifikasi Lingkungan Praktik

#### 1.1. Informasi Kelompok

| Peran | Nama Lengkap | Kelas |
| :--- | :--- | :--- |
| **Ketua Kelompok** | ADITYA KUSTIAWAN  | XI TJKT 2 |
| Anggota 1 | RANDHIKA  | XI TJKT 2 |
| Anggota 2 | MARYAM RIBI PERTIWI | XI TJKT 2 |
| Anggota 2 | SARAH SAFITRI | XI TJKT 2 |
| **Nama Sekolah/Institusi** | SMKN 1 SOREANG | |

#### 1.2. Spesifikasi Alat dan Bahan (Host) 🛠️

| Komponen | Deskripsi / Versi |
| :--- | :--- |
| **Virtualisasi** | VMware Workstation Pro |
| **Sistem Operasi Host** | Windows 11 |
| **RAM Host (Minimal)** | 8 GB |
| **CPU Host** | Amd Ryzen 5 7430 |

#### 1.3. Spesifikasi Server Virtual (VM) 🖥️

| Spesifikasi | Detail |
| :--- | :--- |
| **Sistem Operasi Tamu (Guest OS)** | Debian Trixie (13.x) |
| **Alamat IP Server** | `10.10.1.4` |
| **RAM VM** | 2 GB |
| **vCPU** | 2 Core |
| **Web Server yang Dipilih** | **Apache2** |
| **Versi PHP yang Dipakai** | **[mod_php / php-fpm / lsphp]** |

---

### 2. 📝 Dokumentasi Teknis dan Langkah-Langkah Pengerjaan

#### 2.1. Persiapan Dasar (Debian Trixie di VMware)

1.  Melakukan *update* dan *upgrade* sistem.
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```
2.  Memastikan konfigurasi jaringan (Bridge/NAT/Host-Only) sudah benar.

#### 2.2. Instalasi dan Konfigurasi Web Server 🌐

Kami menggunakan **apache2**. Berikut langkah-langkah utamanya:

* **Instalasi:**
    ```bash
    # sudo apt install apache2
    ```
    ```bash
    # systemctl enable apache2
    ```
     ```bash
    # systemctl start apache2
    ```
     ```bash
    # systemctl status apache2
    ```
     ```bash
    # Uji dari browser: http://10.10.1.4
    ```
* **Konfigurasi Virtual Host/Server Block:**


#### 2.3. Konfigurasi PHP 🐘

Kami menggunakan **JENIS PHP: php** untuk mengintegrasikan PHP dengan *Web Server*.

* **Instalasi PHP:**
    ```bash
    sudo apt install php
    ```
    ```bash
    Buat file uji : nano /var/www/html/info.php
    ```
    ```bash
    Tambahkan script berikut : <?php phpinfo(); ?>
    ```
    ```bash
    Akses dari browser : http://10.10.1.4/info.php
    ```
* **Integrasi:**
    [Jelaskan langkah-langkah integrasi antara PHP dengan Web Server yang Kalian pilih.]

#### 2.4. Implementasi SSL (HTTPS) 🔒

Untuk mengaktifkan akses HTTPS, kami membuat *self-signed certificate*.

1.  Membuat direktori untuk *certificate*.
2.  Membuat *Key* dan *Certificate* menggunakan OpenSSL.
3.  Memodifikasi konfigurasi *Web Server* untuk menggunakan port **443** dan menunjuk ke *certificate* yang telah dibuat, serta memastikan akses dapat dilakukan melalui `https://10.10.1.4`.

---

### 3. 📊 Analisis Web Server

Berdasarkan pengalaman kami dalam proyek ini, berikut adalah analisis kelebihan dan kekurangan dari *Web Server* yang kami gunakan:

| Aspek | Kelebihan ([APACHE2) 👍 | Kekurangan (APACHE2) 👎 |
| :--- | :--- | :--- |
| **Performa & Kecepatan** | Stabil dan andal | Konsumsi resource lebih besar |
| **Kemudahan Konfigurasi**| Modular dan fleksibel | Konfigurasi cukup banyak dan kompleks |
| **Fitur & Modularitas** | Dapat mengaktifkan/menonaktifkan modul dengan mudah | Modularitas berlebih bisa menurunkan performa |

---

### 4. 🧠 Refleksi Proyek: Kesan dan Kendala

#### 4.1. Kesan Selama Proses Pengerjaan ✨

"Kami merasa mendapatkan banyak ilmu baru, terutama dalam praktik membangun web server apache2 ini. dan kami juga merasa bangga karena kami sudah bisa membangun web server sendiri.

#### 4.2. Kendala dan Solusi yang Diterapkan 💡

| Kendala yang Kalian Hadapi 🚧 | Solusi yang Ditemukan ✅ |
| :--- | :--- |
| kami mengalami kesulitan dalam membuat website ini karena kelompok kami agak tidak kompak, yang membuat proses pengerjaan web server ini memakan banyak waktu. solusi untuk masalah ini adalah, dengan cara mendiskusikan kembali kerja kelompok ini dan mengerjakan nya secara bersama sama :) |

---

### 5. 📂 Dokumentasi Konten Website

Seluruh *source code* (Halaman Utama dan Halaman Profil) yang berada di *document root* server telah disalin dan di-*commit* ke dalam folder `/html` di *repository* GitHub ini.

---

### 6. 🎬 Dokumentasi Video Pengerjaan

Seluruh proses pengerjaan telah direkam dan diunggah ke YouTube.

**Link Video YouTube:**

[![Thumbnail Video Pengerjaan](https://img.youtube.com/vi/1-qlNtQS1OA/0.jpg)](https://www.youtube.com/watch?v=1-qlNtQS1OA)

**PETUNJUK:** Ganti semua teks di dalam tanda kurung siku `[ ... ]` dengan informasi proyek yang relevan.
