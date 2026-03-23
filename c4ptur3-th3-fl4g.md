
# [c4ptur3-th3-fl4g](https://tryhackme.com/room/c4ptur3th3fl4g)

# ***Translation & Shifting — Task 1***
Pertanyaan 1: `c4n y0u c4p7u23 7h3 f149?`
Ini disebut leet speak, di mana teks ditulis dengan ejaan yang dimodifikasi menggunakan angka.
Mengganti angka dengan huruf yang mirip secara visual:
4 = A
0 = O
7 = T
2 = R
3 = E
1 = I
Hasil translasi: "can you capture the flag?"
Hasilnya: ```can you capture the flag?```

Pertanyaan 2:
``` 01101100 01100101 01110100 01110011 00100000 01110100 01110010 01111001 00100000 01110011 01101111 01101101 01100101 00100000 01100010 01101001 01101110 01100001 01110010 01111001 00100000 01101111 01110101 01110100 00100001 ```
Apa arti dari rangkaian angka 1 dan 0 ini? Ini adalah biner, "bahasa komputer". Gunakan Binary Decoder untuk menerjemahkannya.
Kode biner yang kamu kirimkan itu kalau diterjemahkan artinya:
``` lets try some binary out ```

Pertanyaan 3: MJQXGZJTGIQGS4ZAON2XAZLSEBRW63LNN5XCA2LOEBBVIRRHOM======
Adanya tanda sama dengan (=) di akhir string menandakan ini adalah Base32 atau Base64. Dalam kasus ini, kita menggunakan dekoder Base32.
Kode tersebut dienkode menggunakan Base32. Jika didekode, hasilnya adalah:
``` let's try some base32 out ```

Pertanyaan 4:``` RWFjaCBCYXNlNjQgZGlnaXQgcmVwcmVzZW50cyBleGFjdGx5IDYgYml0cyBvZiBkYXRhLg== ```
Kode di bawah ini:
``` Ym5nZ3Z6cnZ6YXJnciBnYmJ5YmJncmU= ```
Petunjuk:
Decode dari Base64 terlebih dahulu.
Shift hasilnya menggunakan ROT13 (geser 13 huruf).
Dan yang satu ini dalam bentuk Base64. Anda bisa menggunakan alat di Base64Decode.org.

Pertanyaan 5: ``` 68 65 78 61 64 65 63 69 6d 61 6c 20 6f 72 20 62 61 73 65 31 36 3f ```
Keberadaan angka dan huruf yang tidak melebihi huruf 'f' mengarah pada format heksadesimal (Base16).
Decode Hexadecimal
Untuk memecahkan kode ini, Anda perlu mengubah setiap pasangan angka dan huruf menjadi karakter ASCII yang sesuai.
``` 68 65 78 61 64 65 63 69 6d 61 6c 20 6f 72 20 62 61 73 65 31 36 3f ```
Ketika dikonversi dari Hex ke teks, hasilnya adalah:
Answer:
``` hexadecimal or base16? ```

Pertanyaan 6: ``` Ebgngr zr 13 cynprf! ```
Dilihat dari jawabannya, bentuk karakternya sama dengan pertanyaannya. Ini memastikan bahwa ini adalah sandi pergeseran karakter tunggal, yaitu ROT13. ROT13 adalah sandi sederhana di mana setiap huruf "diputar" sebanyak 13 posisi dalam alfabet.
Adanya tanda sama dengan (=) di akhir string sering digunakan sebagai padding (pengisi) untuk memastikan panjang string Base32 atau Base64 valid, seperti yang kamu identifikasi.
Dalam kasus ini, ini adalah Base32, dan logikamu benar. Hasil dekodenya adalah:
Answer:
``` let's try some base32 out ```

Pertanyaan 7: ``` *@F DA:? >6 C:89E C@F?5 323J C:89E C@F?5 Wcf E:>6DX ```
Ini mirip dengan sebelumnya, namun menggunakan sandi ROT47. Alih-alih hanya huruf A-Z, sandi ini menggunakan hampir semua karakter dalam tabel kode ASCII.
*@F DA:? >6 C:89E C@F?5 323J C:89E C@F?5 Wcf E:>6DX, adalah kode yang dienkripsi menggunakan ROT47.
Tidak seperti ROT13 yang hanya menggeser huruf, ROT47 menggeser 47 karakter dalam rentang karakter ASCII yang dapat dicetak, termasuk angka dan simbol.
Berikut adalah hasil dekode dan jawabannya:
Answer:
``` You spin me right round baby right round (47 times) ```

Pertanyaan 8:```— . .-.. . -.-. — — — — ..- -. .. -.-. .- — .. — — -. . -. -.-. — — -.. .. -. — .```
Jika Anda memiliki pengalaman di bidang forensik, telekomunikasi, atau sering menonton film, Anda akan tahu ini adalah Kode Morse (titik dan garis).
Berikut adalah hasil dekode dari kode Morse Code yang Anda berikan:

*1.
``` - . .-.. . -.-. --- -- -- ..- -. .. -.-. .- - .. --- -. ```
TELECOMMUNICATION

*2.
``` . -. -.-. --- -.. .. -. --. ```
ENCODING
Answer:
``` telecommunication encoding ```

Pertanyaan 9: 85 110 112 97 99 107 32 116 104 105 115 32 66 67 68
Urutan angka ini bisa berupa desimal atau oktal. Setelah dicoba dengan basis 10, ini terbukti merupakan format desimal.
Berikut adalah hasil terjemahan kode Desimal ASCII yang Anda berikan:
Answer:
``` Unpack this BCD ```
Penjelasan:
Angka-angka tersebut mewakili karakter dalam tabel ASCII (American Standard Code for Information Interchange).
85 = U, 110 = n, 112 = p, 97 = a, 99 = c, 107 = k
32 = [spasi]
116 = t, 104 = h, 105 = i, 115 = s
32 = [spasi]
66 = B, 67 = C, 68 = D
Karena jawabannya menyarankan BCD (Binary Coded Decimal), ini adalah jenis encoding baru. 


Question 10: 

```
LS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0=
```
Pada awalnya, Anda akan melihat pertanyaan ini cukup membingungkan dengan banyak karakter `LS0` dan `Li0t`.

Namun perhatikan tanda sama dengan di akhir, itu adalah base64.

Dekode base64 tersebut, kita mendapatkan kode Morse.

```morse

----- .---- .---- ----- ----- .---- .---- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- .---- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- .---- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- ----- .---- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- .---- .---- ----- ----- .---- ----- .----

```

Setelah dikonversi ke kode Morse, kita memiliki:

```
011001100110010100100000011000000101111101100000001000000110000001100000011001010010000001100010011010000010000001100000011000000110010000100000011000100110000100100000011000000101111101101000001000000110100001100110001000000110000001011111011001100010000001100000010111110110000000100000011000100110000100100000011000000110000001100101001000000110000001011111011000110010000001100000010111110110010000100000011000000110000001100100001000000110001001100001001000000110100001100110001000000110001001100001001000000110100001100111001000000110000001011111011001000010000001100000011000000110010100100000011000100110000100100000011000000110000001100101001000000110000001100000011000110010000001100000010111110110010000100000011010000110100000100000011000000101111101100110001000000110000001011111011001000010000001100000010111110110000000100000011000000110000001100011001000000110001101100101001000000110001101100101001000000110001101100101
```

dekode biner:

```
fe `_` ``e bh ``d ba `_h hf `_f `_` ba ``e `_c `_d ``d ba hf ba hg `_d ``e ba ``e ``c `_d hh `_f `_d `_` ``c ce ce ce
```

Hmm, pada langkah ini saya rasa petunjuk di pertanyaan kita sebelumnya adalah rot47.

```
76 101 116 39 115 32 109 97 107 101 32 116 104 105 115 32 97 32 98 105 116 32 116 114 105 99 107 105 101 114 46 46 46
```

Kemudian, ubah dari desimal,`Let's make this a bit trickier...`

<img width="1364" height="693" alt="image" src="https://github.com/user-attachments/assets/2650e3a6-b5ad-4faf-961d-63458ad3150f" />

# ***Spectrograms — Task 2***

Berikut adalah panduan singkat untuk menyelesaikan tugas tersebut:
Unduh File: Ambil file audio .wav yang disediakan di Task 2.
Gunakan Alat Analisis:
Sonic Visualiser: Buka file tersebut, lalu pilih menu Layer > Add Spectrogram.
Audacity: Buka file, klik tanda panah di samping nama trek, dan ubah tampilan dari Waveform menjadi Spectrogram.
Online: Anda juga bisa menggunakan alat berbasis web seperti Aperi'Solve atau fitur analisis spektral di dCode.
Temukan Flag: Setelah tampilan spektrogram muncul, teks atau "flag" akan terlihat secara visual di antara frekuensi suara tersebut

<img width="1366" height="731" alt="image" src="https://github.com/user-attachments/assets/8e1b02f9-a543-4b60-9d3f-fbf3afab1ceb" />
<img width="1361" height="699" alt="image" src="https://github.com/user-attachments/assets/688e1b95-5c75-464c-b5e8-ed24bc346137" />

# ***Steganography — Task 3***
ikuti langkah-langkah berikut:
Unduh Gambar: Simpan gambar yang disediakan dalam tugas tersebut ke komputer Anda.
Gunakan Steghide: Karena petunjuk menyebutkan "Steganographic Decoder", Anda bisa menggunakan alat baris perintah steghide.
Jalankan perintah: steghide extract -sf stegosteg.jpg.
Saat diminta passphrase, cukup tekan Enter (kosongkan) karena file tersebut tidak diproteksi kata sandi.
Baca Hasil Ekstraksi: Perintah di atas akan mengekstrak sebuah file teks (biasanya bernama steganopayload2248.txt). Buka file tersebut untuk melihat flag/jawabannya

Alternatifnya, Anda juga bisa menggunakan layanan web seperti Aperi'Solve dengan mengunggah gambar tersebut untuk melihat pesan yang tersembunyi secara otomatis.

```url
https://www.aperisolve.com/e1bcd066f9d37f46622cb63cf5600a48
```
<img width="327" height="621" alt="image" src="https://github.com/user-attachments/assets/a3f932e1-c047-4112-8235-9afb18341cb6" />

<img width="1337" height="685" alt="image" src="https://github.com/user-attachments/assets/6fa07321-3e56-4040-964e-a2dc64f4c255" />

<img width="1361" height="692" alt="image" src="https://github.com/user-attachments/assets/f45102c2-d694-4801-bc11-99976a0a7351" />

# ***Security through obscurity — Task 4***

Gunakan Perintah binwalk:
Alat ini sangat efektif untuk melihat apakah ada file lain yang "menempel" di balik gambar tersebut. Jalankan perintah:

┌──(kali㉿DESKTOP)-[~]

└─$ ```binwalk meme_1559010886025.jpg```

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
30            0x1E            TIFF image data, big-endian, offset of first image directory: 8
74407         0x122A7         RAR archive data, version 5.x
74478         0x122EE         PNG image, 147 x 37, 8-bit/color RGBA, non-interlaced
74629         0x12385         Zlib compressed data, default compression

┌──(kali㉿DESKTOP)-[~]

└─$ ```binwalk -e meme_1559010886025.jpg```

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
74407         0x122A7         RAR archive data, version 5.x
74629         0x12385         Zlib compressed data, default compression

┌──(kali㉿DESKTOP)-[~]

└─$ binwalk -e meme_1559010886025.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------

WARNING: Extractor.execute failed to run external extractor 'unrar e '%e'': [Errno 2] No such file or directory: 'unrar', 'unrar e '%e'' might not be installed correctly

WARNING: Extractor.execute failed to run external extractor 'unrar -x '%e'': [Errno 2] No such file or directory: 'unrar', 'unrar -x '%e'' might not be installed correctly
74407         0x122A7         RAR archive data, version 5.x
74629         0x12385         Zlib compressed data, default compression

WARNING: One or more files failed to extract: either no utility was found or it's unimplemented

┌──(kali㉿DESKTOP)-[~]

└─$ ```cd _meme_1559010886025.jpg.extracted```

┌──(kali㉿DESKTOP)-[~/_meme_1559010886025.jpg.extracted]

└─$ ```ls```
122A7.rar  12385  12385.zlib

┌──(kali㉿DESKTOP)-[~/_meme_1559010886025.jpg.extracted]

└─$ ```unrar e 122A7.rar```

UNRAR 7.20 freeware      Copyright (c) 1993-2026 Alexander Roshal

Extracting from 122A7.rar

Extracting  hackerchat.png                                            OK
All OK

```hackerchat.png```

┌──(kali㉿DESKTOP)-[~/_meme_1559010886025.jpg.extracted]

└─$ ```ls```
122A7.rar  12385  12385.zlib  hackerchat.png

Silakan masukkan jawaban tersebut. :```hackerchat.png```

Jika kamu diminta untuk mencari "isi" atau flag selanjutnya, kamu perlu memeriksa file tersebut. Karena formatnya adalah .png, kamu bisa mencoba melihat isinya dengan membuka gambar tersebut atau melakukan analisis steganografi lagi pada hackerchat.png menggunakan:
strings hackerchat.png
Atau unggah ke Aperi'Solve lagi.

<img width="1335" height="607" alt="image" src="https://github.com/user-attachments/assets/dcc255eb-21e8-46a3-ad44-b0642ad2e595" />

Exiftool

```
Bit Depth	8
Color Type	RGB with Alpha
Compression	Deflate/Inflate
Creation Time	Wed 15 May 2019 09:09:10 PM CDT
Directory	..
ExifTool Version Number	13.25
File Access Date/Time	2026:03:20 10:47:55+00:00
File Inode Change Date/Time	2026:03:20 10:47:52+00:00
File Modification Date/Time	2026:03:20 10:47:52+00:00
File Name	de4502de0ae70d4a95d0e304f1b24736.png
File Permissions	-rw-r--r--
File Size	5.6 kB
File Type	PNG
File Type Extension	png
Filter	Adaptive
Image Height	37
Image Size	147x37
Image Width	147
Interlace	Noninterlaced
MIME Type	image/png
Megapixels	0.005
Significant Bits	8 8 8 8
Software	gnome-screenshot
Warning	[minor] Trailer data after PNG IEND chunk
```
Binwalk
```
Scan Time:     2026-03-20 10:48:01
Target File:   /app/aperisolve/results/de4502de0ae70d4a95d0e304f1b24736/de4502de0ae70d4a95d0e304f1b24736.png
MD5 Checksum:  de4502de0ae70d4a95d0e304f1b24736
Signatures:    436
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
151           0x97            Zlib compressed data, default compression
Scan Time:     2026-03-20 10:48:01
Target File:   /app/aperisolve/results/de4502de0ae70d4a95d0e304f1b24736/9caf2a949d546ff339d5f63a69b288be/_de4502de0ae70d4a95d0e304f1b24736.png.extracted/97
MD5 Checksum:  f1190ee95afa155bc75f132176cbc779
Signatures:    436
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
```
Pngcheck
```
File: ../de4502de0ae70d4a95d0e304f1b24736.png (5562 bytes)
  chunk IHDR at offset 0x0000c, length 13
    147 x 37 image, 32-bit RGB+alpha, non-interlaced
  chunk sBIT at offset 0x00025, length 4
    red = 8 = 0x08, green = 8 = 0x08, blue = 8 = 0x08, alpha = 8 = 0x08
  chunk tEXt at offset 0x00035, length 25, keyword: Software
  chunk tEXt at offset 0x0005a, length 45, keyword: Creation Time
  chunk IDAT at offset 0x00093, length 5373
    zlib: deflated, 32K window, default compression
  chunk IEND at offset 0x0159c, length 0
  additional data after IEND chunk
ERRORS DETECTED in ../de4502de0ae70d4a95d0e304f1b24736.png
```
Pcrt
```
Correct PNG header
Correct IHDR CRC at offset 0x1D
IHDR chunk check complete at offset 0x8
Copied sBIT chunk (4 bytes)
IDAT chunk check complete at offset 0x8F
Correct IEND chunk
Found 22 bytes after IEND: b'"AHH_YOU_FOUND_ME!" '
IEND chunk check complete
```
Identify
```
Image: ../de4502de0ae70d4a95d0e304f1b24736.png
  Format: PNG (Portable Network Graphics)
  Geometry: 147x37
  Class: DirectClass
  Type: true color
  Depth: 8 bits-per-pixel component
  Channel Depths:
    Red:      8 bits
    Green:    8 bits
    Blue:     8 bits
    Opacity:  1 bits
  Channel Statistics:
    Red:
      Minimum:                     0.00 (0.0000)
      Maximum:                 65535.00 (1.0000)
      Mean:                    15009.91 (0.2290)
      Standard Deviation:      25264.60 (0.3855)
    Green:
      Minimum:                     0.00 (0.0000)
      Maximum:                 65535.00 (1.0000)
      Mean:                    25140.17 (0.3836)
      Standard Deviation:      27513.91 (0.4198)
    Blue:
      Minimum:                     0.00 (0.0000)
      Maximum:                 65535.00 (1.0000)
      Mean:                    23260.08 (0.3549)
      Standard Deviation:      25363.97 (0.3870)
    Opacity:
      Minimum:                     0.00 (0.0000)
      Maximum:                     0.00 (0.0000)
      Mean:                        0.00 (0.0000)
      Standard Deviation:          0.00 (0.0000)
  Filesize: 5.4Ki
  Interlace: No
  Orientation: Unknown
  Background Color: white
  Border Color: #DFDFDF00
  Matte Color: #BDBDBD00
  Page geometry: 147x37+0+0
  Compose: Over
  Dispose: Undefined
  Iterations: 0
  Compression: Zip
  Png:IHDR.color-type-orig: 6
  Png:IHDR.bit-depth-orig: 8
  Software: gnome-screenshot
  Creation Time: Wed 15 May 2019 09:09:10 PM CDT
  Signature: 05a314d393c87850160c0ebd8800d59ec6a783a6e4f0231b003d883f3179d48f
  Tainted: False
  Elapsed Time: 0m:0.001190s
  Pixels Per Second: 4.4Mi
```
<img width="529" height="247" alt="image" src="https://github.com/user-attachments/assets/89577f2f-405a-4575-9766-decfe8518506" />

<img width="1141" height="645" alt="image" src="https://github.com/user-attachments/assets/f24e6c92-c66a-490b-8330-e0386781b8a7" />

Download and get 'inside' the file. What is the first filename & extension?
```
hackerchat.png
```
Get inside the archive and inspect the file carefully. Find the hidden text.

``` 
AHH_YOU_FOUND_ME!
```


//-------------------------------------------------------

# [c4ptur3-th3-fl4g](https://tryhackme.com/room/c4ptur3th3fl4g)
Pertanyaan 1: `c4n y0u c4p7u23 7h3 f149?`
Ini disebut leet speak, di mana teks ditulis dengan ejaan yang dimodifikasi menggunakan angka.
Mengganti angka dengan huruf yang mirip secara visual:
4 = A
0 = O
7 = T
2 = R
3 = E
1 = I
Hasil translasi: "can you capture the flag?"
Hasilnya: ```can you capture the flag?```

Pertanyaan 2:
``` 01101100 01100101 01110100 01110011 00100000 01110100 01110010 01111001 00100000 01110011 01101111 01101101 01100101 00100000 01100010 01101001 01101110 01100001 01110010 01111001 00100000 01101111 01110101 01110100 00100001 ```
Apa arti dari rangkaian angka 1 dan 0 ini? Ini adalah biner, "bahasa komputer". Gunakan Binary Decoder untuk menerjemahkannya.
Kode biner yang kamu kirimkan itu kalau diterjemahkan artinya:
``` lets try some binary out ```

Pertanyaan 3: MJQXGZJTGIQGS4ZAON2XAZLSEBRW63LNN5XCA2LOEBBVIRRHOM======
Adanya tanda sama dengan (=) di akhir string menandakan ini adalah Base32 atau Base64. Dalam kasus ini, kita menggunakan dekoder Base32.
Kode tersebut dienkode menggunakan Base32. Jika didekode, hasilnya adalah:
``` let's try some base32 out ```

Pertanyaan 4:``` RWFjaCBCYXNlNjQgZGlnaXQgcmVwcmVzZW50cyBleGFjdGx5IDYgYml0cyBvZiBkYXRhLg== ```
Kode di bawah ini:
``` Ym5nZ3Z6cnZ6YXJnciBnYmJ5YmJncmU= ```
Petunjuk:
Decode dari Base64 terlebih dahulu.
Shift hasilnya menggunakan ROT13 (geser 13 huruf).
Dan yang satu ini dalam bentuk Base64. Anda bisa menggunakan alat di Base64Decode.org.

Pertanyaan 5: ``` 68 65 78 61 64 65 63 69 6d 61 6c 20 6f 72 20 62 61 73 65 31 36 3f ```
Keberadaan angka dan huruf yang tidak melebihi huruf 'f' mengarah pada format heksadesimal (Base16).
Decode Hexadecimal
Untuk memecahkan kode ini, Anda perlu mengubah setiap pasangan angka dan huruf menjadi karakter ASCII yang sesuai.
``` 68 65 78 61 64 65 63 69 6d 61 6c 20 6f 72 20 62 61 73 65 31 36 3f ```
Ketika dikonversi dari Hex ke teks, hasilnya adalah:
Answer:
``` hexadecimal or base16? ```

Pertanyaan 6: ``` Ebgngr zr 13 cynprf! ```
Dilihat dari jawabannya, bentuk karakternya sama dengan pertanyaannya. Ini memastikan bahwa ini adalah sandi pergeseran karakter tunggal, yaitu ROT13. ROT13 adalah sandi sederhana di mana setiap huruf "diputar" sebanyak 13 posisi dalam alfabet.
Adanya tanda sama dengan (=) di akhir string sering digunakan sebagai padding (pengisi) untuk memastikan panjang string Base32 atau Base64 valid, seperti yang kamu identifikasi.
Dalam kasus ini, ini adalah Base32, dan logikamu benar. Hasil dekodenya adalah:
Answer:
``` let's try some base32 out ```

Pertanyaan 7: ``` *@F DA:? >6 C:89E C@F?5 323J C:89E C@F?5 Wcf E:>6DX ```
Ini mirip dengan sebelumnya, namun menggunakan sandi ROT47. Alih-alih hanya huruf A-Z, sandi ini menggunakan hampir semua karakter dalam tabel kode ASCII.
*@F DA:? >6 C:89E C@F?5 323J C:89E C@F?5 Wcf E:>6DX, adalah kode yang dienkripsi menggunakan ROT47.
Tidak seperti ROT13 yang hanya menggeser huruf, ROT47 menggeser 47 karakter dalam rentang karakter ASCII yang dapat dicetak, termasuk angka dan simbol.
Berikut adalah hasil dekode dan jawabannya:
Answer:
``` You spin me right round baby right round (47 times) ```

Pertanyaan 8:```— . .-.. . -.-. — — — — ..- -. .. -.-. .- — .. — — -. . -. -.-. — — -.. .. -. — .```
Jika Anda memiliki pengalaman di bidang forensik, telekomunikasi, atau sering menonton film, Anda akan tahu ini adalah Kode Morse (titik dan garis).
Berikut adalah hasil dekode dari kode Morse Code yang Anda berikan:

*1.
``` - . .-.. . -.-. --- -- -- ..- -. .. -.-. .- - .. --- -. ```
TELECOMMUNICATION

*2.
``` . -. -.-. --- -.. .. -. --. ```
ENCODING
Answer:
``` telecommunication encoding ```

Pertanyaan 9: 85 110 112 97 99 107 32 116 104 105 115 32 66 67 68
Urutan angka ini bisa berupa desimal atau oktal. Setelah dicoba dengan basis 10, ini terbukti merupakan format desimal.
Berikut adalah hasil terjemahan kode Desimal ASCII yang Anda berikan:
Answer:
``` Unpack this BCD ```
Penjelasan:
Angka-angka tersebut mewakili karakter dalam tabel ASCII (American Standard Code for Information Interchange).
85 = U, 110 = n, 112 = p, 97 = a, 99 = c, 107 = k
32 = [spasi]
116 = t, 104 = h, 105 = i, 115 = s
32 = [spasi]
66 = B, 67 = C, 68 = D
Karena jawabannya menyarankan BCD (Binary Coded Decimal), ini adalah jenis encoding baru. 


Question 10: 

```
LS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0=
```
Pada awalnya, Anda akan melihat pertanyaan ini cukup membingungkan dengan banyak karakter `LS0` dan `Li0t`.

Namun perhatikan tanda sama dengan di akhir, itu adalah base64.

Dekode base64 tersebut, kita mendapatkan kode Morse.
```
----- .---- .---- ----- ----- .---- .---- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- .---- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- .---- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- ----- .---- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- .---- .---- ----- ----- .---- ----- .----
```

Setelah dikonversi ke kode Morse, kita memiliki:

```
011001100110010100100000011000000101111101100000001000000110000001100000011001010010000001100010011010000010000001100000011000000110010000100000011000100110000100100000011000000101111101101000001000000110100001100110001000000110000001011111011001100010000001100000010111110110000000100000011000100110000100100000011000000110000001100101001000000110000001011111011000110010000001100000010111110110010000100000011000000110000001100100001000000110001001100001001000000110100001100110001000000110001001100001001000000110100001100111001000000110000001011111011001000010000001100000011000000110010100100000011000100110000100100000011000000110000001100101001000000110000001100000011000110010000001100000010111110110010000100000011010000110100000100000011000000101111101100110001000000110000001011111011001000010000001100000010111110110000000100000011000000110000001100011001000000110001101100101001000000110001101100101001000000110001101100101
```

dekode biner:

```
fe `_` ``e bh ``d ba `_h hf `_f `_` ba ``e `_c `_d ``d ba hf ba hg `_d ``e ba ``e ``c `_d hh `_f `_d `_` ``c ce ce ce
```

Hmm, pada langkah ini saya rasa petunjuk di pertanyaan kita sebelumnya adalah rot47.

```
76 101 116 39 115 32 109 97 107 101 32 116 104 105 115 32 97 32 98 105 116 32 116 114 105 99 107 105 101 114 46 46 46
```

Kemudian, ubah dari desimal,`Let's make this a bit trickier...`

Answer:

## Spectrograms
Spektrogram adalah representasi visual dari spektrum frekuensi suatu sinyal saat berubah seiring waktu.

Ketika diterapkan pada sinyal audio, spektrogram kadang-kadang disebut sonograf, sidik suara, atau voicegram.

Ketika data direpresentasikan dalam plot 3D, plot tersebut dapat disebut air terjun (waterfall).

Menggunakan Audacity, saya mendapatkan jawabannya.

## Steganography

Steganografi adalah praktik menyembunyikan file, pesan, gambar, atau video di dalam file, pesan, gambar, atau video lain.

atau Anda bisa menggunakan `steghide –extract -sf stegosteg.jpg`

## Security through obscurity

Pertanyaannya mengatakan untuk mengunduh file dan memeriksa ekstensinya, jadi itu bukan gambar biasa.

Saya sudah mencoba dengan perintah strings atau membukanya dengan notepad.

Sangat jelas bahwa ada 2 flag dalam tampilan

atau Anda bisa menggunakan `binwalk –extract meme.jpg`

Prinsipnya dapat dipahami secara sederhana sebagai file terkompresi yang berisi konten gambar dan file lain.

Tentu saja, informasi yang dapat dibaca dalam teks biasa akan ditampilkan saat menggunakan string.
