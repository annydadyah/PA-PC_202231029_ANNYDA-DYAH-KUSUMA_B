# PA-PC_202231029_ANNYDA-DYAH-KUSUMA_B
<br>
Nama  : Annyda Dyah Kusuma <br>
NIM   : 202231029 <br>
Kelas : B <br>
Ketentuan Project : Geommterix Citra <br>

---

## Tahapan dalam geometrix citra
Dalam mengerjakan project, saya melakukan beberapa hal :
- Mempersiapkan citra
- Melakukan rotasi gambar sebesar 45 derajat
- Meresize gambar
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
rows,cols=img.shape[:2]
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kode di atas membaca gambar menggunakan fungsi cv.imread(). Fungsi ini mengambil file gambar 'foto_diri.jpeg' 
dan mengubahnya menjadi array NumPy tiga dimensi. Array ini merepresentasikan gambar dalam format BGR (Blue, Green, Red), 
yang merupakan standar OpenCV. Setiap piksel dalam gambar direpresentasikan oleh tiga nilai intensitas, masing-masing 
untuk kanal biru, hijau, dan merah, dengan rentang nilai 0-255 untuk gambar 8-bit. <br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Setelah gambar dibaca, langkah selanjutnya adalah mengonversi ruang warna dari BGR ke RGB menggunakan fungsi cv.cvtColor(). 
Konversi ini penting karena meskipun OpenCV menggunakan format BGR, matplotlib - yang digunakan untuk menampilkan gambar - 
mengharapkan format RGB. Proses konversi ini pada dasarnya menukar posisi kanal biru dan merah dalam array gambar, 
memastikan bahwa warna ditampilkan dengan benar saat gambar divisualisasikan. <br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Baris kode `rows,cols=img.shape[:2]` digunakan untuk mendapatkan jumlah baris (`rows`) dan kolom (`cols`) dari sebuah gambar 
(`img`). Perintah ini mengambil dimensi pertama dan kedua dari atribut `shape` objek gambar, yang mewakili tinggi dan lebar 
gambar tersebut. Dimensi ketiga (biasanya jumlah saluran warna) diabaikan karena hanya dimensi ruang yang dibutuhkan dalam konteks ini. <br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;


**Melakukan Rotasi Gambar** <br>
```
M=cv.getRotationMatrix2D(((cols-1)/2.0,(rows-1)/2.0),45,1)
rot=cv.warpAffine(img,M,(cols,rows))
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Rotasi gambar melibatkan beberapa langkah. Pertama, titik pusat rotasi dihitung sebagai titik tengah gambar menggunakan rumus 
((cols-1)/2.0, (rows-1)/2.0). Kemudian, matriks rotasi 2D dibuat menggunakan cv.getRotationMatrix2D(), dengan sudut rotasi 45 derajat. 
Matriks ini mendefinisikan bagaimana setiap piksel akan dipindahkan untuk menciptakan efek rotasi. Akhirnya, rotasi diterapkan pada 
gambar menggunakan cv.warpAffine(), yang mengaplikasikan transformasi affine berdasarkan matriks rotasi yang telah dibuat. Proses ini 
menghasilkan gambar baru yang telah diputar sebesar 45 derajat searah jarum jam. <br>

Untuk menampilkan hasil rotasinya dan membandingkan dengan gambar asli bisa menggunakan plot.
```
fig, axs = plt.subplots(1,2, figsize=(15,5))
axs[0].imshow(img)
axs[0].set_title('Gambar Asli')
axs[1].imshow(rot)
axs[1].set_title('Rotated Image')
```
Output :
![Merotasi Gambar](images/rotated.png)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

**Meresize Gambar** <br>
```
height, width = img.shape[:2]
res = cv.resize(img,(1*width, 2*height), interpolation = cv.INTER_CUBIC)
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Baris kode `height,width=img.shape[:2]` digunakan untuk mendapatkan jumlah baris (`height`) dan kolom (`width`) dari sebuah gambar 
(`img`). Perintah ini mengambil dimensi pertama dan kedua dari atribut `shape` objek gambar, yang mewakili tinggi dan lebar 
gambar tersebut. Dimensi ketiga (biasanya jumlah saluran warna) diabaikan karena hanya dimensi ruang yang dibutuhkan dalam konteks ini. <br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Proses merisize dilakukan menggunakan fungsi cv.resize(). Dalam kode ini, gambar diperbesar menjadi dua kali ukuran aslinya, 
baik lebar maupun tingginya. Metode interpolasi yang digunakan adalah interpolasi kubik (cv.INTER_CUBIC), yang melibatkan 16 
piksel terdekat untuk menghitung nilai setiap piksel baru. Metode ini menghasilkan hasil yang lebih halus dibandingkan dengan 
metode interpolasi yang lebih sederhana seperti nearest neighbor atau bilinear, terutama untuk pembesaran gambar. 
Berdasarkan kodingan tersebut maka, gambar diperbesar 2 kali lipat untuk tingginya dan tetap menggunakan lebar yang sebelumnya (1*width), hal ini dilakukan dengan
menggunakan cv.resize() dengan interpolasi cubic. <br>

Untuk menampilkan hasilnya dan membandingkan dengan gambar asli bisa menggunakan plot.
```
fig, axs = plt.subplots(1,2, figsize=(15,5))
axs[0].imshow(img)
axs[0].set_title('Gambar Asli')
axs[1].imshow(res)
axs[1].set_title('Resize Image')
```
Output :

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

**Memotong Gambar** <br>
```
crop = img[100:250, 280:430]
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Operasi cropping dilakukan menggunakan teknik slicing array NumPy. Potongan gambar diambil dengan menentukan rentang indeks untuk 
baris dan kolom array gambar: img[100:250, 280:430]. Ini berarti mengambil bagian gambar dari baris 100 hingga 249 dan kolom 280 
hingga 429. Proses ini efektif mengekstrak area persegi panjang spesifik dari gambar asli, memungkinkan fokus pada region of interest 
tertentu untuk analisis atau pemrosesan lebih lanjut. <br>

Untuk menampilkan hasilnya dan membandingkan dengan gambar asli bisa menggunakan plot. <br>
```
fig, axs = plt.subplots(1,2, figsize=(15,5))
axs[0].imshow(img)
axs[0].set_title('Gambar Asli')
axs[1].imshow(crop)
axs[1].set_title('Cropped Image')
```
Output :

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

**Membalikkan Gambar** <br>
```
flip = cv.flip(img, 1)
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Pembalikan gambar dilakukan menggunakan fungsi cv.flip(). Dengan parameter 1, fungsi ini membalik gambar secara horizontal, 
yang berarti menukar posisi piksel dari kiri ke kanan. Proses ini menciptakan efek cermin pada gambar, di mana sisi kiri gambar 
menjadi sisi kanan dan sebaliknya. Sedangkan jika ingin membalikkan secara vertikal, yang mana gambar awalnya menghadap bawah menjadi menghadap atas 
maka parameter yang diisikan adalah 0. <br>

Untuk menampilkan hasilnya dan membandingkan dengan gambar asli bisa menggunakan plot. <br>
```
fig, axs = plt.subplots(1,2, figsize=(15,5))
axs[0].imshow(img)
axs[0].set_title('Gambar Asli')
axs[1].imshow(flip)
axs[1].set_title('Flipped Image')
```
Output :

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

**Translasi Gambar** <br>
```
M = np.float32([[1,0,100],[0,1,100]])
trans=cv.warpAffine(img,M,(cols,rows))
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Translasi gambar melibatkan pergeseran posisi setiap piksel dalam gambar. Proses dimulai dengan membuat matriks translasi menggunakan 
np.float32([[1,0,100],[0,1,100]]). Matriks ini mendefinisikan pergeseran 100 piksel ke kanan dan 100 piksel ke bawah. Kemudian, 
translasi diterapkan menggunakan cv.warpAffine(), yang mengaplikasikan transformasi affine berdasarkan matriks yang telah dibuat. 
Hasilnya adalah gambar yang telah digeser posisinya dalam bidang dua dimensi.

Untuk menampilkan hasilnya dan membandingkan dengan gambar asli bisa menggunakan plot. <br>
```
fig, axs = plt.subplots(1,2, figsize=(15,5))
axs[0].imshow(img)
axs[0].set_title('Gambar Asli')
axs[1].imshow(trans)
axs[1].set_title('Translated Image')
```
Output :


**Menampilkan Gambar Keseluruhan**
```
fig, axs = plt.subplots(2, 3, figsize=(15, 10))

axs[0, 0].imshow(img)
axs[0, 0].set_title('Gambar asli')

axs[0, 1].imshow(rot)
axs[0, 1].set_title('Rotation Image')

axs[0, 2].imshow(res)
axs[0, 2].set_title('Resized Image')

axs[1, 0].imshow(crop)
axs[1, 0].set_title('Cropped Image')

axs[1, 1].imshow(flip)
axs[1, 1].set_title('Flipped Image')

axs[1, 2].imshow(trans)
axs[1, 2].set_title('Translated Imgae')

plt.show()
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tahap akhir melibatkan visualisasi semua hasil operasi pengolahan citra menggunakan matplotlib. Sebuah figure dengan 
enam subplot dibuat, masing-masing menampilkan gambar asli dan hasil dari setiap operasi pengolahan (rotated, rezised, 
cropped, flipped, dan translated). Pengaturan ini memungkinkan perbandingan visual yang mudah antara gambar asli dan 
berbagai hasil transformasi. Setiap subplot diberi judul yang menjelaskan operasi yang dilakukan, memberikan representasi 
visual yang komprehensif dari seluruh proses pengolahan citra yang telah dilakukan.

Output :

---
## Teori yang mendukung :
Dalam proses pengerjaan, berikut adalah beberapa teori yang mendukung dalam project :
1. Representasi Citra Digital
   
3. Ruang Warna
