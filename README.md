**Nama : Nabilla Tsani Ayasi**

**NIM : H1D022058**

**Shift : F**

## Cara Kerja Login

1. **Membuat API untuk Login di Backend (PHP)**
   - Di backend, kita punya file `login.php` yang bertugas menerima data `username` dan `password` yang dikirim dari aplikasi Ionic.
   - Data ini diterima sebagai JSON, lalu diambil dan diubah menjadi format array PHP.
   - Selanjutnya, `username` dan `password` tersebut dicocokkan dengan data yang ada di database (di tabel `user`).
   - Kalau `username` dan `password` cocok, kita buat respons berupa JSON yang mengandung `username`, `token` (kode unik untuk identifikasi sesi login), dan status login (`status_login`) sebagai `berhasil`.
   - Kalau tidak cocok, responsnya hanya `status_login` sebagai `gagal`.

2. **Membuat Authentication Service di Ionic**
   - `AuthenticationService` di Ionic bertugas untuk mengelola proses login.
   - Fungsi `postMethod` mengirimkan `username` dan `password` ke API login di backend.
   - Jika login berhasil, fungsi `saveData` menyimpan token dan `username` di penyimpanan lokal agar pengguna tetap masuk meski aplikasi ditutup sementara.
   - Fungsi `logout` digunakan untuk menghapus data sesi ini ketika pengguna memilih keluar dari akun mereka.

3. **Menambahkan Guard untuk Autentikasi**
   - Guard adalah cara untuk membatasi akses halaman.
   - `authGuard` memastikan bahwa hanya pengguna yang sudah login yang bisa membuka halaman `home`.
   - `autoLoginGuard` otomatis mengarahkan pengguna yang sudah login langsung ke halaman `home` ketika mencoba mengakses halaman `login` lagi.

4. **Halaman Login di Ionic**
   - Di `login.page.html`, ada form untuk memasukkan `username` dan `password`.
   - Ketika tombol `Login` ditekan, fungsi `login()` dijalankan.
   - Fungsi ini akan memeriksa apakah `username` dan `password` sudah diisi, lalu mengirimkan data tersebut ke API untuk diperiksa.
   - Jika login berhasil, data token dan `username` disimpan, dan pengguna diarahkan ke halaman `home`.
   - Jika gagal, pengguna diberi pesan error sesuai kondisi yang terjadi, misalnya “Username atau Password salah” atau “Periksa koneksi internet Anda”.

5. **Halaman Home di Ionic**
   - Di halaman `home.page.html`, pengguna akan melihat pesan “Selamat datang” diikuti nama mereka.
   - Ada opsi `Logout` yang memanggil fungsi `logout()` untuk membersihkan data sesi, dan pengguna dikembalikan ke halaman login.

Secara keseluruhan, proses login bekerja dengan mengirimkan data ke API untuk memverifikasi informasi pengguna. Jika valid, data sesi disimpan, dan pengguna bisa mengakses halaman tertentu. Guard menjaga agar halaman tertentu hanya bisa diakses oleh pengguna yang sudah login.
