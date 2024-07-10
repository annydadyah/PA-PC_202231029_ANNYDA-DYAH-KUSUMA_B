# PA-PC_202231029_ANNYDA-DYAH-KUSUMA_B
<br>
Nama  : Annyda Dyah Kusuma <br>
NIM   : 202231029 <br>
Kelas : B <br>
Ketentuan Project : Geommterix Citra <br>

---

## Tahapan dalam geometrix citra
Dalam mengerjakan project, saya melakukan beberapa hal :
- Membaca dan menampilkan gambar asli
- Melakukan rotasi gambar sebesar 45 derajat
- Mengubah ukuran gambar menjadi 2 kali lebih besar
- Memotong (crop) sebagian gambar
- Membalik (flip) gambar secara horizontal
- Melakukan translasi gambar

---
Berikut adalah penjelasan lebih rinci terkait tahapan-tahapannya <br>
**Persiapan Citra** <br>
```
img = cv.imread('foto_diri.jpeg')
img.shape
img = cv.cvtColor(img, cv.COLOR_BGR2RGB)
```
<br>
Kode di atas membaca gambar menggunakan fungsi cv.imread(). Fungsi ini mengambil file gambar 'foto_diri.jpeg' dan mengubahnya menjadi array NumPy tiga dimensi. Array ini merepresentasikan gambar dalam format BGR (Blue, Green, Red), yang merupakan standar OpenCV. Setiap piksel dalam gambar direpresentasikan oleh tiga nilai intensitas, masing-masing untuk kanal biru, hijau, dan merah, dengan rentang nilai 0-255 untuk gambar 8-bit.
---
## Teori yang mendukung :
Dalam proses pengerjaan, berikut adalah beberapa teori yang mendukung dalam project :
1. Representasi Citra Digital
   
3. Ruang Warna
