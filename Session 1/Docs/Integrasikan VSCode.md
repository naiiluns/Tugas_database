# Cara Integrasi VSCode dengan GitHub

### 1. **Buat Akun GitHub**
Buka https://github.com lalu daftar dengan email aktif

### 2. **Buka **Terminal** kemudian Buat Folder**
Jalankan perintah ini di Terminal
```bash
mkdir .ssh
```

### 3. **Generate SSH Key**
Jalankan perintah:
```bash
ssh-keygen -t ed25519 -c "youremail@example.com"
```
Bagian "youremail@example.com" ganti dengan email yang terdaftar **GitHub** 

### 4. **Generate SSH Key**
Jalankan perintah:
```bash
ssh-keygen -t rsa -b 4096 -C "youremail@example.com"
```
Bagian "youremail@example.com" masukkan nama bebas, lalu tekan enter.

### 5. **Lewati Passphrase**
Saat muncul tulisan *Enter passphrase*, cukup tekan enter dua kali tanpa mengetik apa-apa.

### 6. **Cek Isi Folder**
Jalankan perintah ini untuk memastikan file sudah berhasil dibuat
```bash
ls
```

### 7. **Tampilkan Isi File**
Jalankan perintah ini lalu akan memunculkan kode panjang:
```bash
cat example.pub
```

### 8. **Salin Kode**
Salin kode panjang tersebut (dimulai dari *ssh-rsa...* sampai alamat email di belakang).

### 9. **Buka Github**
Buka **GitHub**, klik icon profil kanan atas lalu pilih settings

### 10. **Masuk ke Menu SSH and GPG Keys**
Setelah masuk ke menu **SSH and GPG Keys**, klik tombol **New SSH Key** lalu masukkan kode panjang yang sebelumnya sudah disalin. Kemudian klik **Add SSH Key**

### 11. **Verifikasi Via Email**
Jika Github meminta verifikasi, pencet link verifikasi yang muncul.

### 12. **Terakhir, Masukkan Kode Verifikasi**
Cek inbox email, salin kode yang dikirim, lalu masukkan ke Github
