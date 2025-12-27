# Cara Instal MongoDB

### 1. Buka terminal
Jalankan perintah ini untuk menginstal kunci publik MongoDB: 
```bash
wget -qO - https://www.mongodb.org/static/pgp/server-7.0.asc | sudo apt-key add - 
``` 


### 2. Buka File daftar repository
Jalankan perintah ini: 
```bash
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```


### 3. Perbarui daftar paket
Lanjutkan dengan kode ini: 
```bash
sudo apt update
```


### 4. Install MOngoDB
Jalankan perintah ini: 
```bash
sudo apt install mongodb-org
```

### 5. Mulai Layanan
Jalankan perintah ini:
```bash
sudo systemctl start mongod
```
```bash
sudo systemctl enable mongod
```
Tempel keduanya di **Terminal** dengan **Ctrl+Shift+V**


### 6. Cek Status
Jalankan perintah ini: 
```bash
sudo systemctl status mongod
```
Jika MongoDB berhasil terinstal, akan muncul tulisan active(running).
Untuk keluar dari tampilan status, klik **:q** lalu enter


### 7. Masuk ke Shell MongoDB
Jalankan perintah ini: 
```bash
mongosh
```