# Laporan Proyek Machine Learning - Arif Maulana Insaf

## Domain Proyek : Destinasi Wisata

Pada bagian ini, kamu perlu menuliskan latar belakang yang relevan dengan proyek yang diangkat.

wisata di indonesia sangat indah dan beragam, dan dengan keberagamannya hampir tidak ada alasan dunia untuk tidak mengenali wisata di indonesia. dikutip dari [UNESCO](https://whc.unesco.org/en/statesparties/id) tercatat 10 tempat di indonesia yang telah di akui dunia seperti raja ampat, pulau komodo dan masih banyak lain. akan tetapi itu hanya sebagian kecil tempat wisata di indonesia.

melalui analsis ini, diharapkan dapat membantu lokasi tempat yang belum dikenal wisatawan lain untuk mengunjugi tempat-tempat tersebut
**Rubrik/Kriteria Tambahan (Opsional)**:
- melalui analsis pengelompokan ini, diharapkan dapat membantu lokasi tempat yang belum dikenal wisatawan lain untuk mengunjugi tempat-tempat tersebut
- [referensi](https://ejournal.stipram.ac.id/index.php/kepariwisataan/article/view/209)


- Jelaskan mengapa dan bagaimana masalah tersebut harus diselesaikan
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
- Format Referensi dapat mengacu pada penulisan sitasi [IEEE](https://journals.ieeeauthorcenter.ieee.org/wp-content/uploads/sites/7/IEEE_Reference_Guide.pdf), [APA](https://www.mendeley.com/guides/apa-citation-guide/) atau secara umum seperti [di sini](https://penerbitdeepublish.com/menulis-buku-membuat-sitasi-dengan-mudah/)
- Sumber yang bisa digunakan [Scholar](https://scholar.google.com/)

## Business Understanding

Pada bagian ini, kamu perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- bagaimana cara tempat wisata populer di indonesia berdasarkan data rating dan jumlah review
- bagaimana cara memanfaatkan data kategorikal (kategori dan provinsi) dalam membangun model klasifikasi popularitas
- bagaimana cara mengatasi imbalancing

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengembangkan model klasifikasi untuk memprediksi apakah sebuah tempat wisata populer atau tidak
- menggunakan informasi kategori dan provinsi untuk memperkaya fitur input bagi model prediktif
- menggukanakan teknik smote untuk mengatasi teknik imbalancing

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:


- Menambahkan bagian “Solution Statement” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements

|model | hasil |
|------|-------|
|random forest| akurasi 75.2% dan f1 score 69.8%, ini menunjukan performa terbaik diantara semua model|
|KNN| akurasi 55.0% dan f1 score 50.0%, ini menunjukan performa yang buruk|
|SVM| akurasi 46.0% dan f1 score 0%, ini menunjukan peforma yang paling buruk diantara yang lain|
logistic regression| akurasi 52.0% dan f1 score 44.0%, ini menunjukan  performa yang buruk|
|decision tree| akurasi 72% dan f1 score, ini menunjukan performa yang lumayan ketimbang tang lain akan tetapi lebih rendah dari random forest|


    - Mengajukan 2 atau lebih solution statement. Misalnya, menggunakan dua atau lebih algoritma untuk mencapai solusi yang diinginkan atau melakukan improvement pada baseline model dengan hyperparameter tuning.
    - Solusi yang diberikan harus dapat terukur dengan metrik evaluasi.

## Data Understanding

saya menggunakan teknik scraping untuk mendapatkan dataset tersebut, pada tersebut terdapat 1169 baris dan 11 kolom yang saya simpan di [github_saya](https://github.com/arif-maulana-insaf/submission-1_mlterapan)

Paragraf awal bagian ini menjelaskan informasi mengenai data yang Anda gunakan dalam proyek. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
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
**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data atau exploratory data analysis.
|#|column| Non-Null count| Dtype|
|1|id|1169 non-null|int|
|2|nama|1169 non-null|object|
|3|alamat|1167 non-null|object|
|4|rating|1168 non-null|float64|
|5|jumlah_review|1168 not-null|float64|
|6|deskripsi|1169 not-null|object|
|7|koordinat|1169 non-null|object| 
|8|url|1169 non-null|object| 
|9|provinsi|1169 non-null|object| 
|10|foto|1169 non-null|object| 
|11|kategori|1169 non-null|object| 
## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
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

