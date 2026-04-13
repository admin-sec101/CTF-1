Wekor - TryHackMe Writeup
Dokumentasi ini berisi langkah-langkah penyelesaian (writeup) untuk mesin Wekor di platform TryHackMe. Tantangan ini berfokus pada teknik enumerasi, eksploitasi web, dan eskalasi hak istimewa di lingkungan Linux.
📝 Ringkasan Mesin

    Nama Mesin: Wekor
    Tingkat Kesulitan: Medium
    Sistem Operasi: Linux
    Fokus Utama: SQL Injection (SQLi), WordPress, VHost Enumeration, Memcached, dan Reverse Engineering sederhana.

🚀 Langkah Penyelesaian
1. Enumerasi Awal
Langkah pertama adalah pemindaian port menggunakan Nmap untuk mengidentifikasi layanan yang berjalan:

```
$ sudo nmap -p- wekor.thm -vvv -sCV -T4
```
    Port 80 (HTTP): Layanan web utama.
    Port 22 (SSH): Akses jarak jauh.

Dianjurkan untuk menambahkan entri domain ke file hosts lokal agar mempermudah akses:
bash

```echo "<IP_ADDRESS> wekor.thm" | sudo tee -a /etc/hosts```

<img width="523" height="75" alt="image" src="https://github.com/user-attachments/assets/b8fe7c2a-4043-4c44-9f99-460db5be58d1" />

2. Eksploitasi Web & SQL Injection

    Directory Brute-forcing: Ditemukan direktori tersembunyi melalui file robots.txt yang mengarah ke /it-next.
    SQLi: Pada bagian keranjang belanja (it_cart.php), terdapat parameter yang rentan terhadap SQL Injection.
    SQLMap: Gunakan alat ini untuk mengekstrak data dari database, termasuk kredensial admin untuk WordPress.

```
┌──(kali㉿kali)-[~/TryHackMe]
└─$ sqlmap -u http://wekor.thm/it-next/it_cart.php --data "coupon_code=&apply_coupon=Apply%20Coupon" -D wordpress -T wp_users --dump
```
<img width="811" height="421" alt="image" src="https://github.com/user-attachments/assets/c970e128-95d1-4437-a4da-6939146234d0" />

3. Akses Awal (Initial Access)

    WordPress: Masuk ke dashboard admin menggunakan kredensial yang ditemukan.
    Reverse Shell: Ubah salah satu file tema PHP untuk menyisipkan payload reverse shell guna mendapatkan akses ke sistem sebagai user www-data.

<img width="1366" height="684" alt="image" src="https://github.com/user-attachments/assets/522d5638-f3a7-4731-baa8-8b07ef5a86f2" />


4. Eskalasi Hak Istimewa (Privilege Escalation)

    User Escalation: Melakukan enumerasi pada layanan Memcached untuk menemukan kata sandi user lokal.
    Root Escalation:
        Menganalisis file binari ELF yang mencurigakan.
        Melakukan teknik binary spoofing atau memanfaatkan variabel PATH untuk mengeksekusi perintah dengan hak akses root.

🚩 Flag
Dapatkan kedua flag untuk menyelesaikan tantangan ini:

    User Flag: /home/user/local.txt
    Root Flag: /root/proof.txt

    
