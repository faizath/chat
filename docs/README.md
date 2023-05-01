# Offden Chat Frontend Testing

[https://app.offden.chat](https://app.offden.chat)

*<i>Back-end dari aplikasi belum dideploy. Anda baru dapat mencoba front-end dari aplikasi.</i>

## Memulai Percakapan
Gunakan ID kontak berikut pada pencarian kontak untuk memulai percakapan.

- 9933a091 (Alice)
- 94e8bf54 (Bob)
- abecab71 (Charlie)
- 9b6a9a4d (Eve)

## Command-command Deniable Encryption
Command untuk deniable encryption diketik pada fitur pencarian kontak (tombol tanda panah di bagian kiri atas).


1. init<br>
   Membuat partisi baru jika sebelumnya belum pernah membuat partisi

2. enter<br>
   Toggle mode password pada input. Setelah menjadi mode password, input password untuk memasuki partisi yang sudah pernah dibuat.

3. add<br>
   Menambah partisi baru jika sebelumnya sudah pernah membuat partisi. Ketik password baru dan masukkan semua password partisi yang sudah pernah dibuat sebelumnya, jika tidak, partisi akan di-overwrite dan data partisi tidak dapat diakses kembali.

## Penjelasan Teknis Deniable Encryption

[![Advanced Encryption Standard](https://raw.githubusercontent.com/faizath/chat/docs/docs/AES.png)](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)

[![Deniable Encryption](https://raw.githubusercontent.com/faizath/chat/docs/docs/Screenshot%20(37).png)](https://en.wikipedia.org/wiki/Deniable_encryption)

Misal baris 1 itu ciphertext, baris 2 itu index dari karakter ciphertext diatasnya, dan sebuah partisi memiliki 8 karakter. Terdapat sebuah partisi pada index 5-12 (9dab6218). Sisa katrakter diluar partisi tersebut adalah karakter random.

Pada percobaan dekripsi, program akan mencoba mendekripsi setiap 8 karakter yang mungkin dari index terendah.

1-8 (9fb79dab)<br>
2-9 (fb79dab6)<br>
3-10 (b79dab62)<br>
4-11 (79dab621)<br>
5-12 (9dab6218)<br>

Pada index 1-8, 2-9, 3-10, dan 4-11 dekripsi gagal karena karakter tersebut bukan partisi, lalu lanjut mendekripsi index selanjutnya.

Pada index 5-12 dekripsi berhasil, lalu partisi dibuka.

Ciphertext dapat memuat lebih dari satu partisi dengan stringnya yang digabung dengan karakter heksadesimal random untuk menambah deniability.
