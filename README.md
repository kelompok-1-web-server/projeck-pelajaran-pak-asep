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
| **Sistem Operasi Tamu (Guest OS)** | Debian Trixie (12.x) |
| **Alamat IP Server** | `103.139.192.42` |
| **RAM VM** | 2 GB |
| **vCPU** | 2 Core |
| **Web Server yang Dipilih** | **Apache2** |
| **Versi PHP yang Dipakai** | **mod_php** |

---

#### 2.1. Persiapan Dasar (Debian Trixie di VMware)

Langkah 1: Setup Awal Sistem

```bash
# Masuk sebagai super user
sudo su -

# Perbarui paket sistem
apt update && apt upgrade -y

# Install paket-paket penting
apt install -y wget curl nano net-tools openssh-server ufw
```
Langkah 2: Setting Jaringan Static IP

```bash
# Edit konfigurasi jaringan
nano /etc/network/interfaces

# Tambahkan setting IP statis
auto eth0
iface eth0 inet static
    address 103.139.192.42
    netmask 255.255.255.0
    gateway 103.139.192.1
    dns-nameservers 8.8.8.8 8.8.4.4

# Restart layanan jaringan
systemctl restart networking

# Cek IP address
ip addr show eth0
```
Langkah 3: Konfigurasi Keamanan

```bash
# Aktifkan SSH
systemctl start ssh
systemctl enable ssh

# Setting firewall
ufw allow 22/tcp    # Port SSH
ufw allow 80/tcp    # Port HTTP
ufw allow 443/tcp   # Port HTTPS
ufw allow 7080/tcp  # Port Web Admin
ufw enable
```
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
    # Uji dari browser: http://103.139.192.42
    ```
#### 2.3. Konfigurasi PHP 🐘

Kami menggunakan **JENIS PHP: mod_php** untuk mengintegrasikan PHP dengan apache2.

* **Instalasi PHP:**
    ```bash
    sudo apt install php
    ```
* **Uji PHP Sudah Muncul Atau belum**
    ```bash
    Buat file uji : nano /var/www/html/info.php
    ```
    ```bash
    Tambahkan script berikut : <?php phpinfo(); ?>
    ```
    ```bash
    Akses dari browser : http://103.139.192.42/info.php
    ```

#### 2.4. Implementasi SSL (HTTPS) 🔒
Untuk mengaktifkan akses HTTPS, kami membuat *self-signed certificate*.

**Instal OpenSSL**

    apt install openssl

    a2enmod ssl

    mkdir /etc/apache2/ssl

    openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/selfsigned.key -out /etc/apache2/ssl/selfsigned.crt
    
    **ISI SEPERTI INI**
    
    Country Name (2 letter code) [AU]: ID
    State or Province Name (full name) [Some-State]: Jawa Barat
    Organization Name (eg, company) [Internet Widgits Pty Ltd]: SMKN 1 Soreang
    Common Name (e.g. server FQDN or YOUR name) []: server.local
    
 * **Konfigurasi Virtual Host HTTPS**
    masukan
    ```bash
    cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default-ssl.conf
    ```
    Edit supaya bisa memasukan konfigurasi file SSL
    ```bash
    nano /etc/apache2/sites-available/000-default-ssl.conf
    ```
    Isi dengan konfigurasi berikut
   ```bash
   <VirtualHost *:443>
    ServerAdmin admin@localhost
    DocumentRoot /var/www/html
    ServerName server.local

    SSLEngine on
    SSLCertificateFile /etc/apache2/ssl/selfsigned.crt
    SSLCertificateKeyFile /etc/apache2/ssl/selfsigned.key

    <Directory /var/www/html>
        AllowOverride All
        Options Indexes FollowSymLinks
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```
 * **Aktifkan HTTPS dan Modul Rewrite**
   
   Aktifkan situs SSL dan modul rewrite
   ```bash
   a2ensite 000-default-ssl.conf
   a2enmod rewrite
   ystemctl reload apache2
   ```
   Uji dari browser: https://103.139.192.42
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
kesan utama yang saya rasakan adalah bahwa Apache2 merupakan web server yang sangat stabil, fleksibel, dan mudah dikonfigurasi.
#### 4.2. Kendala dan Solusi yang Diterapkan 💡
Tidak ada kendala saat mengerjakan proyek webserver ini. tapi kendala nya ada pada anggota kelompok yang cuek. Solusinya memngingatkan setiap anggota kelompok untuk mengerjakan tugas tersebut, dan akhirnya tugas webserver ini selesai. 

---

### 5. 📂 Dokumentasi Konten Website

Seluruh *source code* (Halaman Utama dan Halaman Profil) yang berada di *document root* server telah disalin dan di-*commit* ke dalam folder `/html` di *repository* GitHub ini.

---

### 6. 🎬 Dokumentasi Video Pengerjaan

Seluruh proses pengerjaan telah direkam dan diunggah ke YouTube.

**Link Video YouTube:**

[![Thumbnail Video Pengerjaan](https://img.youtube.com/vi/1-qlNtQS1OA/0.jpg)](https://youtu.be/tmgkfZbXk7w?si=Tq5oQmpxXwi-I4pF)

**PETUNJUK:** Ganti semua teks di dalam tanda kurung siku `[ ... ]` dengan informasi proyek yang relevan.
