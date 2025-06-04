# Laporan Proyek Machine Learning - Arif Maulana Insaf

## Domain Proyek : Destinasi Wisata

wisata di indonesia sangat indah dan beragam, dan dengan keberagamannya hampir tidak ada alasan dunia untuk tidak mengenali wisata di indonesia. dikutip dari [UNESCO](https://whc.unesco.org/en/statesparties/id) tercatat 10 tempat di indonesia yang telah di akui dunia seperti raja ampat, pulau komodo dan masih banyak lain. akan tetapi itu hanya sebagian kecil tempat wisata di indonesia.

melalui analsis ini, diharapkan dapat membantu lokasi tempat yang belum dikenal wisatawan lain untuk mengunjugi tempat-tempat tersebut
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

Dataset yang digunakan dalam proyek ini adalah Dataset Tempat Wisata Indonesia yang berisi informasi komprehensif tentang destinasi wisata di seluruh Indonesia. Dataset ini dikumpulkan dengan scraping di Google Maps dan berisi 1.169 tempat wisata yang tersebar di 38 provinsi Indonesia. dan ini saya kumpulkan dan saya upload di github beserta cara saya scarpinya juga.

**Sumber Dataset**: 
- **Tautan**: [tempat_wisata_indonesia.csv](https://github.com/NusantaraGo/NusantaraGo-ML/blob/main/Scrape_Data/tempat_wisata_indonesia.csv)
- **Metode Pengumpulan**: Web scraping dari Google Maps

**Informasi Dataset**:
- **Jumlah data**: 1.169 tempat wisata
- **Jumlah kolom**: 11 kolom
- **Ukuran dataset**: (1169, 11)
- **Kondisi data**: Dataset relatif bersih dengan beberapa missing values

 

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
|  1 | dropna()                      | karena terdapat missing value yang mana hanya 2 baris oleh karena itu saya menghapus baris tersebut |
| 2  | drop_columns()                | saya menghapus beberapa columns yaitu `id`, `koordinat`, `url`, `foto` karena columns tersebut tidak akan sya gunakan |
| 3  | Transformasi Log              | Digunakan pada kolom `jumlah_review` untuk menstabilkan varians akibat banyaknya outlier.          |
| 4  | Interquartile Range (IQR)     | Digunakan untuk menghapus outlier yang dapat mempengaruhi distribusi data dan performa model.      |
| 5  | Parsing String ke List        | Diperlukan agar kolom `kategori` yang awalnya berupa string list bisa diproses dalam bentuk list.  |
| 6  | MultiLabel Encoding           | Agar model dapat membaca data multikategori setelah parsing, dengan mengubahnya menjadi numerik.   |
| 7  | One-Hot Encoding              | Digunakan untuk mengubah fitur kategorikal seperti `provinsi` menjadi format numerik biner.        |
| 8  | Membuat Label Target `populer`| Menandai tempat wisata sebagai populer jika masuk dalam 30% teratas berdasarkan rating/review.     |
| 9  | Split Data (Train/Test)       | Memisahkan data latih dan data uji untuk validasi model yang lebih objektif.                       |
| 10 | StandardScaler                | Menstandarkan skala fitur numerik agar model tidak bias terhadap fitur dengan skala lebih besar. dan agat bisa dipakai oleh random forest dan decision tree yang mana tidak membutuhkan stadarscale dalam pediksi modelnya   |


## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

### random forest
Random Forest adalah algoritma ensemble learning berbasis decision tree. Ia bekerja dengan membuat banyak decision tree secara acak (randomized trees), lalu menggabungkan hasilnya (voting untuk klasifikasi, rata-rata untuk regresi). Sangat handal terhadap outlier, data tidak linear, dan tidak membutuhkan scaling fitur.

| parameternya | fungsinya |
|---------------|--------|
| `max_depth=5` | Membatasi kedalaman (jumlah level) dari setiap pohon agar tidak terlalu kompleks, mencegah overfitting terhadap data latih. |
| `n_estimators=100` | Menentukan jumlah pohon (tree) dalam ensemble. Semakin banyak pohon, semakin stabil dan akurat model, namun waktu komputasi juga bertambah. |
| `class_weight='balanced'` | Menyesuaikan bobot kelas secara otomatis berdasarkan frekuensi. Berguna jika jumlah data antar kelas tidak seimbang (misalnya, kelas mayoritas 90%, minoritas 10%). |


### kelebihaan dan kekurangan random forest
#### kelebihan
- Akurasi tinggi: Menggabungkan banyak pohon membuat prediksi lebih stabil dan kuat terhadap overfitting.
- Robust terhadap outlier dan noise: Tidak mudah dipengaruhi oleh data ekstrem.
- Cocok untuk data dengan fitur non-linear: Karena setiap tree dapat membagi data secara non-linear.
- Menangani missing value dan data imbalance dengan baik.
- Tidak perlu scaling atau normalisasi fitur.
#### kekuragan
- Kurang interpretatif: Sulit menjelaskan bagaimana prediksi dibuat karena banyaknya pohon (model kompleks).
- Waktu prediksi relatif lambat untuk dataset besar (karena harus memproses banyak pohon).
- Model besar: Konsumsi memori tinggi karena menyimpan banyak tree.



### K-nearest neightbors (KNN)
KNN adalah model instance-based learning, di mana prediksi dilakukan berdasarkan kedekatan (jarak) ke beberapa tetangga terdekat (biasanya menggunakan Euclidean Distance). Tidak ada proses pelatihan aktual model menyimpan semua data latih.

| parameternya | fungsinya |
|---------------|--------|
| `weights='distance'` | Memberi bobot lebih besar pada tetangga yang lebih dekat. Artinya, tetangga yang lebih jauh kurang berpengaruh, sehingga hasil lebih akurat dibandingkan bobot rata (uniform). |
| `n_neighbors=5` | Jumlah tetangga terdekat yang dipertimbangkan saat menentukan kelas target. Nilai default 5, namun bisa disesuaikan untuk optimasi performa. |

### kelebihan dan kekurangan K-nearest neightbors (KNN)
#### kelebihan
- Mudah dipahami dan diimplementasikan: Konsep intuitif berdasarkan tetangga terdekat.
- Tidak ada proses pelatihan: Cukup menyimpan data latih (lazy learner).
- Adaptif terhadap bentuk distribusi data: Tidak mengasumsikan distribusi linear.
#### kekurangan
- Waktu prediksi lambat: Harus menghitung jarak ke semua titik saat memprediksi (tidak efisien untuk data besar).
- Sensitif terhadap skala fitur dan outlier: Fitur yang besar bisa mendominasi jarak, outlier bisa menyesatkan.
- Tidak cocok untuk data berdimensi tinggi (curse of dimensionality).
- Tidak melakukan generalisasi: Hanya "menyontek" data pelatihan.

### Support Vector Machine (SVM)
SVM adalah model diskriminatif yang mencari hyperplane terbaik yang memisahkan kelas-kelas data dengan margin maksimum. Sangat efektif untuk data high-dimensional dan bisa menggunakan kernel untuk menangani non-linearitas.

| parameternya | fungsinya |
|---------------|--------|
| `class_weight='balanced'` | Menyeimbangkan bobot kelas secara otomatis berdasarkan frekuensi data. Sangat penting untuk menghindari bias ke kelas mayoritas. |
| `probability=True` | Mengaktifkan kemampuan untuk menghitung probabilitas prediksi, bukan hanya label. Berguna untuk evaluasi model (misalnya ROC AUC) dan stacking ensemble. |

### kelebihan dan kekurangan Support Vector Machine (SVM)
#### kelebihan
- Akurasi tinggi pada data high-dimensional: Efektif saat jumlah fitur besar.
- Tahan terhadap overfitting jika parameter disetel dengan benar.
- Dapat menggunakan kernel untuk menangani data yang tidak linear (misalnya kernel RBF, polynomial).
- Fokus pada support vectors: Hanya sebagian data yang berpengaruh, membuat model efisien secara konsep.
#### kekurangan 
- Waktu pelatihan bisa lama untuk dataset besar.
- Sulit diinterpretasikan: Tidak mudah menjelaskan keputusan model (terutama dengan kernel).
- Perlu scaling fitur: Sangat sensitif terhadap perbedaan skala.
- Pemilihan parameter (C, kernel, gamma) krusial dan kompleks.


### Logistic Regression
Logistic Regression adalah model linier yang digunakan untuk klasifikasi biner (atau multinomial). Ia menghitung probabilitas dari suatu data termasuk ke dalam suatu kelas berdasarkan fungsi logistik (sigmoid). Sangat cocok untuk baseline atau ketika interpretasi model penting.

| parameternya | fungsinya |
|---------------|--------|
| `max_iter=1000` | Menentukan jumlah maksimum iterasi pelatihan. Jika data kompleks, iterasi kecil bisa gagal konvergen. Disetel tinggi agar model memiliki cukup waktu belajar. |
| `class_weight='balanced'` | Menangani class imbalance dengan memberi penalti lebih besar pada kesalahan di kelas minoritas, mencegah model bias ke mayoritas. |

### kelebihan dan kekurangan Logistic Regression
#### kelebihan 
- Cepat dan efisien: Pelatihan dan prediksi cepat, cocok untuk dataset besar dan baseline.
- Interpretatif: Koefisien model menunjukkan pengaruh fitur (positif atau negatif) secara langsung.
- Dapat diperluas ke klasifikasi multikelas dengan pendekatan one-vs-rest atau softmax.
- Mudah dituning dan jarang overfitting jika fitur tidak terlalu banyak.
#### kekurangan
- Kinerja buruk untuk data non-linear: Model linier tidak bisa memisahkan kelas yang bentuknya non-linear.
- Perlu scaling agar bobot fitur adil.
- Rentan terhadap multikolinearitas antar fitur.
- Tidak cocok untuk data dengan interaksi fitur kompleks.


### Decision Tree
Decision Tree adalah model berbentuk pohon yang membagi data berdasarkan fitur untuk mencapai prediksi. Setiap simpul pohon memutuskan pembagian berdasarkan fitur yang menghasilkan impuritas paling rendah. Mudah dimengerti dan tidak memerlukan scaling.

| parameternya | fungsinya |
|---------------|--------|
| `max_depth=3` | Membatasi kedalaman pohon hingga 3 level saja, untuk menghindari overfitting dan meningkatkan interpretabilitas. |
| `class_weight='balanced'` | Sama seperti model lain, memberi bobot lebih tinggi pada kelas minoritas, membantu mengatasi distribusi kelas yang tidak merata. |
| `criterion='gini'` | Ukuran untuk memilih fitur pemisah di setiap simpul. Gini impurity mengukur ketidakteraturan dalam node (default). Alternatifnya adalah 'entropy'. |


### kelebihan dan kekurangan Decision Tree
#### kelebihan 
- Sangat interpretatif: Struktur pohon bisa divisualisasikan dan dijelaskan secara logis.
- Tidak butuh scaling atau normalisasi.
- Dapat menangani fitur kategorikal dan numerik sekaligus.
- Cepat dilatih dan diprediksi, cocok untuk aplikasi real-time.
#### kekurangan
- Mudah overfitting: Jika tidak dibatasi (misalnya max_depth), pohon akan belajar noise.
- Cenderung tidak stabil: Perubahan kecil pada data bisa menghasilkan struktur pohon yang sangat berbeda.
- Kurang akurat dibandingkan model ensemble (seperti Random Forest).
- Tidak cocok untuk data dengan banyak noise.


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
| # | Model                   | Akurasi (%) | F1-Score | Precision (Populer) | Recall (Populer) | Evaluasi                                                                                                                         |
| - | ----------------------- | ----------- | -------- | ------------------- | ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 1 | **Random Forest**       | 78.87       | 0.76     | 0.97                | 0.62             | **Performa terbaik secara keseluruhan.** Akurasi tinggi, precision sangat tinggi. Recall agak rendah. Cocok sebagai model utama. |
| 2 | **Decision Tree**       | 78.87       | 0.75     | 1.00                | 0.60             | Alternatif yang sangat mirip Random Forest, tapi lebih ringan dan cepat.                                                         |
| 3 | **Logistic Regression** | 70.89       | 0.73     | 0.72                | 0.74             | Performa seimbang, cocok untuk baseline. Tidak sebaik tree-based model tapi stabil.                                              |
| 4 | **SVM**                 | 70.42       | 0.72     | 0.72                | 0.73             | Performa cukup baik. Tidak sekuat Random Forest atau Decision Tree, tapi tetap layak dipertimbangkan.                            |
| 5 | **K-Nearest Neighbors** | 67.61       | 0.69     | 0.70                | 0.67             | Paling lemah di antara semua model. Perlu tuning parameter `k` lebih lanjut.                                                     |




### perbandingan evaluasi model 
![image](https://github.com/user-attachments/assets/916793a4-bb8d-41ed-9436-440edecd2df8)


dapaat dilihat dari perbandingan hasil evalusai tersebut random forest dan decision tree adalah model yang paling seimbang dari yang lainnya

### confusion matrix
![image](https://github.com/user-attachments/assets/c9667c6a-3861-472c-9ae6-b4b99376523f)

- Model memiliki akurasi tinggi dalam memprediksi "Tidak Populer" (98 benar, 2 salah).
- Prediksi "Populer" cukup baik (70 benar) tetapi masih ada kesalahan (43 salah).
- Performa lebih konsisten dibandingkan Decision Tree sebelumnya, terutama untuk kelas minoritas ("Populer").
- Rekomendasi: Evaluasi lebih lanjut untuk mengurangi false negative (43 prediksi "Populer" yang salah) dengan teknik seperti class weighting atau data augmentation.

![image](https://github.com/user-attachments/assets/aa9a41d6-3537-4bbe-a436-a7a5c7837d5c)

- Model memiliki akurasi yang baik dalam memprediksi kelas "Tidak Populer" (100 benar, 0 salah).
- Performa model pada kelas "Populer" kurang konsisten (68 benar, tetapi ada 45 dan 40 prediksi salah).
- Terdapat ketidakseimbangan klasifikasi, terutama saat memprediksi "Populer" sebagai "Tidak Populer".
- Secara umum, model lebih andal untuk prediksi "Tidak Populer" dibandingkan "Populer".

![image](https://github.com/user-attachments/assets/15b7650f-e94e-4c38-a2f8-f9f78f301b68)

- Model menunjukkan performa yang cukup baik dengan prediksi benar (68 Tidak Populer dan 76 Populer).
- Namun, masih ada kesalahan prediksi (32 dan 37), terutama pada klasifikasi "Populer".
- Rekomendasi: Optimalkan model (misalnya dengan tuning hyperparameter) untuk mengurangi kesalahan, khususnya pada kelas minoritas jika ada ketidakseimbangan data.

![image](https://github.com/user-attachments/assets/441f593a-a751-4f56-a56c-7ff00969cf54)

- Akurasi tinggi untuk prediksi "Populer" (83 benar), tetapi masih ada kesalahan (30 salah).
- Prediksi "Tidak Populer" cukup baik (67 benar), meski terdapat 33 misklasifikasi.
- Rekomendasi: Fokus pada peningkatan prediksi "Tidak Populer", seperti penyeimbangan data atau optimasi model.

![image](https://github.com/user-attachments/assets/aec5df18-f05d-4884-a9ff-62f6d9539598)

- Prediksi "Populer" sangat akurat (84 benar) dengan sedikit kesalahan (29 salah).
- Prediksi "Tidak Populer" cukup baik (67 benar) namun masih ada 33 kesalahan.
- Rekomendasi: Tingkatkan akurasi untuk kelas "Tidak Populer" dengan teknik seperti resampling atau feature engineering.

### roc curve dan auc score

![image](https://github.com/user-attachments/assets/7220c6fe-8e8e-4c84-8d01-811676ef09a1)


#### catatan 
- True Positive Rate (TPR) = Sensitivitas = Recall
- False Positive Rate (FPR) = 1 - Spesifisitas

| **Model**               | **AUC**  | **Evaluasi**                                                               |
| ----------------------- | -------- | -------------------------------------------------------------------------- |
| **Decision Tree**       | **0.84** | Performa terbaik dalam membedakan kelas, sangat cocok untuk klasifikasi.   |
| **Random Forest**       | 0.83     | Hampir sebaik Decision Tree, kuat dan stabil, cocok untuk generalisasi.    |
| **SVM**                 | 0.80     | Cukup baik, menunjukkan kemampuan diskriminatif yang layak.                |
| **Logistic Regression** | 0.80     | Sejajar dengan SVM, performa cukup stabil meskipun lebih sederhana.        |
| **KNN**                 | 0.73     | Performa paling rendah di antara model lain, sensitif terhadap skala data. |





**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

