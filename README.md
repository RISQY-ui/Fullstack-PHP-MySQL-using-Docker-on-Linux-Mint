---

Lab Fullstack PHP + MySQL dengan Docker di Linux Mint

📁 Langkah 1: Buat Folder Projek

Buka terminal, lalu jalankan:

```bash
mkdir ~/Desktop/Lab_PHP_Faris
cd ~/Desktop/Lab_PHP_Faris
code .
```

VS Code akan terbuka di folder kosong tersebut.

---

🐳 Langkah 2: Buat File docker-compose.yml

Di dalam VS Code, buat file bernama docker-compose.yml, lalu isi dengan kode berikut:

```yaml
version: '3.8'

services:
  # Web server PHP + Apache
  web:
    image: php:8.2-apache
    container_name: php_faris
    ports:
      - "8080:80"
    volumes:
      - ./src:/var/www/html
    networks:
      - lab_network
    depends_on:
      - db

  # Database MySQL
  db:
    image: mysql:5.7
    container_name: mysql_database_faris
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password_faris_123
      MYSQL_DATABASE: komi_db
    ports:
      - "3306:3306"
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - lab_network

volumes:
  db_data:

networks:
  lab_network:
    driver: bridge
```

---

📄 Langkah 3: Buat Folder src dan File index.php

Buat folder src di samping file docker-compose.yml.

Di dalam folder src, buat file index.php dengan isi:

```php
<?php
echo "<h1>Halo Fullstack Docker Faris</h1>";
echo "<p>PHP server berhasil berjalan di Linux Mint</p>";
?>
```

---

🚀 Langkah 4: Jalankan Container Docker

Jalankan perintah berikut di terminal (dalam folder projek):

```bash
sudo docker compose up -d
```

Jika Docker belum terinstal, ikuti langkah instalasi di bawah.

---

🛠️ Langkah 5: Instal Docker (Jika Belum Ada)

```bash
sudo apt update
sudo apt install docker.io -y
sudo apt install docker-compose-v2 -y
```

Agar tidak perlu sudo setiap kali:

```bash
sudo usermod -aG docker $USER
```

Setelah perintah ini, restart VS Code atau logout/login agar perubahan berlaku.

---

🌐 Langkah 6: Akses Website

Buka browser dan akses:

```
http://localhost:8080
```

Jika muncul tulisan dari index.php, maka server sudah berjalan dengan baik.

---

⚠️ Catatan Jika Terjadi Error

Jika muncul error TLS handshake timeout atau koneksi gagal:

1. Ganti jaringan (misal pakai hotspot HP)
2. Hapus container lama:
   ```bash
   sudo docker compose down
   ```
3. Jalankan ulang:
   ```bash
   sudo docker compose up -d
   ```

Docker akan melanjutkan download dari titik terhenti, tidak mengulang dari awal.

---

✅ Kesimpulan

· Folder src adalah tempat semua file .php, .html, .css, .js
· Setiap perubahan file akan langsung terlihat di browser tanpa restart container
· Cocok untuk belajar PHP, MySQL, dan keamanan web (SQL injection)

---

Dibuat oleh: Faris
Tujuan: Portofolio belajar Fullstack dengan Docker di Linux Mint

---
