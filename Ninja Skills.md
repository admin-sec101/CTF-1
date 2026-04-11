🥷 TryHackMe: Ninja Skills - Writeup & Notes

Dokumentasi ini berisi langkah-langkah teknis dan perintah Linux yang digunakan untuk menyelesaikan tantangan "Ninja Skills" di platform TryHackMe. Fokus utama tantangan ini adalah kemahiran menggunakan perintah find, grep, dan manipulasi file di Linux.

📋 Deskripsi Tantangan

Mencari sekumpulan file spesifik yang tersebar di seluruh sistem file dan mengekstrak informasi tertentu (seperti jumlah baris, pemilik, atau konten) untuk menjawab pertanyaan kuis.

🔍 Daftar File Target

Daftar file yang perlu diidentifikasi lokasinya:
8V2L, bny0, c4ZX, D8B3, FHl1, oiM0, PFbD, rmfX, SRSq, uqyw, v2Vb, X1Uy.

🛠️ Langkah-Langkah & Perintah

1. Mencari Lokasi File
   
Gunakan perintah find untuk melacak semua file target di seluruh direktori root (/) sambil membuang pesan error (Permission Denied) ke /dev/null.

```bash

find / -type f \( -name 8V2L -o -name bny0 -o -name c4ZX -o -name D8B3 -o -name FHl1 -o -name oiM0 -o -name PFbD -o -name rmfX -o -name SRSq -o -name uqyw -o -name v2Vb -o -name X1Uy \) 2>/dev/null
```

Gunakan kode dengan hati-hati.

2. Menganalisis Jumlah Baris

Untuk menemukan file yang memiliki jumlah baris spesifik (misalnya 230 baris), gunakan flag -exec dengan wc -l.

```bash

find / -type f \( -name ... \) -exec wc -l {} + 2>/dev/null
```

Gunakan kode dengan hati-hati.

3. Mencari Konten Spesifik (Flag)
   
Jika tantangan meminta Anda menemukan string tertentu di dalam file-file tersebut:

```bash

grep -rnE "THM{|string_kunci" /path/ke/direktori/target 2>/dev/null
```

Gunakan kode dengan hati-hati.

📝 Hasil Temuan Sementara

Nama File	Lokasi	Jumlah Baris
```
D8B3	/mnt/D8B3	209
c4ZX	/mnt/c4ZX	209
v2Vb	/home/v2Vb	209
bny0	(Cek Lokasi)	230
```
Dibuat untuk keperluan edukasi dan dokumentasi belajar keamanan siber.
