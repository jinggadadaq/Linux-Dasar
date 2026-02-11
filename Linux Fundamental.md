# **Pengaturan Dasar**

## **1. Mengatur hostname (nama host server)**

```bash
hostnamectl set-hostname <hostname>
```
Untuk mengganti nama host (hostname) sistem/server Anda.

## **2. Mengatur zona waktu (timezone)**

```bash
timedatectl set-timezone Asia/Jakarta
```
Untuk mengatur waktu sistem ke zona waktu Jakarta (WIB).

## **3. Pengaturan jaringan (IP statis)**

```bash
vim /etc/netplan/00-installer-config.yaml
```

**Contoh konfigurasi:**

```yaml
network:
  ethernets:
    enp0s3:
      dhcp4: false
      addresses: ['172.23.x.x/20']
      routes:
        - to: default
          via: 172.23.0.1
      nameservers:
        addresses: ['8.8.8.8']
  version: 2
```
``` netplan apply ```
netplan apply digunakan untuk menerapkan aturan jaringan di ubuntu.
Mengatur IP statis, gateway, dan DNS pada Ubuntu Server menggunakan Netplan jangan lupa juga untuk interface yang di gunakan wajid disamakan dengan yang sudah ada sebelumnya.

# **Perintah Dasar Linux**

## **1. Menampilkan user yang sedang digunakan**

```bash
whoami
```

Menampilkan nama user saat ini.

## **2. Menampilkan siapa saja user yang login**

```bash
who
```

Menampilkan daftar semua user yang sedang login ke sistem.

## **3. Menampilkan hostname server**

```bash
hostnamectl
hostname
```

Menampilkan detail nama host dan informasi sistem lainnya.

## **4. Menampilkan tanggal dan waktu**

```bash
date
timedatectl
```

Menampilkan dan mengatur waktu sistem.

# **Asesment Server**

## **1. Menampilkan sistem operasi yang digunakan**

```bash
cat /etc/os-release
```

Menampilkan informasi OS Linux.

## **2. Menampilkan nama kernel**

```bash
uname
```

Menampilkan nama sistem kernel.

## **3. Menampilkan info prosesor**

```bash
lscpu
```

Menampilkan informasi CPU/arsitektur.

## **4. Menampilkan penggunaan RAM**

```bash
free -h
```

Menampilkan penggunaan memori secara ringkas (dalam format human-readable).

## **5. Menampilkan partisi/penyimpanan**

```bash
lsblk
df -h
```

Menampilkan daftar partisi disk dan penggunaan disk.

# **Manajemen File & Direktori**

## **Manajemen Direktori**

### **1. Membuat direktori**

```bash
mkdir Folder1
```

Membuat folder baru bernama `Folder1`.

### **2. Masuk dan keluar direktori**

```bash
cd Folder1
```

Masuk ke direktori `Folder1`.

### **3. Menampilkan isi direktori**

```bash
ls
```

Melihat isi folder.

### **4. Menampilkan path lokasi saat ini**

```bash
pwd
```

Menampilkan direktori aktif saat ini.

### **5. Menghapus direktori kosong**

```bash
rmdir Folder1
```

Menghapus folder `Folder1` jika kosong.

# **Manajemen File**

### **1. Membuat file kosong**

```bash
touch file1.txt
```

Membuat file kosong bernama `file1.txt`.

### **2. Membuat file berisi teks**

```bash
echo "Hello World" >> file2.pdf
```

Menambahkan "Hello World" ke file `file2.pdf`.

### **3. Menampilkan isi file**

```bash
cat file2.txt
```

Menampilkan isi seluruh file.

### **4. Menampilkan 10 baris pertama/terakhir file**

```bash
head /folder/file_tujuan
tail /folder/file_tujuan
```

Menampilkan 10 baris awal dan akhir file.

### **5. Menghapus file**

```bash
rm file1.txt
```

Menghapus file bernama `file1.txt`.

### **6. Menyalin file atau folder**

```bash
cp file1.txt /mnt
```

Menyalin file ke direktori lain.

### **7. Memindahkan atau mengubah nama file/folder**

```bash
mv file1.txt /mnt/file1.jpg
```

Memindahkan/rename file.

# **Manajemen User & Grup**

## **User**

### **1. Membuat user baru**

```bash
adduser nama_peserta
```

Membuat user sistem baru.

### **2. Melihat daftar user**

```bash
cat /etc/passwd
```

Menampilkan seluruh user.

### **3. Mengubah password user**

```bash
passwd nama_user
```

Mengatur atau mengubah password user.

### **4. Mengubah ID user atau menambahkan ke grup**

```bash
usermod -u 10000 jingga
usermod -aG nama_group nama_user
```

Mengubah UID user dan menambahkan user ke grup.

## **Grup**

### **1. Membuat grup baru**

```bash
groupadd developer
```

Membuat grup `developer`.

### **2. Melihat daftar grup**

```bash
cat /etc/group
```

Melihat seluruh grup.

### **3. Mengganti nama grup**

```bash
groupmod -n nama_baru nama_lama
```

Mengubah nama grup.

### **4. Menghapus grup**

```bash
groupdel nama_grup
```

Menghapus grup tertentu.

# **Hak Akses & Kepemilikan**

## **1. Mengatur hak akses file**

```bash
chmod 640 file_name
```

Memberi izin baca & tulis ke owner, baca ke grup, tidak ada akses untuk lainnya.

## **2. Mengubah kepemilikan file**

```bash
chown nama_user file_name
```

Mengganti pemilik file.

## **3. Mengubah grup dari file**

```bash
chgrp nama_grup file_name
```

Mengganti grup pemilik file.

# **Apa Itu WebServer**

**Web Server** adalah software yang digunakan untuk menyimpan, memproses, dan mengirimkan halaman web ke client melalui jaringan. **Web Server** menggunakan protokol **HTTP (80)** atau **HTTPS (443)**.

# **Installation**

Jadi disini kita akan melakukan instalasi webserver dengan menggunakan apache, apa itu apache merupakan sebuah perangkat lunak server web gratis dan open-source yang populer, dikelola oleh Apache Software Foundation.

**Langkah-langkah instalasi:**

```bash
apt update -y && apt upgrade -y
apt install apache2 -y
systemctl status apache2
```

Jika statusnya sudah active kita bisa coba akses IP server kita masuk ke browser bisa menggunakan chrome, firefox, microsoft edge dll:

```text
http://IP-SERVER
```

# Konfigurasi Virtual Host Apache (games)

## 1. Persiapan Source Code

Siapkan terlebih dahulu source code project. Teman-teman bisa mencari di GitHub atau platform lain.

```bash
git clone https://github.com/TomMalbran/games.git
```

## 2. Pindahkan Folder ke `/var/www`

Setelah repository berhasil di-clone, pindahkan folder `games` ke direktori web root Apache:

```bash
mv games/ /var/www/
ls /var/www/
```

Output:

```text
games  html
```

## 3. Copy Konfigurasi Virtual Host Default

Masuk ke direktori konfigurasi virtual host Apache:

```bash
cd /etc/apache2/sites-available/
cp 000-default.conf games.conf
```

## 4. Edit File `games.conf`

Edit file `games.conf` menggunakan editor favorit (vim/nano/vi/pico):

```bash
vim games.conf
```

Isi konfigurasi:

```apache
<VirtualHost *:80>

    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/games

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
```

Simpan file (**SAVE**).

## 5. Disable Default Site & Enable VHost Baru

```bash
a2dissite 000-default.conf
a2ensite games.conf
systemctl reload apache2
```

## 6. Akses Website

Buka browser (Google/Chrome/Firefox) dan akses server:

```text
http://IP-SERVER
```

Website akan berubah dan menampilkan project **games**.

## Catatan

Pastikan permission folder benar:

```bash
chown -R www-data:www-data /var/www/games
chmod -R 755 /var/www/games
```

Jika tidak tampil, cek log:

```bash
tail -f /var/log/apache2/error.log
```

Siap untuk upload ke GitHub sebagai dokumentasi konfigurasi Virtual


# **Install Paket WordPress**

```bash
apt install mysql-server php php-mysql libapache2-mod-php php-cli php-curl php-gd php-mbstring php-xml php-xmlrpc php-zip unzip wget -y
```

# **Konfigurasi MySQL**

```bash
mysql_secure_installation
mysql
```

```sql
CREATE DATABASE wordpress_db;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'P@ssw0rd2025';
SELECT User, Host FROM mysql.user;
GRANT ALL PRIVILEGES ON *.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

# **Download & Install WordPress**

```bash
cd /var/www/html
rm index.html
wget https://wordpress.org/latest.tar.gz
tar -xvzf latest.tar.gz
mv wordpress/* .
rm -rf wordpress latest.tar.gz
```

# **Set Permission**

```bash
chown -R www-data:www-data /var/www/html/
chmod -R 755 /var/www/html/
```

# **Konfigurasi Apache untuk WordPress**

```bash
vim /etc/apache2/sites-available/wordpress.conf
```

```apache
<VirtualHost *:80>
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html
    ServerName localhost

    <Directory /var/www/html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

```bash
a2ensite wordpress.conf
a2enmod rewrite
systemctl restart apache2
```

# **Konfigurasi WordPress**

```bash
cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php
vim /var/www/html/wp-config.php
```

```php
define( 'DB_NAME', 'wordpress_db' );
define( 'DB_USER', 'wpuser' );
define( 'DB_PASSWORD', 'P@ssw0rd2025' );
define( 'DB_HOST', 'localhost' );
```

# **Akses WordPress**

```text
http://IP-SERVER/
```

Lanjutkan wizard instalasi WordPress sampai selesai.
