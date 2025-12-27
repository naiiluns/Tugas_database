<<<<<<< HEAD
# Cara Menginstal Visual Studio Code di Linux Mint

Berikut adalah langkah-langkah untuk menginstal VS Code di Terminal:

### 1.  **Perbarui Sistem**
    Jalankan perintah ini untuk memastikan sistemmu sudah diperbarui:
    
    ```bash
    sudo apt update
    ```
    
### 2.  **Instal Dependensi**
    Instal paket-paket yang dibutuhkan untuk menginstal VS Code:
    
    ```bash
    sudo apt install software-properties-common apt-transport-https wget
    ```
    
### 3.  **Impor Kunci Repository**
    Unduh dan impor kunci yang diperlukan untuk verifikasi paket:
    
    ```bash
    wget -q [https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc) -O- | sudo apt-key add -
    ```
    
### 4.  **Tambahkan Repositori VS Code**
    Jalankan perintah ini untuk menambahkan repositori VS Code ke sistemmu:
    
    ```bash
    sudo add-apt-repository "deb [arch=amd64] [https://packages.microsoft.com/repos/vscode](https://packages.microsoft.com/repos/vscode) stable main"
    ```
    
### 5.  **Perbarui dan Instal**
    Sekarang, perbarui daftar paket dan instal VS Code:
    
    ```bash
    sudo apt update
    sudo apt install code
    ```
    
### 6.  **Verifikasi Instalasi**
    Setelah instalasi selesai, kamu bisa membuka VS Code dengan mengetik perintah `code` di Terminal, atau mencarinya di menu aplikasi.
    
