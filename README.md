# Instalasi Nginx

## 🚀 Instalasi dan Konfigurasi Nginx
Pertama, pastikan Anda telah menginstal Termux di perangkat Anda. Setelah itu, buka aplikasi Termux dan ikuti langkah-langkah di bawah ini.

  - Instalasi Nginx
    Untuk menginstal Nginx, ketik perintah berikut:
    ~~~
    pkg install nginx
    ~~~
    
    Perintah ini akan mengunduh dan menginstal paket Nginx beserta semua dependensi yang diperlukan.

  - Edit Konfigurasi Nginx
    Setelah instalasi selesai, kita perlu mengedit file konfigurasi Nginx agar dapat berjalan dengan PHP-FPM. Gunakan nano untuk mengedit file tersebut:
    ~~~
    nano -l $PREFIX/etc/nginx/nginx.conf
    ~~~
    
      - Tekan Ctrl + / untuk mencari baris.
    
      - Cari baris 44-45 dan ubah root serta index menjadi seperti ini:
        ~~~
        root   /data/data/com.termux/files/home/htdocs;
        index  index.php index.html index.htm;
        ~~~
    
      - Selanjutnya, cari baris 65-71 dan hapus tanda # di beberapa bagian untuk mengaktifkan konfigurasi PHP-FPM:
        ~~~
        location ~ .php$ {
        root           /data/data/com.termux/files/home/htdocs;
        fastcgi_pass   unix://data/data/com.termux/files/usr/var/run/php-fpm.sock;
        fastcgi_index  index.php;
        #  fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        include        fastcgi.conf;
        }
        ~~~

  - Tekan Ctrl + X untuk keluar, lalu ketik Y dan Enter untuk menyimpan perubahan.

## 💻 Menjalankan dan Mengetes Server
Setelah konfigurasi selesai, mari kita jalankan server dan lakukan pengetesan.

  - Jalankan PHP-FPM & Nginx
    Ketikkan perintah berikut untuk memulai kedua layanan secara bersamaan:
    ~~~
    php-fpm && nginx
    ~~~
    
      - php-fpm adalah proses yang akan mengelola eksekusi kode PHP.
      - nginx adalah web server yang akan melayani permintaan HTTP.

  - Buat Direktori dan File PHP
    Sekarang, buat folder htdocs di direktori home Anda dan masuk ke dalamnya:
    ~~~
    mkdir htdocs && cd htdocs
    ~~~
    
    Di dalam folder htdocs, buat file index.php untuk pengetesan:
    ~~~
    nano -l index.php
    ~~~
    
    Tambahkan kode berikut ke dalam file index.php:
    ~~~
    <?php
    phpinfo();
    ?>
    ~~~

    - Simpan file dengan menekan Ctrl + X, ketik Y, dan Enter.

  - Akses Melalui Browser
    Buka browser di perangkat Anda (Chrome, Firefox, dll.) dan ketikkan alamat berikut di bilah URL:
    ~~~
    localhost:8080
    ~~~
    
    Jika semua berjalan dengan benar, Anda akan melihat halaman phpinfo() yang menampilkan detail konfigurasi PHP Anda.

## 🚦 Perintah Penting
Berikut adalah beberapa perintah dasar untuk mengelola Nginx:

  - Mulai Nginx:
    ~~~
    nginx
    ~~~

  - Berhenti/Matikan Nginx:
    ~~~
    nginx -s stop
    ~~~

  - Memuat Ulang Konfigurasi Nginx:
    ~~~
    nginx -s reload
    ~~~
    
    Perintah ini sangat berguna setelah Anda melakukan perubahan pada file konfigurasi tanpa perlu mematikan dan menyalakan ulang server.
