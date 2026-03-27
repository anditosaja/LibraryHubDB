# LibraryHubDB
Sistem manajemen perpustakaan berbasis Node.js, Express, dan MongoDB. Mendukung fitur pengelolaan buku, anggota, peminjaman, serta review dengan sistem poin dan denda.

## Fitur yang tersedia
1. Manajemen Buku (CRUD + filter + search)
2. Manajemen Anggota (CRUD + soft delete untuk nonaktif)
3. Sistem Peminjaman & Pengembalian
4. Perhitungan Denda Otomatis
5. Sistem Poin untuk Anggota
6. Review Buku (ketika pernah meminjam)
7. Relasi data dengan MongoDB (menggunakan populate())

## Teknologi yang dipakai
Pastikan semua sudah terinstall
* Node.js
* Express.js
* Mongodb Compass/Mongodb Server Lokal
* Mongoose
* dotenv

## CMD 
Pastikan Command Prompt berada di Root dengan perintah `cd..`

## Instalasi
Install semua yang diperlukan, lakukan di terminal cmd
* `npm install express`
* `npm install mongoose`
* `npm install dotenv`

## Folder (Opsional)
Buat Folder agar lebih terstruktur.
* `mkdir models`
*  `mkdir routes`
*  `mkdir middleware`
*  `mkdir seed`

## Konfigurasi Database
Lakukan di root, buat file ".env" yang berisikan PORT dan MONGO_URI (untuk koneksi ke lokal MongoDB)

## MongoDB
* Jalankan MongoDB Lokal, dapat dicek pada "services.msc" apakah sudah running
* Jalankan MongoDB Compass, koneksikan ke: `mongodb://127.0.0.1:27017`

## SEED
Seed data ini berisikan dengan dummy data, dapat dijalankan di terminal cmd
 `node seed/seed.js`

## Menjalankan Server
Jalankan di terminal laptop
`node app.js` atau `npx nodemon app.js` (nodemon agar auto restart jika ada perubahan dalam file)

## Base Url
Dapat dijalankan di browser ataupun Postman
`http://localhost:3000`

## Middleware
Memiliki Logger, sehingga setiap request akan log

## ENDPOINT API: 
Diperoleh dari kebutuhan penugasan
1. Resource: Buku (/buku)
Method Path Deskripsi
* GET /buku Ambil semua buku
* GET /buku/:id Ambil buku berdasarkan ID
* GET /buku?genre=:genre * Filter buku berdasarkan genre
* GET /buku?search=:keyword * Cari buku berdasarkan judul atau pengarang (regex)
* GET /buku/:id/review * Ambil semua review untuk buku tertentu (populate anggota)
* POST /buku Tambah buku baru
* PUT /buku/:id Update data buku
* DELETE /buku/:id Hapus buku (validasi: tidak boleh hapus jika sedang dipinjam)

2. Resource: Anggota (/anggota)
Method Path Deskripsi
* GET /anggota Ambil semua anggota
* GET /anggota/:id Ambil anggota berdasarkan ID
* GET /anggota/:id/riwayat * Ambil riwayat peminjaman anggota (populate buku)
* POST /anggota Daftarkan anggota baru
* PUT /anggota/:id Update data anggota
* DELETE /anggota/:id Nonaktifkan anggota (soft delete: ubah status ke nonaktif)

3. Resource: Peminjaman (/pinjam)
Method Path Deskripsi
* GET /pinjam Ambil semua data peminjaman (populate buku & anggota)
* GET /pinjam/:id Ambil detail peminjaman
* GET /pinjam?status=terlambat * Filter peminjaman yang terlambat
* POST /pinjam * Buat peminjaman baru (validasi stok, kurangi stok, set tgl_kembali_rencana +7 hari)
* PUT /pinjam/:id/kembali * Proses pengembalian: hitung denda (Rp2.000/hari terlambat), tambah poin anggota, tambah stok
* PUT /pinjam/cek-terlambat * Update status semua peminjaman yang melewati tgl_kembali_rencana menjadi 'terlambat'

4. Resource: Review (/review)
Method Path Deskripsi
* GET /review Ambil semua review (populate buku & anggota)
* POST /review * Tambah review (validasi: anggota harus pernah meminjam buku tersebut)
* PUT /review/:id Update review
* DELETE /review/:id Hapus review

## ANDITO DWI WICAKSONO - 2410511115
