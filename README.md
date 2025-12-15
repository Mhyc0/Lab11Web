# Praktikum 12 – Autentikasi dan Session (PHP OOP)

Nama: ..........................................
NIM: ...........................................
Kelas: .........................................

---

## 1. Pendahuluan

Praktikum 12 membahas tentang **Autentikasi dan Session** pada aplikasi web berbasis PHP dengan konsep **Object Oriented Programming (OOP)**. Pada praktikum ini, mahasiswa mempelajari cara membuat sistem login sederhana, membatasi akses halaman menggunakan session, serta menambahkan fitur profil untuk user yang sedang login.

Autentikasi digunakan untuk memastikan bahwa hanya user yang berwenang yang dapat mengakses halaman tertentu, sedangkan session digunakan untuk menyimpan status login user selama masih berada di dalam aplikasi.

---

## 2. Tujuan Praktikum

Tujuan dari praktikum ini adalah:

1. Memahami konsep dasar autentikasi (login dan logout).
2. Memahami konsep dasar session pada PHP.
3. Mengimplementasikan sistem login sederhana menggunakan database.
4. Mengamankan halaman tertentu agar hanya dapat diakses setelah login.
5. Membuat fitur profil user dan perubahan password dengan enkripsi.

---

## 3. Persiapan Database

Database yang digunakan pada praktikum ini adalah **latihan_oop**.

### 3.1 Membuat Tabel Users

Tabel `users` digunakan untuk menyimpan data user/admin yang dapat login ke sistem.

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL,
    nama VARCHAR(100)
);
```

### 3.2 Menambahkan Data Dummy

Data dummy digunakan sebagai akun admin awal. Password tidak disimpan dalam bentuk teks biasa, melainkan sudah dienkripsi menggunakan `password_hash()`.

```sql
INSERT INTO users (username, password, nama)
VALUES ('admin', 'HASH_PASSWORD', 'Administrator');
```

---

## 4. Implementasi Autentikasi dan Session

### 4.1 Login User

Login diimplementasikan pada file `module/user/login.php`. Pada halaman ini:

* User memasukkan username dan password.
* Sistem mengambil data user dari database.
* Password diverifikasi menggunakan fungsi `password_verify()`.
* Jika login berhasil, session disimpan.

Session yang digunakan:

* `$_SESSION['is_login']`
* `$_SESSION['username']`
* `$_SESSION['nama']`

### 4.2 Proteksi Halaman dengan Session

Proteksi halaman dilakukan pada file `index.php`. Jika user belum login dan mencoba mengakses halaman selain halaman publik, maka user akan otomatis diarahkan ke halaman login.

Dengan cara ini, halaman seperti **artikel** dan **profil** hanya dapat diakses oleh user yang sudah login.

---

## 5. Modul User

### 5.1 Login

File: `module/user/login.php`

Fungsi utama:

* Menampilkan form login
* Memproses autentikasi user
* Menyimpan session jika login berhasil

### 5.2 Logout

File: `module/user/logout.php`

Fungsi utama:

* Menghapus seluruh session menggunakan `session_destroy()`
* Mengarahkan user kembali ke halaman login

---

## 6. Fitur Profil User

Fitur profil dibuat pada file `module/user/profile.php`.

Fungsi fitur profil:

* Menampilkan data user yang sedang login (Nama dan Username)
* Menyediakan form untuk mengubah password

### 6.1 Ubah Password

* User memasukkan password baru dan konfirmasi password
* Password baru dienkripsi menggunakan `password_hash()`
* Password lama di database diganti dengan password yang sudah terenkripsi

Keamanan:

* Halaman profil hanya dapat diakses jika user sudah login

---

## 7. Penyesuaian Tampilan Header

Menu navigasi dibuat dinamis sesuai dengan status login user.

### 7.1 Kondisi Belum Login

Menu yang tampil:

* Home
* Login

### 7.2 Kondisi Sudah Login

Menu yang tampil:

* Home
* Data Artikel
* Profil
* Logout (Nama User)

---

## 8. Hasil Pengujian

Pengujian dilakukan untuk memastikan seluruh fitur berjalan dengan baik.

1. Mengakses halaman artikel tanpa login

   * Hasil: diarahkan ke halaman login
2. Login menggunakan akun admin

   * Hasil: login berhasil
3. Mengakses halaman artikel setelah login

   * Hasil: halaman dapat diakses
4. Mengakses menu profil

   * Hasil: data user tampil dengan benar
5. Mengubah password melalui halaman profil

   * Hasil: password berhasil diubah
6. Logout dari sistem

   * Hasil: kembali ke halaman login
7. Login ulang menggunakan password baru

   * Hasil: login berhasil

---

## 9. Struktur Folder Project

```
lab11_php_oop/
│
├── module/
│   ├── user/
│   │   ├── login.php
│   │   ├── logout.php
│   │   └── profile.php
│   ├── artikel/
│
├── template/
│   ├── header.php
│   └── footer.php
│
├── class/
├── index.php
└── README.md
```

---

## 10. Kesimpulan

Dari praktikum ini dapat disimpulkan bahwa:

1. Autentikasi dan session sangat penting dalam pengamanan aplikasi web.
2. Penggunaan session memungkinkan sistem mengetahui status login user.
3. Fungsi `password_hash()` dan `password_verify()` meningkatkan keamanan password.
4. Si
