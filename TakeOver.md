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

Gunakan kode dengan hati-hati.
### 2. Subdomain Enumeration (VHost Fuzzing)
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

### 3. Analisis Sertifikat SSL (Deep Recon)
Melakukan inspeksi pada sertifikat SSL di port 443 untuk mencari Subject Alternative Names (SAN) yang mungkin membocorkan subdomain lain.
```bash

openssl s_client -connect 10.48.147.210:443 | openssl x509 -noout -text | grep DNS
```

Gunakan kode dengan hati-hati.
Ditemukan petunjuk mengenai subdomain support.futurevera.thm. Melalui fuzzing lanjutan pada protokol HTTPS, ditemukan subdomain rahasia yang panjang: secrethelpdesk934752.support.futurevera.thm.
### 4. Menemukan Flag (Subdomain Takeover)
Setelah mendaftarkan subdomain rahasia tersebut ke /etc/hosts, dilakukan pengecekan header HTTP untuk melihat ke mana domain tersebut mengarah.
```bash

curl -I http://futurevera.thm
```

Gunakan kode dengan hati-hati.
Analisis Respons:
Server memberikan respons 302 Found yang melakukan redirect ke alamat AWS S3 Bucket yang mengandung flag.
```text

Location: http://flag{beea0d6edfcee06a59b83fb50ae81b2f}://
```

Gunakan kode dengan hati-hati.
```Flag: flag{beea0d6edfcee06a59b83fb50ae81b2f}```

💡 Pelajaran yang Didapat (Key Takeaways)

    DNS Hygiene: Selalu hapus catatan DNS (CNAME/A record) jika layanan pihak ketiga (seperti S3 Bucket) sudah tidak digunakan.
    SSL Leakage: Sertifikat SSL seringkali membocorkan daftar seluruh subdomain perusahaan.

    HTTPS vs HTTP: Konfigurasi Virtual Host bisa berbeda antara port 80 dan 443, selalu cek keduanya.

Disclaimer: Dokumentasi ini dibuat hanya untuk tujuan edukasi keamanan siber.
<img width="772" height="485" alt="1" src="https://github.com/user-attachments/assets/89a23507-e423-4c99-9790-73df654ffdae" />
<img width="764" height="69" alt="2" src="https://github.com/user-attachments/assets/d82c3ce2-3492-4849-b29b-6ec99e247487" />
<img width="772" height="247" alt="3" src="https://github.com/user-attachments/assets/313a3b7e-3f26-4724-ae41-9ff3dbcb7159" />

