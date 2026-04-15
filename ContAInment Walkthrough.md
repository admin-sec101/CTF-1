🚩 TryHackMe - ContAInment Walkthrough
Dokumentasi langkah-langkah investigasi insiden keamanan menggunakan analisis forensik dan bantuan AI pada workstation yang terkompromi.

📝 Skenario
Terjadi aktivitas mencurigakan pada workstation peneliti senior Oliver Deer (o.deer). Data sensitif telah dieksfiltrasi dan dienkripsi oleh penyerang menggunakan teknik manipulasi AI (Prompt Injection). Tugas kita adalah melacak jejak penyerang, menemukan kunci enkripsi, dan mengidentifikasi flag yang asli.
🛠️ Langkah-langkah Investigasi
1. Akses Awal
Lakukan koneksi ke workstation korban menggunakan SSH:
bash

ssh o.deer@<TARGET_IP>
# Password: TryHackMe!

Gunakan kode dengan hati-hati.
2. Analisis Lalu Lintas Jaringan (PCAP)
Penyerang meninggalkan jejak aktivitas di folder dokumen. Kita menemukan beberapa file dump PCAP.
bash

ls -la /home/o.deer/Documents/pcap_dumps/2025-06-17/

Gunakan kode dengan hati-hati.
File session_4444_dump.pcap terlihat mencurigakan karena ukurannya yang besar dan penggunaan port 4444 (umum untuk reverse shell).
3. Ekstraksi Informasi & Password
Gunakan perintah strings untuk melihat isi komunikasi di dalam PCAP. Terungkap adanya serangan Prompt Injection terhadap asisten AI.
bash

strings /home/o.deer/Documents/pcap_dumps/2025-06-17/session_4444_dump.pcap

Gunakan kode dengan hati-hati.
Temuan Penting:
Ditemukan string tersembunyi di akhir log: **w#e@%s~t^t-e$c*h_v^i%ct_im_1**.
Setelah dibersihkan dari karakter simbol, kita mendapatkan password:

    Password: westtechvictim1

4. Dekripsi File Proyek
Gunakan password tersebut untuk mengekstrak file proyek yang dienkripsi ke direktori /dev/shm:
bash

unzip -P westtechvictim1 /home/o.deer/westtech_projects_encrypted.zip -d /dev/shm

Gunakan kode dengan hati-hati.
5. Identifikasi Flag (Analisis Data & Base64)
Di dalam file thm_flags.txt, data disimpan dalam format Base64. Sesuai petunjuk, flag yang asli mengandung tepat 3 bilangan prima antara 10 hingga 99.
Gunakan skrip Python otomatis untuk melakukan decoding dan penyaringan:
python

import re, base64

def is_prime(n):
    n = int(n)
    if n < 2: return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0: return False
    return True

path = '/dev/shm/home/o.deer/westtech_projects/thm_flags.txt'
with open(path, 'r') as f:
    for line in f:
        try:
            # Decode Base64
            decoded = base64.b64decode(line.strip()).decode('utf-8')
            # Cari angka 2 digit
            nums = re.findall(r'\d{2}', decoded)
            # Filter angka prima
            primes = [n for n in nums if is_prime(n)]
            
            if len(primes) == 3:
                print(f"Flag Ditemukan: {decoded}")
        except:
            continue

Gunakan kode dengan hati-hati.
🏆 Hasil Akhir
Berdasarkan hasil penyaringan, flag yang valid adalah:
thm{23,82,20,17,53}
Verifikasi Angka Prima:

    23 (Prima)
    17 (Prima)
    53 (Prima)
    (82 dan 20 bukan bilangan prima).

🛡️ Pelajaran yang Diambil

    AI Security: Pentingnya memitigasi serangan Prompt Injection agar AI tidak membocorkan data sensitif.
    Forensik Jaringan: File PCAP seringkali menyimpan kredensial atau draft pesan penyerang yang sangat berharga.
    Data Obfuscation: Penggunaan Base64 dan karakter simbolis sering digunakan penyerang untuk menyembunyikan informasi penting.



<img width="1346" height="275" alt="image" src="https://github.com/user-attachments/assets/cbf209fe-a6fa-4121-a712-ddd55e27c4a6" />




<img width="1031" height="530" alt="image" src="https://github.com/user-attachments/assets/7c751fff-2b5d-4b7c-a1d0-90be611a1240" />
