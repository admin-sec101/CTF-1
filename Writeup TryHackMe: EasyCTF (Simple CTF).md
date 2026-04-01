🚩 TryHackMe: EasyCTF (Simple CTF) Writeup

<img width="1232" height="538" alt="image" src="https://github.com/user-attachments/assets/bce2917d-1a46-405c-a216-20c084b4fcd8" />

Dokumentasi lengkap proses Security Audit dan Penetration Testing pada mesin EasyCTF (Simple CTF) di platform TryHackMe. Tantangan ini mencakup enumerasi jaringan, eksploitasi kerentanan Web (SQL Injection), hingga eskalasi hak akses (Privilege Escalation) di lingkungan Linux.
🛠️ Informasi Mesin & Alat

    Target IP: 10.49.154.112

    Sistem Operasi: Linux (Ubuntu)
    Tools Utama:
        Nmap: Port scanning & service discovery.
        Gobuster: Directory brute-forcing.
        Searchsploit: Exploit database lookup.
        Python: Menjalankan skrip eksploitasi.
        SSH: Akses remote shell.

🔍 Tahap 1: Enumerasi (Reconnaissance)
1.1 Pemindaian Port (Nmap)
Melakukan pemindaian terhadap seluruh port untuk mengidentifikasi layanan yang berjalan:
bash

nmap -sC -sV -p- 10.49.154.112

Gunakan kode dengan hati-hati.
Hasil Temuan:

    Port 21 (FTP): Terbuka (Anonymous login diperbolehkan).
    Port 80 (HTTP): Terbuka (Apache Web Server).
    Port 2222 (SSH): Terbuka (SSH berjalan pada port non-standar).

1.2 Enumerasi Web (Gobuster)
Mencari direktori tersembunyi pada web server:
bash

gobuster dir -u http://10.49.154.112 -w /usr/share/wordlists/dirb/common.txt

Gunakan kode dengan hati-hati.
Temuan Penting: Direktori /simple ditemukan, yang mengarah ke sebuah instalasi CMS.
🛡️ Tahap 2: Analisis Kerentanan
Setelah menelusuri direktori http://10.49.154, teridentifikasi penggunaan CMS Made Simple versi 2.2.8.

    Vulnerability: SQL Injection (Unauthenticated Time-based Blind SQLi).
    CVE: CVE-2019-9053.
    Deskripsi: Kerentanan ini memungkinkan penyerang mengekstrak data sensitif dari database tanpa memerlukan autentikasi.

🚀 Tahap 3: Eksploitasi (Gaining Access)
3.1 Menjalankan Skrip Eksploitasi
Menggunakan skrip Python dari Exploit-DB (ID: 46635) untuk melakukan serangan SQL Injection secara otomatis:
bash

python 46635.py -u http://10.49.154 --crack -w /usr/share/wordlists/rockyou.txt

Gunakan kode dengan hati-hati.
Kredensial yang Didapatkan:

    Username: mitch
    Password: secret

3.2 Akses Remote (SSH)
Menggunakan kredensial tersebut untuk masuk ke sistem melalui SSH pada port 2222:
bash

ssh mitch@10.49.154.112 -p 2222

Gunakan kode dengan hati-hati.

    User Flag: G00d j0b, keep up!
    User Lain: Ditemukan user lain bernama sunbath di direktori /home.

⚡ Tahap 4: Privilege Escalation
4.1 Audit Sudo (sudo -l)
Memeriksa binari yang dapat dijalankan dengan hak akses root tanpa password:
bash

sudo -l

Gunakan kode dengan hati-hati.
Temuan: User mitch diizinkan menjalankan /usr/bin/vim sebagai root (NOPASSWD).
4.2 Vim Breakout (GTFOBins)
Memanfaatkan fitur eksekusi sistem pada Vim untuk memicu shell root:
bash

sudo vim -c ':!/bin/sh'

Gunakan kode dengan hati-hati.
Setelah shell muncul, verifikasi identitas dengan whoami, hasilnya adalah root.
🏁 Tahap 5: Flag Akhir
Root Flag
Ditemukan di direktori home milik root:
bash

cd /root
cat root.txt

Gunakan kode dengan hati-hati.
Isi Flag: W3ll d0n3. You made it!
📝 Kesimpulan
Penyerangan pada mesin EasyCTF ini menunjukkan betapa pentingnya:

    Memperbarui CMS ke versi terbaru (Patching).
    Mengubah port layanan standar (SSH) tidak cukup jika kredensial lemah.
    Konfigurasi sudoers yang terlalu longgar (misal: izin Vim) dapat menyebabkan eskalasi hak akses penuh.
    
Ringkasan Hasil EasyCTF
Berikut adalah rangkuman poin-poin penting yang sudah Anda selesaikan:

***
How many services are running under port 1000?    ```2```
What is running on the higher port?               ```ssh```
What's the CVE you're using against the application? Vulnerability: SQL Injection (```CVE-2019-9053```).
To what kind of vulnerability is the application vulnerable?            ```sqli```
What's the password? Password:             ```secret```.
Where can you login with the details obtained?           ```ssh```     
        Login Method: SSH pada port 2222.
What's the user flag?User Flag:             ```G00d j0b, keep up!```
Is there any other user in the home directory? What's its name? Other User:             ```sunbath```.
What can you leverage to spawn a privileged shell? PrivEsc Method: Memanfaatkan binary ```vim```.
What's the root flag? Root Flag:             ```W3ll d0n3. You made it!```.
***

        Vulnerability (SQLi): Menjelaskan pintu masuk Anda. Tanpa tahu jenis celahnya, kita tidak bisa mengeksploitasi sistem.
    Password & Login: Menjelaskan cara Anda bertahan di dalam sistem (Persistence/Access).
    Port 2222: Menjelaskan hasil enumerasi (pengamatan) Anda bahwa target mencoba menyembunyikan SSH, tapi tetap ketahuan.
    User & Root Flag: Ini adalah bukti keberhasilan (Proof of Concept) bahwa Anda sudah menembus level user biasa dan level tertinggi (admin).
    PrivEsc (Vim): Ini bagian paling krusial, karena menjelaskan kelemahan fatal pada konfigurasi sistem tersebut.

    Sedikit Penjelasan "Kenapa" Hal-hal Itu Terjadi:

    Kenapa SQLi? Karena pengembang CMS-nya lupa menyaring input dari user, sehingga database-nya bisa "dibujuk" untuk membocorkan password.
    Kenapa port 2222? Biasanya admin mengubah port SSH dari 22 ke 2222 untuk menghindari serangan otomatis dari bot internet, tapi bagi pentester seperti Anda, itu cuma masalah waktu sebelum ditemukan lewat Nmap.
    Kenapa Vim bisa jadi Root? Ini adalah kesalahan admin. Memberikan izin sudo pada aplikasi yang punya fitur "shell escape" (seperti Vim, Nano, atau Less) sama saja dengan memberikan kunci utama gedung kepada orang asing.
    
Disclaimer: Dokumentasi ini dibuat hanya untuk kepentingan edukasi dan pembelajaran keamanan informasi secara etis.
