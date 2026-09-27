# BOWOX STORE — Firebase V3

File:
- `index.html` = website pembeli
- `admin.html` = website admin
- `firestore.rules` = aturan Firestore

## 1. Aktifkan Anonymous Authentication
Di Firebase Console:
Authentication → Sign-in method → Anonymous → Enable → Save.

Website ini memakai anonymous auth untuk membuat koneksi Firebase. Login username/password Bowox yang tampil di website masih mengikuti sistem UI lama, sedangkan data toko disinkronkan ke Firestore.

## 2. Buat Firestore Database
Firebase Console → Build → Firestore Database → Create database.
Untuk pengujian, pilih mode yang sesuai lalu buat database.
Setelah database dibuat, buka Rules dan gunakan isi `firestore.rules` dari paket ini.

## 3. Deploy
Kedua file HTML bisa diletakkan di hosting yang sama:
- `/index.html`
- `/admin.html`

Jangan menjalankan versi final dengan `file://` jika Firebase bermasalah. Gunakan hosting/localhost/HTTPS.

## 4. Data yang sekarang disinkronkan
Dokumen Firestore:
`bowox_store/main`

Field utama:
- `db` = order, topup, saldo, log saldo, dan data transaksi lain yang dipakai website
- `customers` = daftar akun pembeli
- `admins` = daftar akun admin

Perubahan dari HP pembeli/admin akan diterima oleh halaman lain melalui listener Firestore.

## 5. Catatan keamanan
`firebaseConfig` web boleh berada di HTML; itu bukan password Firebase. Jangan memasukkan service-account private key atau password Google ke HTML.

Rules di paket ini hanya memastikan pengguna yang sudah authenticated (anonymous) dapat mengakses dokumen. Karena sistem login admin lama masih berupa username/password di sisi browser, ini cocok sebagai tahap sinkronisasi/prototipe, bukan sistem pembayaran produksi. Untuk produksi, login admin sebaiknya dipindahkan ke Firebase Authentication dan hak admin dibatasi dengan Security Rules/custom claims.

## 6. QRIS
`index.html` masih memakai URL QRIS yang ada di konfigurasi. Jika QRIS yang benar sudah tersedia, ganti nilai `QRIS_IMAGE_URL` ke URL gambar QRIS langsung atau gunakan file lokal `assets/qris.jpeg` sesuai kebutuhan.
