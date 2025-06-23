# Laporan Proyek Machine Learning - Naia Az - Zahra MC132D5X1884
## Prediksi Kualitas Tiudr Berdasarkan Faktor Gaya Hiduo

## Domain Proyek
### Latar Belakang
Kualitas tidur adalah pilar utama kesehatan fisik dan mental yang seringkali terabaikan di tengah gaya hidup modern yang serba cepat. Kurang tidur atau kualitas tidur yang buruk telah dikaitkan dengan berbagai masalah kesehatan serius, termasuk penyakit jantung, diabetes tipe 2, obesitas, gangguan suasana hati, dan penurunan fungsi kognitif [1], [2]. Dengan semakin berkembangnya teknologi wearable dan kesadaran akan pentingnya self-care, individu memiliki akses data yang lebih besar tentang pola tidur dan gaya hidup mereka.

Namun, banyak orang kesulitan mengidentifikasi faktor spesifik dari gaya hidup mereka yang paling berdampak pada kualitas tidur. Minimnya pemahaman ini menghambat upaya personalisasi untuk meningkatkan kualitas tidur. Oleh karena itu, diperlukan sebuah sistem yang dapat menganalisis data gaya hidup dan memprediksi kualitas tidur.


### Referensi 
[1] Walker, M. P. (2017). Why We Sleep: Unlocking the Power of Sleep and Dreams. Scribner.
[2] National Sleep Foundation. (2020). Sleep Health Index. Diakses dari https://www.sleepfoundation.org/ (Perhatikan: tautan ini adalah contoh umum dan mungkin tidak mengarah langsung ke "Sleep Health Index" tertentu, perlu dicari referensi spesifik).

## Business Understanding


### Problem Statements
- Kesulitan Individu dalam Mengidentifikasi Kualitas Tidur Mereka Sendiri.
  Banyak individu tidak menyadari bahwa mereka memiliki kualitas tidur yang buruk atau berada pada risiko tinggi mengalami masalah tidur. Gejala-gejala seperti kelelahan kronis atau penurunan konsentrasi seringkali dianggap normal, padahal dapat menjadi indikator kualitas tidur yang rendah.

- Kurangnya Pemahaman tentang Dampak Faktor Gaya Hidup Terhadap Kualitas Tidur.
  Meskipun banyak yang mengakui pentingnya tidur, tidak semua individu memahami bagaimana kebiasaan sehari-hari mereka (misalnya, tingkat aktivitas, stres, pola makan) secara langsung memengaruhi kualitas tidur mereka. Hal ini menghambat upaya pencegahan dan perbaikan kualitas tidur.

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Membangun model klasifikasi yang mampu memprediksi kualitas tidur seseorang ke dalam kategori "Baik" atau "Buruk" berdasarkan faktor gaya hidup.
  
  Model ini akan membantu individu mendapatkan gambaran awal tentang kualitas tidur mereka tanpa perlu intervensi medis yang kompleks.
- Mengidentifikasi faktor-faktor gaya hidup dominan yang paling berpengaruh terhadap kualitas tidur.

  Dengan memahami faktor-faktor kunci ini, individu dan tenaga kesehatan dapat fokus pada area yang paling relevan untuk perbaikan kualitas tidur.

## Data Understanding
Dataset yang digunakan dalam proyek ini adalah Sleep Health and Lifestyle Dataset yang tersedia di Kaggle. Dataset ini berisikan informasi mengenai berbagai faktor gaya hidup dan kesehatan yang relevan dengan kualitas tidur.
[Sumber Datase -- Kaggle ] : (https://www.kaggle.com/datasets/uom190346a/sleep-health-and-lifestyle-dataset).

### Variabel-variabel pada dataset adalah sebagai berikut:
- Variabel-variabel pada Sleep Health and Lifestyle Dataset adalah sebagai berikut:
- Person ID (int64): ID unik untuk setiap individu. Ini adalah fitur identifikasi dan tidak akan digunakan dalam pemodelan.
- Gender (object): Jenis kelamin individu (misalnya, Male, Female). Ini adalah fitur kategorikal.
- Age (int64): Usia individu dalam tahun. Ini adalah fitur numerik.
- Occupation (object): Profesi atau pekerjaan individu (misalnya, Software Engineer, Doctor, Teacher). Ini adalah fitur kategorikal dengan banyak kelas.
- Sleep Duration (float64): Durasi tidur dalam jam per malam. Ini adalah fitur numerik.
- Quality of Sleep (int64): Penilaian subjektif terhadap kualitas tidur individu, dengan skala dari 1 hingga 10. Nilai yang lebih tinggi menunjukkan kualitas tidur yang lebih baik.
- Physical Activity Level (int64): Tingkat aktivitas fisik harian individu, diukur dalam menit per hari.
- Stress Level (int64): Penilaian subjektif terhadap tingkat stres yang dialami individu, dengan skala dari 1 hingga 10. Nilai yang lebih tinggi menunjukkan tingkat stres yang lebih tinggi.
- BMI Category (object): Kategori Indeks Massa Tubuh (BMI) individu, yang mengklasifikasikan status berat badan mereka.
- Blood Pressure (object): Pengukuran tekanan darah individu, yang ditunjukkan sebagai tekanan sistolik di atas tekanan diastolik (misalnya, 120/80). Ini adalah fitur kategorikal yang merupakan string dari dua angka.
- Heart Rate (int64): Denyut jantung istirahat individu, diukur dalam denyut per menit (bpm - beats per minute). Ini adalah fitur numerik.
- Daily Steps (int64): Jumlah langkah harian yang diambil individu. Ini adalah fitur numerik.
- Sleep Disorder (object): Jenis gangguan tidur yang mungkin dimiliki individu ( Insomnia, Sleep Apnea, None). Ini adalah fitur kategorikal.


## Data Preparation
Tahap persiapan data adalah krusial untuk memastikan data siap untuk pemodelan machine learning. Teknik-teknik yang diterapkan di sini mengikuti urutan logis untuk membersihkan, mengubah, dan menyiapkan fitur.

- Distribusi Kualitas Tidur
![Distribusi Kualitas Tidur](images/dis_kualitas_tidur.png)
- Penjelasan : Visualisasi ini menunjukkan sebaran frekuensi setiap skor dari 'Quality of Sleep'. Pada distribusi terdapat ambang batas nilai individu yaitu berada pada rentang 4 - 9 jam waktu tidur pada masing-masing individu.

- Penangan Kolom 'Person ID'
  Mendrop/menghilangkan kolom 'person ID' dengan menggunakan .dropna()
- Penanganan Nilai Hilang pada 'Sleep Disorder'
  pada kolom 'Sleep Disorder' terdapat 3 nilai yaitu (NaN, Insomnia, dan Sleep Anea). Nilai NaN akan diisi dengan kategori (No Disorder).
- 

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahap pemodelan melibatkan pemilihan, pelatihan, dan pengoptimalan algoritma machine learning untuk memprediksi kualitas tidur. Dalam proyek ini, kami akan menggunakan dua algoritma klasifikasi utama untuk perbandingan: Random Forest Classifier dan Decision Tree Classifier, serta K-Nearest Neighbors sebagai pembanding tambahan.

**Pemilihan Algoritma**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.

## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

