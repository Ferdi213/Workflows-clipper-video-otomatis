>>>>jika potong video di satu baris pakai workflows potong-video.yml<<<<



>>>>
>>>>,jika link video lebih satu pakai workflows multi-video.yml<<<<<<
>>>>


>>>>>JIKA PAKAI MULTI VIDEO<<<<<
Kalau **URL dipisahkan koma**, ada dua pilihan logika.

### Pilihan 1 (yang sekarang di workflow kamu)

Semua video **digabung dulu**, baru dipotong.

Contoh Sheet:

| URL_Video        | Timestamps        |
| ---------------- | ----------------- |
| `url1,url2,url3` | `1-5,18-25,40-50` |

Misal:

* Video1 = 10 detik
* Video2 = 20 detik
* Video3 = 15 detik

Maka timeline menjadi:

```
Video1 : 0 - 10
Video2 : 10 - 30
Video3 : 30 - 45
```

Kalau ingin:

* Video1 detik 1-5
* Video2 detik 8-15
* Video3 detik 10-15

Isi Sheet:

```
1-5,18-25,40-45
```

Karena harus menghitung akumulasi durasi.

---

## Pilihan 2 (yang lebih enak)

Timestamp dibuat **per video**, tidak perlu menghitung total durasi.

Contoh:

```
URL_Video
url1,url2,url3

Timestamps
1-5|8-15|10-15
```

Artinya:

* `url1` → potong 1-5
* `url2` → potong 8-15
* `url3` → potong 10-15

Workflow akan:

1. Download url1 → potong 1-5
2. Download url2 → potong 8-15
3. Download url3 → potong 10-15
4. Baru hasil potongannya digabung menjadi .video.mp4

Keuntungannya:

* Tidak perlu menghitung durasi gabungan.
* Kalau ganti urutan video tidak perlu mengubah timestamp lain.
* Jauh lebih mudah diisi di Google Sheet.

Contoh yang lebih kompleks:

Di kolom SHEET 


URL_Video
url1,url2,url3

Timestamps
1-5,8-10|15-20|2-8,10-12


Artinya:

* Video1 → ambil 1-5 lalu 8-10
* Video2 → ambil 15-20
* Video3 → ambil 2-8 lalu 10-12

Lalu semua hasil potongan itu digabung menjadi satu video akhir.

**Saya lebih menyarankan cara kedua** karena jauh lebih praktis untuk otomatisasi n8n dan Google Sheets. Tidak perlu lagi menghitung offset waktu setiap kali jumlah atau durasi video berubah.

