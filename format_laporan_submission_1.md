# Laporan Proyek Machine Learning - Arif Maulana Insaf

## Domain Proyek : Destinasi Wisata

wisata di indonesia sangat indah dan beragam, dan dengan keberagamannya hampir tidak ada alasan dunia untuk tidak mengenali wisata di indonesia. dikutip dari [UNESCO](https://whc.unesco.org/en/statesparties/id) tercatat 10 tempat di indonesia yang telah di akui dunia seperti raja ampat, pulau komodo dan masih banyak lain. akan tetapi itu hanya sebagian kecil tempat wisata di indonesia.

melalui analsis ini, diharapkan dapat membantu lokasi tempat yang belum dikenal wisatawan lain untuk mengunjugi tempat-tempat tersebut
**Rubrik/Kriteria Tambahan (Opsional)**:
- melalui analsis pengelompokan ini, diharapkan dapat membantu lokasi tempat yang belum dikenal wisatawan lain untuk mengunjugi tempat-tempat tersebut
- [referensi](https://ejournal.stipram.ac.id/index.php/kepariwisataan/article/view/209)

## Business Understanding

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- bagaimana cara tempat wisata populer di indonesia berdasarkan data rating dan jumlah review
- bagaimana cara memanfaatkan data kategorikal (kategori dan provinsi) dalam membangun model klasifikasi popularitas

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengembangkan model klasifikasi untuk memprediksi apakah sebuah tempat wisata populer atau tidak
- menggunakan informasi kategori dan provinsi untuk memperkaya fitur input bagi model prediktif


### Solution statements
Untuk mencapai tujuan mengembangkan model klasifikasi popularitas tempat wisata dan memanfaatkan fitur kategori serta provinsi, beberapa pendekatan solusi yang dapat diterapkan adalah sebagai berikut:
1. Menerapkan dan Membandingkan Berbagai Algoritma Klasifikasi
Menggunakan lebih dari satu algoritma klasifikasi untuk membangun model prediksi yang akurat terhadap status popularitas tempat wisata. Beberapa algoritma yang digunakan antara lain:
- Decision Tree
- Random Forest
- Logistic Regression
- Support Vector Machine (SVM)
- K-Nearest Neighbors (KNN)
2. Feature Engineering dan Pemanfaatan Data Kategorikal
Melakukan encoding pada fitur kategorikal seperti:
- Kategori tempat wisata (e.g., pantai, taman, museum)
- Provinsi (e.g., Bali, Jawa Barat)
Beberapa teknik yang digunakan:
- One-Hot Encoding atau Target Encoding untuk mengubah data kategorikal menjadi fitur numerik yang bisa diproses oleh model.
- Penggabungan data rating dan jumlah review sebagai fitur numerik tambahan.
3. Hyperparameter Tuning pada Model Terbaik
Melakukan optimasi hyperparameter pada model dengan performa terbaik (misalnya Random Forest atau Decision Tree) menggunakan:
- Grid Search CV atau Randomized Search CV
Parameter yang bisa dioptimalkan misalnya:
- max_depth, n_estimators, min_samples_split (untuk Random Forest dan Decision Tree)
- C dan kernel (untuk SVM)

## Data Understanding

saya menggunakan teknik scraping untuk mendapatkan dataset tersebut, pada tersebut terdapat 1169 baris dan 11 kolom yang saya simpan di [github_saya](https://github.com/arif-maulana-insaf/submission-1_mlterapan)
 

### Variabel-variabel prediksi popularitas destinasi wisata di indonesia
- id = nomor urutan
- nama = nama tempat
- alamat = alamat tempat
- rating = rating tempat
- jumlah review = jumlah review dari lokasi
- deskripsi = dekripsi tempat
- koordinat = titik lokasi
- url = link lokasi di maps
- provinsi = lokasi provinsi
- foto = foto lokasi
- kategori = kategori wisata


## Exploratory Data Analysis - deskripsi variabel
| # | column | Non-Null count | Dtype |
|---|--------|----------------|-------|
| 1 | id | 1169 non-null | int |
| 2 | nama | 1169 non-null | object |
| 3 | alamat | 1167 non-null | object |
| 4 | rating | 1168 non-null | float64 |
| 5 | jumlah_review | 1168 not-null | float64 |
| 6 | deskripsi | 1169 not-null | object |
| 7 | koordinat | 1169 non-null | object | 
| 8 | url | 1169 non-null | object | 
| 9 | provinsi| 1169 non-null | object | 
| 10 | foto | 1169 non-null | object | 
| 11 | kategori | 1169 non-null | object | 


dari dataset diatas banyak fitur kategorikal dan hanya beberapa yang numerikal :
- terdapat 8 fitur kategorikal atau object yaitu nama, alamat, deskripsi, koordinat, url, provinsi, foto, kategori.
- terdapat 3 fitur numerikal yang terdiri dari 2 rating, jumlah_review dan 1 int id  

Menghapus data yang dianggap tidak terlalu penting, yaitu terdiri dari 1 int dan 3 kategorikal
- id = ini dihapus karena list urutan tidak diperlukan
- koordinat = ini dihapus karena koordinat hanya tertuju pada titik dimana tempat berada yaitu latitude dan longitude
- url = ini dihapus karena hanya berisi link url destinisasi wiasata di maps
- foto = ini dihapus karena berisi foto dilokasi tersebut

### Exploratory Data Analysis - missing value dan outlier 
pengecekan missing value, duplikat dan data yang dianggap memiliki kejanggalan.
| column | value |
|--------|-------|
| id | 0 |
| nama | 0 |
| alamat | 2 |
| rating | 1 |
| jumlah_review | 1 |
| deskripsi | 0 |
| koordinat | 0 |
| url | 0 | 
| provinsi | 0 |
| foto | 0 | 
| kategori | 0 |

### Visualisasi dengan boxplot pada data numerik 
saya memakai boxplot untuk melihat untuk melihat outlier 

![image](https://github.com/user-attachments/assets/eb48b27c-1a22-4b33-86dc-0edee9a1a88b)
![image](https://github.com/user-attachments/assets/7f935aa3-2fb1-4518-b354-3480a5f9ed51)

karena outlier sangat banyak pada gambar tesebut maka saya memakai log transform agar mempertahan data tersebut sehingga menjadi seperti digambar ini 

![image](https://github.com/user-attachments/assets/4c1baa87-98f0-4643-99ee-c8498b9404ab)

### Exploratory Data Analysis - Univariate Analysis
- univariate analysis bertujuan untuk menvisualisasiskan dan menganalisis setiap fiturdawn variabel individual dalam dataset, sehingga pemahaman yang mendalam tentang distrubusi dan karakteristik data pada masing-masing fitur tersebut.
#### Univariate Analysis

![image](https://github.com/user-attachments/assets/94a8ef3c-eb22-4543-91dd-95c399e1e172)

ini adalah distribusi rating yang mana dapat dilihat 4.4-4.5 memiliki distribusi rating tertinggi dari yang lainnya

![image](https://github.com/user-attachments/assets/d969adaa-724c-488e-9185-1519b7a5db5b)

ini adalah frekuensi kategori tempat wisata yang mana dapat dilihat bahwa kategori lainnya adalah kategori yang paling banyak akan tetapi itu tidak diterdefinisi sebagai suatu objek yang sama oleh karena ini pantai adalah tempat yang paling banyak frekuensinnya berkisar 200-250

![image](https://github.com/user-attachments/assets/560c7eaf-0010-446b-af04-d4d932e9460b)

ini adalah frekuensi tempat wisata per provinsi dan bali adalah tempat yang paling banyak frekuensinya

#### Multivariate Analysis

![image](https://github.com/user-attachments/assets/6483644d-cca7-4740-bd3d-e44e087eb0b3)

ini adalah rata-rata rating per kategori yang mana kategori makam adalah yang memiliki rating paling tinggi

![image](https://github.com/user-attachments/assets/515a78f3-671c-4ba6-8c70-041eb947fa73)

ini adalah rata-rata rating per provinisi papua barat daya adalah provinsi yang memiliki rating tertinggi

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.


| No | Teknik yang Digunakan         | Alasan                                                                                             |
|----|-------------------------------|-----------------------------------------------------------------------------------------------------|
| 1  | Transformasi Log              | Digunakan pada kolom `jumlah_review` untuk menstabilkan varians akibat banyaknya outlier.          |
| 2  | Interquartile Range (IQR)     | Digunakan untuk menghapus outlier yang dapat mempengaruhi distribusi data dan performa model.      |
| 3  | Parsing String ke List        | Diperlukan agar kolom `kategori` yang awalnya berupa string list bisa diproses dalam bentuk list.  |
| 4  | MultiLabel Encoding           | Agar model dapat membaca data multikategori setelah parsing, dengan mengubahnya menjadi numerik.   |
| 5  | One-Hot Encoding              | Digunakan untuk mengubah fitur kategorikal seperti `provinsi` menjadi format numerik biner.        |
| 6  | Membuat Label Target `populer`| Menandai tempat wisata sebagai populer jika masuk dalam 30% teratas berdasarkan rating/review.     |
| 7  | Split Data (Train/Test)       | Memisahkan data latih dan data uji untuk validasi model yang lebih objektif.                       |
| 8  | SMOTE                         | Untuk menangani ketidakseimbangan kelas (imbalanced dataset) dengan oversampling kelas minoritas.  |
| 9  | StandardScaler                | Menstandarkan skala fitur numerik agar model tidak bias terhadap fitur dengan skala lebih besar. dan agat bisa dipakai oleh random forest dan decision tree yang mana tidak membutuhkan stadarscale dalam pediksi modelnya   |


## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

| No | Model                            | Penjelasan & Parameter                                                                                                                                                      |
| -- | -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | **Random Forest**                | `max_depth=5`, `n_estimators=100`, `class_weight='balanced'` – Digunakan untuk menangani ketidakseimbangan class dan mencegah overfitting dengan membatasi kedalaman pohon. `False` - Karena random forest tidak membutuhkan standarscale |
| 2  | **K-Nearest Neighbors (KNN)**    | `weights='distance'` – Memberi bobot lebih besar pada tetangga yang lebih dekat. Dikombinasikan dengan `StandardScaler()` karena KNN sensitif terhadap skala.               |
| 3  | **Support Vector Machine (SVM)** | `class_weight='balanced'`, `probability=True` – Ditambah `StandardScaler()` karena SVM sensitif terhadap skala fitur.                                                       |
| 4  | **Logistic Regression**          | `max_iter=1000`, `class_weight='balanced'` – Model linier klasik untuk klasifikasi, ditambah `StandardScaler()`.                                                            |
| 5  | **Decision Tree**                | `max_depth=3`, `class_weight='balanced'`, `False` – Bekerja tanpa perlu scaling. Depth kecil menghindari overfitting.                                                                |


### kelebihan dan kekurangan 
| Model             | Kelebihan | Kekurangan |
| ----------------- | --------- | ---------- |
| **Random Forest** | tidak membutuhkan scaling, kuat terhadap overfitting dibandingkan dengan decission tree, stabil meski ada outlier atau noise,   | sulit diinterpretasikan, lebih lambat saat training dengan data besar         |
| **Decision Tree** | mudah dipahami dan divisualisasikan, cepat untuk training dan prediksi, sama seperti random forest tidak butuh scaling | sangat rentan overfitting, kurang stabil |
| **KNN** | sederhana dan intuitif, tidak membuat asumsi tentang distribusi data | sensitif terhadap skala(butuh scaling), lambat saatu prediksi jika data besar rentan terhadap outlier |
| **svm** | bagus untuk data berdimensi tinggi, efektif dalam kasus margin yang jelas | butuh scaling, tidak cocok untuk dataset besar dan tidak seimbang, Sensitif terhadap parameter (C, kernel, gamma)|
| **logistic regression** | cepat dan efisien untuk klasifikasi linear, mudah diinterpertesikan | kurang fleksibel untuk data non linear, bisa underfitting jika relasi antar fitur kompleks |


## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.
pada bagian evaluasi ini saya menggunakan

| # | komponen evaluasi | tujuan |
|---|--------------------|--------|
| 1 | **akurasi** | yang bertujuan untuk melihat hasil data, dengan formula $\frac{TP + TN}{TP + TN + FP + FN}$ |
| 2 | **klasifikasi report** | dalam klasifikasi report Precision: Dari semua yang diprediksi positif, berapa yang benar-benar positif , dengan formula $\frac{TP}{TP + FP}$, Recall: Dari semua yang sebenarnya positif, berapa yang berhasil terprediksi dengan formula $\frac{TP}{TP + FN}$, F1-score: Gabungan dari precision dan recall, dengan formula $2 \times \frac{Precision \times Recall}{Precision + Recall}$, Support: Jumlah data per kelas |
| 3 | **perbandingan evaluasi model** | melihat evaluasi dari setiap model |
| 4 | **confusion matrix** | yaitu untuk melihat jumlah prediksi benar dan salah |
| 5 | **roc curve dan auc score** | ROC Curve menunjukkan perbandingan antara True Positive Rate (Recall) dan False Positive Rate, AUC (Area Under Curve) = seberapa besar area di bawah kurva ROC. Semakin dekat ke 1, semakin baik |
#### catatan 
- **TP** = True Positive
- **TN** = True Negative
- **FP** = False Positive
- **FN** = False Negative


### berikut adalah hasil dan perbandingan yang saya dapatkan

| # | Model                   | Akurasi (%) | F1-Score | Precision (Populer) | Recall (Populer) | Evaluasi                                                                                                    |
| -- | ----------------------- | ----------- | -------- | ------------------- | ---------------- | ----------------------------------------------------------------------------------------------------------- |
| 1  | **Random Forest**       | 78.87       | 0.76     | 0.97                | 0.62             | Performa terbaik. Akurasi tinggi dan presisi sangat baik. Recall agak rendah. Cocok untuk penggunaan utama. |
| 2  | **Decision Tree**       | 76.99       | 0.73     | 0.96                | 0.59             | Alternatif baik, mirip Random Forest namun sedikit lebih rendah. Komputasi lebih ringan.                    |
| 3  | **K-Nearest Neighbors** | 59.15       | 0.53     | 0.68                | 0.44             | Performa cukup buruk. Perlu tuning parameter. Sensitif terhadap distribusi data.                            |
| 4  | **Logistic Regression** | 56.81       | 0.51     | 0.64                | 0.42             | Hasil kurang memuaskan. Sulit membedakan tempat populer dan tidak populer.                                  |
| 5  | **SVM**                 | 46.95       | 0.00     | 0.00                | 0.00             | Gagal mengenali kelas populer. Tidak layak digunakan tanpa perbaikan skala/fit.                             |

### perbandingan evaluasi model 
![image](https://github.com/user-attachments/assets/f682bf42-f32b-4159-b803-6947c78ff0ce)

dapaat dilihat dari perbandingan hasil evalusai tersebut random forest dan decision tree adalah model yang paling seimbang dari yang lainnya

### confusion matrix
![image](https://github.com/user-attachments/assets/c9667c6a-3861-472c-9ae6-b4b99376523f)

pada tp hanya 2, maksudnya dari total kesalahan hanya 2 yang populer itu salah, akan tetapi fp 43 dari 113 data populer ini salah

![image](https://github.com/user-attachments/assets/dafc27ad-175b-46b5-9029-8033bc2d9a0f)

pada tp terdapat 34 kesalahan, yang mana ini mampu mendeteksi data populer tetapi banyak masalah, dan model ini kurang efektif

![image](https://github.com/user-attachments/assets/99eb843d-df8d-4e54-933e-9d245012eef4)

pada model ini sangat bermasalah karena fp terdapat 100 yang mana ini maksudnya model tidak mengenali tidak populer sama sekali

![image](https://github.com/user-attachments/assets/aa06c230-13ea-48f7-9915-72b733de77d5)

pada model ini fn 91 yang mana model tidak mengenali populer sama sekali karena model condong di tidak populer

![image](https://github.com/user-attachments/assets/a5548ef5-eba3-4d9f-81f6-aa77af27d697)

pada model ini fn 0, maksudnya model membaca 100% akurat untuk `tidak populer` akan tetapi masih bermasalah pada fn masih terdapat masalah 45 data klasifikasi yang salah 

### roc curve dan auc score

![image](https://github.com/user-attachments/assets/87c2412e-c37b-4c32-b04e-dc49e105be37)

#### catatan 
- True Positive Rate (TPR) = Sensitivitas = Recall
- False Positive Rate (FPR) = 1 - Spesifisitas

| Model                   | AUC      | Evaluasi                                                            |
| ----------------------- | -------- | ------------------------------------------------------------------- |
| **Decision Tree**       | **0.84** | **Terbaik** dalam membedakan kelas, sangat baik untuk klasifikasi.  |
| **Random Forest**       | 0.81     | Hampir sebaik Decision Tree, performa stabil dan kuat.              |
| **Logistic Regression** | 0.61     | Di atas tebakan acak, tapi jauh lebih rendah dari model tree-based. |
| **KNN**                 | 0.60     | Performa buruk, hanya sedikit lebih baik dari tebakan acak.         |
| **SVM**                 | 0.59     | Hampir sama seperti KNN, **sangat tidak optimal** pada dataset ini. |




**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

