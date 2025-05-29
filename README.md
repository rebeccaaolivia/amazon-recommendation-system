# Laporan Proyek Machine Learning - Rebecca Olivia

## Project Overview

### Latar Belakang

Proyek ini bertujuan untuk membangun sistem rekomendasi produk menggunakan dataset penjualan dan ulasan produk dari Amazon. Di era digital saat ini, perkembangan *e-commerce* berlangsung sangat cepat dan telah mengubah preferensi serta perilaku konsumen dalam berbelanja, yang mendorong pergeseran besar menuju platform digital [[1](https://ejournalwarmadewa.id/index.php/juinhum/article/view/8482)]. *E-commerce* sendiri merupakan aktivitas jual beli produk maupun jasa melalui jaringan internet. Perannya yang krusial dalam perekonomian global terletak pada kemampuannya menjangkau pasar yang lebih luas, meningkatkan efisiensi operasional bisnis, serta memberikan pengalaman berbelanja yang lebih praktis dan nyaman bagi pengguna [[2](https://mutiara.al-makkipublisher.com/index.php/al/article/view/220/298)]. Dalam konteks ini, kemampuan untuk memberikan rekomendasi produk yang tepat kepada konsumen menjadi faktor penting untuk meningkatkan pengalaman berbelanja, mendorong peningkatan penjualan, serta membangun loyalitas pelanggan. Dataset Amazon yang digunakan menyediakan informasi berharga mengenai interaksi pengguna dengan produk, termasuk detail produk, kategori, harga, rating, jumlah rating, serta konten ulasan. 

### Pentingnya Proyek

Proyek sistem rekomendasi ini penting karena [[3](https://alphasoft.id/blog/bisnis-5/apa-manfaat-penggunaan-sistem-e-commerce-bagi-peningkatan-penjualan-146)]:

1. **Aksesibilitas Tanpa Batas Waktu**: Sistem *e-commerce* memberikan kemudahan akses selama 24 jam sehari dan 7 hari dalam seminggu, tanpa dibatasi oleh jam operasional sebagaimana pada toko fisik. Hal ini memberikan peluang penjualan yang lebih besar, terutama bagi konsumen yang memiliki keterbatasan waktu atau berada di lokasi terpencil.
2. **Perluasan Jangkauan Pasar**: Melalui platform *e-commerce*, pelaku usaha dapat memperluas jangkauan pasarnya ke tingkat global. Produk yang ditawarkan tidak hanya dapat diakses oleh konsumen lokal, tetapi juga oleh konsumen internasional, sehingga meningkatkan potensi pendapatan bisnis.
3. **Personalisasi dan Rekomendasi Produk**: Dengan memanfaatkan data analitik dan algoritma kecerdasan buatan, *e-commerce* memungkinkan pengalaman belanja yang lebih personal. Sistem dapat memberikan rekomendasi produk berdasarkan preferensi atau riwayat pembelian pengguna, yang berkontribusi terhadap peningkatan tingkat konversi dan loyalitas pelanggan.
4. **Efisiensi Operasional dan Penghematan Biaya**: Implementasi *e-commerce* dapat menekan biaya operasional karena mengurangi kebutuhan akan toko fisik dan jumlah tenaga kerja. Selain itu, proses otomatisasi seperti sistem pembayaran daring dan manajemen inventaris turut meningkatkan efisiensi operasional.
5. **Peningkatan Pengalaman Belanja Konsumen**: Konsumen dapat dengan mudah membandingkan harga, membaca ulasan, serta memperoleh informasi produk secara lengkap sebelum melakukan pembelian. Hal ini menciptakan pengalaman belanja yang lebih nyaman, informatif, dan transparan.
6. **Kemudahan dalam Pelaksanaan Kampanye Pemasaran**: Platform *e-commerce* memungkinkan pelaku usaha untuk menjalankan kampanye pemasaran digital secara efektif dan terukur. Strategi promosi seperti *email marketing*, iklan digital tertarget, serta penggunaan media sosial dapat dioptimalkan untuk menjangkau lebih banyak konsumen.
7. **Pengumpulan dan Pemanfaatan Data Konsumen**: Melalui *e-commerce*, pelaku bisnis dapat memperoleh data penting mengenai perilaku konsumen, seperti preferensi, pola pembelian, dan demografi. Data ini sangat bermanfaat untuk menyusun strategi pemasaran dan pengambilan keputusan yang berbasis pada analisis data.

### Hasil Riset atau Referensi Terkait

Proyek ini mengimplementasikan dua pendekatan utama dalam sistem rekomendasi:

1.  **Content-Based Filtering:** Pendekatan ini merekomendasikan produk berdasarkan kesamaan fitur antara produk yang disukai pengguna di masa lalu dengan produk lain. Dalam proyek ini, fitur tekstual (nama produk, kategori, deskripsi, ulasan) diekstraksi menggunakan **TF-IDF (Term Frequency-Inverse Document Frequency)** untuk merepresentasikan konten produk dalam bentuk vektor numerik. **Cosine Similarity** kemudian dihitung untuk mengukur tingkat kemiripan antar produk. Referensi terkait meliputi literatur tentang Information Retrieval dan Text Mining, serta studi kasus penerapan TF-IDF dan Cosine Similarity dalam rekomendasi item.
2.  **Collaborative Filtering:** Pendekatan ini merekomendasikan produk kepada seorang pengguna berdasarkan preferensi pengguna lain yang memiliki selera serupa (User-Based) atau berdasarkan produk-produk yang sering disukai bersama oleh pengguna lain (Item-Based). Dalam proyek ini, digunakan pendekatan **Model-Based Collaborative Filtering** menggunakan **Neural Network (RecommenderNet)**. Model ini mempelajari representasi (*embeddings*) laten dari pengguna dan produk dari data rating untuk memprediksi preferensi pengguna terhadap produk yang belum pernah dilihat. Referensi utama untuk pendekatan ini adalah makalah atau tutorial mengenai model *matrix factorization* berbasis neural network atau model rekomendasi mendalam (Deep Learning based recommendation systems).

Proses data understanding dan EDA (Exploratory Data Analysis) yang dilakukan menunjukkan bahwa dataset memiliki sebaran kategori dan rating yang beragam, serta adanya nilai-nilai yang perlu ditangani (missing values dan nilai tidak konsisten) sebelum pemodelan. Hasil tuning hyperparameter pada model Collaborative Filtering menunjukkan kombinasi parameter yang optimal untuk dataset ini guna mencapai performa prediksi rating terbaik.


## Business Understanding

Proyek sistem rekomendasi ini berangkat dari observasi umum dalam ekosistem e-commerce, di mana pengguna dihadapkan pada jumlah produk yang sangat besar. Fenomena ini, yang dikenal sebagai *information overload*, seringkali menyulitkan pengguna untuk menemukan produk yang benar-benar relevan dengan minat dan kebutuhan mereka. Di sisi lain, bagi platform e-commerce, kesulitan pengguna dalam menemukan produk yang tepat dapat berujung pada rendahnya tingkat konversi (pembelian), kepuasan pengguna yang menurun, dan pada akhirnya hilangnya potensi pendapatan. Untuk mengklarifikasi masalah ini, maka dilakukan analisis dataset penjualan dan ulasan dari Amazon, yang merepresentasikan interaksi nyata antara pengguna dan produk. Dilakukan identifikasi bahwa data ini mengandung informasi berharga mengenai perilaku pengguna (ulasan dan rating) serta karakteristik produk (nama, kategori, deskripsi). Informasi ini menjadi kunci untuk memahami preferensi pengguna dan atribut produk, yang dapat dimanfaatkan untuk mempersonalisasi pengalaman belanja. Proses klarifikasi masalah ini melibatkan identifikasi *gap* antara ketersediaan produk yang melimpah dan kemampuan pengguna untuk menavigasi serta menemukan produk yang diinginkan secara efisien. *Gap* inilah yang berusaha dijembatani oleh sistem rekomendasi.

### Problem Statements

Berdasarkan klarifikasi masalah di atas, pernyataan masalah yang ingin diatasi melalui proyek ini adalah:

1.  Bagaimana cara membantu pengguna platform e-commerce menemukan produk yang relevan dengan minat dan preferensi mereka di tengah jutaan produk yang tersedia?
2.  Bagaimana platform e-commerce dapat meningkatkan tingkat interaksi pengguna dan konversi penjualan dengan menyediakan rekomendasi produk yang personal dan akurat?

### Goals

Tujuan utama dari proyek ini adalah untuk membangun sistem rekomendasi produk yang efektif menggunakan dataset Amazon, dengan target sebagai berikut:

1.  Mengembangkan model rekomendasi yang mampu memberikan daftar produk yang relevan untuk pengguna individual. Relevansi ini dapat didasarkan pada kesamaan konten produk atau pola perilaku pengguna lain.
2.  Menyediakan dua pendekatan model rekomendasi (Content-Based Filtering dan Collaborative Filtering) sebagai perbandingan kinerja dan eksplorasi metode yang berbeda.
3.  Menghasilkan rekomendasi yang dapat meningkatkan potensi pengguna untuk menemukan dan membeli produk yang sesuai, meskipun pengukuran dampak langsung terhadap konversi berada di luar cakupan proyek ini.

### Solution statements

Untuk mencapai tujuan yang telah ditetapkan, maka akan diimplementasikan dua pendekatan utama dalam membangun sistem rekomendasi: Content-Based Filtering dan Collaborative Filtering.

1. **Content-Based Filtering**: Pendekatan Content-Based Filtering akan berfokus pada karakteristik intrinsik dari item (produk). Ide dasarnya adalah merekomendasikan item kepada pengguna yang "mirip" dengan item yang disukai pengguna di masa lalu.

*   **Cara Kerja:**
    *   Setiap produk akan direpresentasikan sebagai vektor fitur berdasarkan atribut-atributnya seperti nama produk, kategori, deskripsi, dan konten ulasan.
    *   Teknik **TF-IDF (Term Frequency-Inverse Document Frequency)** akan digunakan untuk mengubah teks dari atribut-atribut ini menjadi representasi numerik (vektor). TF-IDF memberikan bobot lebih tinggi pada kata-kata yang penting dalam sebuah dokumen (produk) tetapi jarang muncul di dokumen lain.
    *   Setelah setiap produk direpresentasikan sebagai vektor TF-IDF, **Cosine Similarity** akan dihitung antara semua pasangan produk. Cosine Similarity mengukur sudut antara dua vektor, di mana nilai mendekati 1 menunjukkan kemiripan tinggi dan nilai mendekati 0 menunjukkan kemiripan rendah. Matriks Cosine Similarity akan menyimpan skor kemiripan antara setiap produk dengan setiap produk lainnya.
    *   Ketika seorang pengguna melihat atau menyukai suatu produk, sistem akan mencari produk lain yang memiliki skor Cosine Similarity tinggi dengan produk tersebut dalam matriks kemiripan. Produk-produk dengan skor tertinggi (di luar produk yang sudah dilihat/disukai) akan direkomendasikan kepada pengguna.

*   **Keunggulan:**
    *   Tidak memerlukan data interaksi dari banyak pengguna; dapat merekomendasikan produk baru meskipun belum ada yang memberikannya rating atau ulasan.
    *   Dapat merekomendasikan item-item yang jarang (niche items) jika kontennya sesuai.
    *   Rekomendasi mudah dijelaskan berdasarkan fitur-fitur item itu sendiri.

*   **Keterbatasan:**
    *   Sulit merekomendasikan item yang kontennya sangat berbeda dari preferensi pengguna di masa lalu (filter bubble).
    *   Membutuhkan analisis konten yang mendalam; jika konten item tidak deskriptif, kinerja rekomendasi bisa buruk.

2. **Collaborative Filtering**: Pendekatan Collaborative Filtering (CF) akan memanfaatkan data interaksi pengguna dengan item, khususnya rating produk dalam dataset ini. CF berasumsi bahwa pengguna yang memiliki preferensi serupa di masa lalu akan terus memiliki preferensi yang serupa di masa depan. Pendekatan yang akan digunakan adalah Model-Based CF menggunakan Neural Network.

*   **Cara Kerja:**
    *   Data interaksi (user_id, product_id, rating) akan digunakan sebagai input.
    *   ID pengguna dan produk akan di-*encode* menjadi indeks numerik.
    *   Rating produk akan dinormalisasi ke dalam rentang 0-1 untuk digunakan sebagai target prediksi.
    *   Model **RecommenderNet** (atau arsitektur serupa berbasis neural network) akan dibangun. Model ini biasanya terdiri dari:
        *   *Embedding layers* untuk pengguna dan produk: Setiap pengguna dan produk direpresentasikan sebagai vektor berdimensi rendah (embedding) yang dipelajari selama pelatihan. Vektor ini menangkap preferensi pengguna dan karakteristik laten produk.
        *   Lapisan yang menghitung *dot product* (atau interaksi lain) antara embedding pengguna dan produk.
        *   Lapisan *bias* untuk pengguna dan produk untuk menangkap preferensi rata-rata pengguna atau popularitas rata-rata produk.
        *   Lapisan aktivasi (misalnya Sigmoid) untuk memprediksi rating yang dinormalisasi.
    *   Model dilatih menggunakan data interaksi untuk meminimalkan kesalahan prediksi rating. Selama pelatihan, embedding pengguna dan produk disesuaikan sehingga dot product dari embedding pengguna dan produk ditambah bias mereka mendekati rating aktual yang dinormalisasi.
    *   Setelah model dilatih, untuk merekomendasikan produk kepada pengguna tertentu, model akan mengambil embedding pengguna tersebut dan menghitung prediksi rating untuk semua produk yang belum pernah diberi rating oleh pengguna tersebut.
    *   Produk-produk dengan prediksi rating tertinggi akan direkomendasikan kepada pengguna.

*   **Keunggulan:**
    *   Mampu menemukan pola dan interaksi kompleks antar pengguna dan item yang mungkin sulit ditangkap oleh analisis konten murni.
    *   Dapat merekomendasikan item-item yang "tidak terduga" namun disukai oleh pengguna serupa (serendipity).
    *   Tidak bergantung pada konten item itu sendiri, sehingga bekerja baik bahkan jika informasi konten minim.

*   **Keterbatasan:**
    *   **Cold Start Problem:** Sulit memberikan rekomendasi untuk pengguna baru (belum ada interaksi historis) atau item baru (belum ada yang memberikan rating).
    *   Membutuhkan data interaksi dalam jumlah besar untuk kinerja yang optimal.
    *   Rekomendasi terkadang sulit dijelaskan kepada pengguna ('mengapa saya direkomendasikan ini?').

Kedua pendekatan ini akan dikembangkan dan diuji secara terpisah, memberikan wawasan komparatif mengenai efektivitas masing-masing dalam konteks dataset Amazon ini.


## Data Understanding

Bagian ini bertujuan untuk memahami struktur, tipe data, kualitas data, serta informasi penting dari dataset yang digunakan sebelum dilakukan analisis atau pembuatan model sistem rekomendasi. Melalui Data Understanding, dapat mengidentifikasi pola, tren, atau anomali yang ada dalam data, yang kemudian akan membantu dalam proses *feature engineering*, pemilihan model, dan interpretasi hasil.

Dataset yang digunakan dalam proyek ini adalah "**Amazon Sales Dataset**", yang diunduh dari [[Kaggle](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset/data)]. Dataset ini berisi informasi mengenai penjualan dan ulasan produk di Amazon, yang mencakup berbagai detail penting untuk analisis dan pembangunan sistem rekomendasi.

### Informasi Mengenai Data

Dataset ini memiliki **1465 baris** data awal dan **16 kolom**. Setelah proses pembersihan data (menghapus nilai yang hilang dan nilai tidak konsisten), jumlah data menjadi **1462 baris**.

*   **Jumlah Data Produk Unik:** 1351 (awal) -> 1348 (setelah pembersihan)
*   **Jumlah Data User Unik:** 1194 (awal) -> 1191 (setelah pembersihan)
*   **Jumlah Data Review Unik:** 1194 (awal) -> 1191 (setelah pembersihan)

Kondisi data secara umum cukup baik setelah dilakukan langkah-langkah pembersihan untuk menangani *missing values* pada kolom `rating_count` dan nilai tidak konsisten ('|') pada kolom `rating`. Tipe data untuk kolom harga, persentase diskon, rating, dan jumlah rating telah diubah menjadi numerik (`float64`) agar siap untuk analisis. Tidak ditemukan baris yang sepenuhnya duplikat dalam datase

### Deskripsi Variabel (Fitur)

Dataset ini terdiri dari 16 kolom dengan rincian sebagai berikut:

1.  **`product_id`** (object): ID unik untuk setiap produk.
2.  **`product_name`** (object): Nama lengkap dari produk.
3.  **`category`** (object): Kategori produk, seringkali dalam format hierarki (misalnya, "Electronics|HomeTheater,TV&Video|Accessories|Cables").
4.  **`discounted_price`** (float64): Harga produk setelah diskon diterapkan (dalam mata uang Rupiah, setelah konversi tipe data).
5.  **`actual_price`** (float64): Harga asli produk sebelum diskon (dalam mata uang Rupiah, setelah konversi tipe data).
6.  **`discount_percentage`** (float64): Persentase diskon yang diterapkan pada produk (dalam desimal, setelah konversi tipe data).
7.  **`rating`** (float64): Rating rata-rata produk (setelah konversi tipe data).
8.  **`rating_count`** (float64): Jumlah total ulasan atau rating yang diterima produk (setelah konversi tipe data).
9.  **`about_product`** (object): Deskripsi singkat mengenai fitur atau keunggulan produk.
10. **`user_id`** (object): ID pengguna yang memberikan ulasan. (Perlu dicatat bahwa satu baris bisa berisi multiple user IDs, yang menunjukkan data agregasi ulasan, bukan ulasan individual).
11. **`user_name`** (object): Nama pengguna yang memberikan ulasan (sesuai dengan `user_id`).
12. **`review_id`** (object): ID unik untuk ulasan. (Seperti `user_id`, ini mungkin merepresentasikan sekumpulan ulasan).
13. **`review_title`** (object): Judul dari ulasan yang diberikan.
14. **`review_content`** (object): Isi atau teks dari ulasan yang diberikan.
15. **`img_link`** (object): Tautan (URL) ke gambar produk.
16. **`product_link`** (object): Tautan (URL) ke halaman produk di Amazon.

Selain itu, telah ditambahkan kolom baru sebagai hasil *feature engineering* awal:
*   **`rating_weighted`** (float64): Nilai rating yang diberi bobot berdasarkan jumlah ulasan (`rating` \* `rating_count`).
*   **`main_category`** (object): Kategori utama produk, diekstrak dari kolom `category`.
*   **`sub_category`** (object): Sub-kategori produk, diekstrak dari kolom `category`.
*   **`combined_text` / `all_text_features`** (object): Gabungan teks dari kolom `product_name`, `category`, `about_product`, dan `review_content` untuk keperluan analisis teks.

### Exploratory Data Analysis (EDA) dan Insights

Beberapa tahapan EDA telah dilakukan untuk mendapatkan wawasan mendalam tentang data:

1.  **Distribusi Kategori:**
<p align="center">
  <img src="https://github.com/user-attachments/assets/cf28819c-bacc-4cfc-bb7b-0993c3d6d99e" alt="Gambar 1. Distribusi produk pada kategori utama" width="500"/>
</p>

<p align="center"><strong>Gambar 1.</strong> Distribusi produk pada kategori utama</p>

- Analisis menunjukkan bahwa dataset didominasi oleh kategori **Electronics**, **Computers & Accessories**, dan **Home & Kitchen**. Kategori lain memiliki jumlah produk yang jauh lebih sedikit.
- Visualisasi bar plot dari 10 kategori utama teratas mengkonfirmasi dominasi tiga kategori tersebut.
-  **Insight:** Sistem rekomendasi mungkin akan lebih efektif atau memiliki lebih banyak data untuk dilatih pada produk di kategori-kategori dominan ini. Kategori dengan sedikit data mungkin mengalami *cold start* jika hanya menggunakan data rating.

---
2.  **Distribusi Sub-Kategori:**
<p align="center">
  <img src="https://github.com/user-attachments/assets/6ab96f2d-eb81-4052-9992-c6196e729c0b" alt="Gambar 2. Distribusi produk pada sub kategori" width="500"/>
</p>

<p align="center"><strong>Gambar 2.</strong> Distribusi produk pada sub kategori</p>

- Sub-kategori seperti **USB Cables**, **Smart Watches**, **Smartphones**, dan **Smart Televisions** memiliki jumlah produk terbanyak.
- Visualisasi bar plot dari 10 sub-kategori teratas menunjukkan pola serupa dengan kategori utama, di mana sub-kategori yang berkaitan dengan elektronik dan aksesorisnya sangat menonjol.
- **Insight:** Fokus rekomendasi berbasis konten pada sub-kategori ini akan memiliki kekayaan data tekstual yang tinggi.

---
3.  **Rata-rata Rating per Kategori/Sub-Kategori:**
<p align="center">
  <img src="https://github.com/user-attachments/assets/18701e2c-66d6-42c5-b3d0-ae5dd683af04" alt="Gambar 3.Rata-rata Rating per Kategori Utama" width="500"/>
</p>

<p align="center"><strong>Gambar 3.</strong> Rata-rata Rating per Kategori Utama</p>


<p align="center">
  <img src="https://github.com/user-attachments/assets/89962afe-382c-49f9-a060-6ea3d275e182" alt="Gambar 4.Rata-rata Rating per Sub Kategori" width="500"/>
</p>

<p align="center"><strong>Gambar 4.</strong> Rata-rata Rating per Sub Kategori</p>

 - Meskipun kategori seperti Electronics memiliki banyak produk, kategori dengan rata-rata rating tertinggi justru adalah **Office Products**, **Toys & Games**, dan **Home Improvement** (untuk kategori utama).
- Untuk sub-kategori, **Tablets** memiliki rata-rata rating tertinggi, diikuti oleh beberapa sub-kategori aksesori dan perlengkapan spesifik.
- Visualisasi bar plot menunjukkan perbandingan rata-rata rating antar kategori/sub-kategori.
- **Insight:** Popularitas (jumlah produk) tidak selalu berkorelasi langsung dengan kepuasan pengguna (rata-rata rating). Kategori atau sub-kategori dengan jumlah produk sedikit bisa jadi memiliki produk-produk berkualitas tinggi yang sangat disukai. Informasi rata-rata rating ini penting untuk mengevaluasi kualitas produk dalam suatu kelompok.

---
4.  **Produk dengan Rating Tertimbang (Rating\_weighted) Tertinggi:**

Tabel 1. Daftar Produk dengan Rating terbanyak.
| main_category          | sub_category            | rating | rating_count | rating_weighted |
|------------------------|-------------------------|--------|---------------|------------------|
| Computers&Accessories  | Webcams                 | 4.3    | 20398         | 87711.4          |
| Computers&Accessories  | PCMicrophones           | 3.9    | 14969         | 58379.1          |
| Computers&Accessories  | Webcams                 | 4.1    | 10976         | 45001.6          |
| Computers&Accessories  | PCSpeakers              | 4.0    | 7352          | 29408.0          |
| Computers&Accessories  | PCHeadsets              | 3.5    | 7222          | 25277.0          |
| Computers&Accessories  | PCSpeakers              | 4.1    | 5195          | 21299.5          |
| Computers&Accessories  | USBtoUSBAdapters        | 4.3    | 4426          | 19031.8          |
| Computers&Accessories  | PCMicrophones           | 3.3    | 2804          | 9253.2           |
| Computers&Accessories  | USBtoUSBAdapters        | 4.0    | 1540          | 6160.0           |
| Car&Motorbike          | AirPurifiers&Ionizers   | 3.8    | 1118          | 4248.4           |

- Daftar produk dengan `rating_weighted` tertinggi didominasi oleh produk dari kategori **Computers & Accessories** dan **Electronics**.
- `rating_weighted` memberikan skor yang menggabungkan rating dan jumlah ulasan, mengidentifikasi produk yang populer dan memiliki rating baik.
- **Insight:** Produk-produk ini adalah kandidat kuat untuk direkomendasikan sebagai produk unggulan atau "best-sellers" dalam kategori mereka.

---
5.  **Rata-rata Persentase Diskon:**
<p align="center">
  <img src="https://github.com/user-attachments/assets/98c91303-4d92-44a2-a163-34fe98b5c570" alt="Gambar 5. Rata-rata Persentase Diskon per Kategori Utama" width="500"/>
</p>

<p align="center"><strong>Gambar 5.</strong>  Rata-rata Persentase Diskon per Kategori Utama</p>


<p align="center">
  <img src="https://github.com/user-attachments/assets/4e232b6b-32ec-42a0-a5f3-0fcfb92ddd69" alt="Gambar 6. Rata-rata Persentase Diskon per Sub Kategori" width="500"/>
</p>

<p align="center"><strong>Gambar 6.</strong>  Rata-rata Persentase Diskon per Sub Kategori</p>

- Kategori seperti **Home Improvement**, **Computers & Accessories**, dan **Health & Personal Care** memiliki rata-rata persentase diskon tertinggi.
- Sub-kategori dengan diskon rata-rata tertinggi seringkali adalah aksesoris kecil (misalnya, Cable Connection Protectors, Earpads) dengan diskon mencapai 90%.
- Visualisasi bar plot menunjukkan rata-rata diskon per kategori/sub-kategori.
- **Insight:** Informasi diskon dapat menjadi fitur tambahan yang menarik untuk dipertimbangkan dalam model rekomendasi, atau digunakan untuk filter produk berbasis promosi. Kategori/sub-kategori tertentu secara strategis diberi diskon lebih besar.

---
6.  **Statistik Deskriptif Numerik:**

Tabel 2. Statistik Deskriptif untuk Kolom-Kolom Numerik

| Statistic | discounted_price | actual_price | discount_percentage | rating | rating_count | rating_weighted     |
|-----------|------------------|--------------|----------------------|--------|--------------|----------------------|
| Count     | 1462             | 1462         | 1462                 | 1462   | 1462         | 1462                |
| Mean      | 3129.98          | 5453.09      | 0.4767               | 4.10   | 18307.38     | 76265.01            |
| Std       | 6950.55          | 10884.47     | 0.2161               | 0.29   | 42766.10     | 180208.70           |
| Min       | 39.00            | 39.00        | 0.0000               | 2.00   | 2.00         | 4.00                |
| 25%       | 325.00           | 800.00       | 0.3200               | 4.00   | 1191.50      | 4766.20             |
| 50%       | 799.00           | 1670.00      | 0.5000               | 4.10   | 5179.00      | 21587.40            |
| 75%       | 1999.00          | 4321.25      | 0.6300               | 4.30   | 17342.25     | 71861.85            |
| Max       | 77990.00         | 139900.00    | 0.9400               | 5.00   | 426973.00    | 1878681.00          |


- Analisis `describe()` pada kolom numerik (`discounted_price`, `actual_price`, `discount_percentage`, `rating`, `rating_count`, `rating_weighted`) menunjukkan sebaran nilai, rata-rata, median, standar deviasi, minimum, dan maksimum.
- Terlihat adanya nilai ekstrem pada kolom harga (`actual_price`, `discounted_price`) dan jumlah rating (`rating_count`, `rating_weighted`), yang menyebabkan perbedaan signifikan antara rata-rata dan median serta standar deviasi yang besar.
- **Insight:** Distribusi harga dan jumlah rating yang *skewed* perlu diperhatikan dalam pemodelan. Kolom `rating_weighted` sangat dipengaruhi oleh produk dengan jumlah ulasan sangat tinggi.

---
Seluruh tahapan EDA ini memberikan pemahaman yang komprehensif tentang karakteristik dataset, distribusi produk dan rating, serta potensi wawasan yang dapat digunakan untuk membangun dan mengevaluasi model sistem rekomendasi.


## Data Preparation

Pada tahap ini, data disiapkan agar bisa digunakan dalam proses machine learning atau analisis lanjutan. Langkah-langkah yang dilakukan meliputi: seleksi fitur, penggabungan teks, dan vektorisasi teks menggunakan TF-IDF (untuk Content-Based Filtering), serta langkah-langkah spesifik untuk Collaborative Filtering.

### Data Cleaning

Sebelum melakukan tahapan persiapan data yang lebih lanjut, beberapa langkah pembersihan data (data cleaning) telah dilakukan pada tahap Data Understanding untuk memastikan kualitas data. Tahapan ini meliputi:

1.  **Penanganan Missing Values:** Memeriksa dan menghapus baris yang memiliki nilai kosong (missing values) pada kolom `rating_count`.
2.  **Penanganan Nilai Tidak Konsisten:** Mengidentifikasi dan menghapus baris dengan nilai yang tidak biasa atau non-numerik (karakter '|') pada kolom `rating`.
3.  **Konversi Tipe Data:** Mengubah tipe data kolom `discounted_price`, `actual_price`, `discount_percentage`, `rating`, dan `rating_count` menjadi tipe numerik (`float64`) agar dapat diolah dalam perhitungan dan analisis.

Alasan mengapa tahapan data cleaning ini diperlukan adalah untuk:
*   Memastikan data yang digunakan bersih dan valid, menghindari *error* atau hasil yang bias saat analisis dan pemodelan.
*   Menstandardisasi format data, terutama untuk kolom numerik, agar siap untuk operasi matematika dan input model.

Saat melakukan pengecekan *missing values*, diketahui bahwa hanya kolom `rating_count` yang memiliki nilai yang hilang, yaitu sebanyak 2 data:

```
print("\n" + "="*50 + " Missing Values " + "="*50)
print(amazon.isnull().sum())
```

Hasilnya:

```
================================================== Missing Values ==================================================
product_id             0
product_name           0
category               0
discounted_price       0
actual_price           0
discount_percentage    0
rating                 0
rating_count           2
about_product          0
user_id                0
user_name              0
review_id              0
review_title           0
review_content         0
img_link               0
product_link           0
dtype: int64
```

Nilai yang hilang ini dapat dihapus menggunakan fungsi `drop` agar tidak mengganggu proses analisis. Selain pada fitur `rating_count`, ditemukan juga nilai tidak valid pada fitur `rating`, yaitu berupa karakter `'|'`:

```
================================================== Value Counts for Rating Column ==================================================
rating
4.1    244
4.3    230
4.2    228
4.0    129
3.9    123
4.4    123
3.8     86
4.5     75
4       52
3.7     42
3.6     35
3.5     26
4.6     17
3.3     16
3.4     10
4.7      6
3.1      4
4.8      3
5.0      2
3.2      2
2.8      2
3.0      2
2.3      1
|        1
2        1
3        1
2.6      1
2.9      1
Name: count, dtype: int64
```

Nilai yang tidak valid (misalnya `'|'`) dihapus agar tidak mempengaruhi analisis. Setelah proses pembersihan ini selesai dan pola data dapat dipahami dengan lebih baik, maka proses seleksi fitur, *encoding*, dan pengembangan model dapat dilanjutkan.


### Seleksi Fitur

Proses ini bertujuan untuk menyederhanakan dataset dengan hanya mengambil kolom-kolom yang relevan untuk model rekomendasi. Kolom-kolom yang tidak dibutuhkan secara langsung untuk perhitungan kemiripan konten atau interaksi pengguna-item (seperti harga, link gambar, nama user, dll.) dihapus agar fokus pada informasi penting.

Dalam proyek ini, kolom-kolom berikut dipertahankan untuk digunakan dalam proses selanjutnya: `product_id`, `product_name`, `category`, `rating`, `rating_count`, `about_product`, `user_id`, `review_content`, `rating_weighted`, `sub_category`, dan `main_category`. Kolom `user_id`, `product_id`, dan `rating` akan menjadi fokus untuk model Collaborative Filtering, sementara kolom tekstual dan kategori akan digunakan untuk Content-Based Filtering.

Alasan mengapa seleksi fitur diperlukan adalah untuk:
*   Mengurangi dimensi data, mempercepat proses komputasi.
*   Menghilangkan *noise* atau informasi yang tidak relevan yang dapat mengganggu kinerja model.
*   Memastikan bahwa model hanya menggunakan fitur-fitur yang paling informatif untuk tugas rekomendasi.


### Penggabungan Teks (untuk Content-Based Filtering)

Untuk model Content-Based Filtering yang akan menggunakan informasi tekstual produk, teks dari beberapa kolom yang relevan digabungkan menjadi satu kolom baru. Kolom yang digabungkan adalah `product_name`, `category`, `about_product`, dan `review_content`. Hasil penggabungan disimpan dalam kolom `combined_text` atau `all_text_features`. Selain itu, nilai-nilai yang mungkin hilang dalam kolom teks diisi dengan string kosong (`''`) untuk menghindari *error* saat pemrosesan teks.

Alasan penggabungan teks diperlukan adalah untuk:
*   Mengkonsolidasikan semua informasi tekstual yang relevan dari berbagai sumber (nama, deskripsi, ulasan, kategori) ke dalam satu representasi.
*   Memudahkan proses vektorisasi teks selanjutnya menggunakan teknik seperti TF-IDF.


### Vektorisasi Teks: TF-IDF (untuk Content-Based Filtering)

TF-IDF (Term Frequency-Inverse Document Frequency) adalah teknik yang digunakan untuk mengubah data teks yang telah digabungkan (`combined_text` atau `all_text_features`) menjadi representasi numerik dalam bentuk matriks. Matriks ini merepresentasikan seberapa penting sebuah kata (term) dalam sebuah dokumen (produk) relatif terhadap seluruh kumpulan dokumen.

Dalam implementasi, digunakan `TfidfVectorizer` dari library `sklearn.feature_extraction.text` dengan beberapa parameter:
*   `stop_words='english'`: Menghapus kata-kata umum dalam bahasa Inggris yang biasanya tidak memiliki makna diskriminatif.
*   `max_features=5000`: Membatasi jumlah fitur (kata unik) yang dipertimbangkan menjadi 5000 teratas berdasarkan skor TF-IDF mereka.
*   `min_df=2`: Mengabaikan kata-kata yang muncul di kurang dari 2 dokumen.
*   `max_df=0.8`: Mengabaikan kata-kata yang muncul di lebih dari 80% dokumen.

Output dari proses ini adalah matriks TF-IDF (`tfidf_matrix` atau `tfidf_matrix_features`) dengan bentuk (jumlah dokumen, jumlah fitur) yang siap digunakan untuk menghitung kemiripan antar produk.

Alasan mengapa vektorisasi teks dengan TF-IDF diperlukan adalah untuk:
*   Mengubah data teks yang tidak terstruktur menjadi format numerik yang dapat diproses oleh algoritma machine learning.
*   Menangkap pentingnya kata kunci dalam setiap produk, yang akan digunakan sebagai dasar untuk menghitung kemiripan konten antar produk.

---

## Persiapan Data untuk Collaborative Filtering

Bagian ini menjelaskan langkah-langkah spesifik yang dilakukan untuk menyiapkan data rating agar bisa digunakan dalam membangun model Collaborative Filtering berbasis Neural Network (RecommenderNet).

1.  **Pemilihan Data Rating:**
    Langkah pertama adalah memfilter dataset utama (`amazon`) untuk hanya mengambil kolom-kolom yang relevan untuk model Collaborative Filtering, yaitu `user_id`, `product_id`, dan `rating`. Data ini disimpan dalam DataFrame baru (misalnya, `rating_data`). Ini adalah data interaksi pengguna dengan produk yang akan dipelajari oleh model.

2.  **Encoding ID Pengguna dan Produk:**
    Model neural network membutuhkan input dalam bentuk indeks numerik. Oleh karena itu, `user_id` dan `product_id` yang awalnya berupa string unik diubah menjadi representasi numerik (indeks) yang berurutan (misalnya, 0, 1, 2, ...). Proses ini melibatkan pembuatan daftar ID unik untuk pengguna dan produk, lalu membuat kamus (dictionary) untuk memetakan ID asli ke indeks numerik, dan sebaliknya. Kolom-kolom baru (`user_encoded`, `product_encoded`) ditambahkan ke DataFrame data rating untuk menyimpan indeks ini.

3.  **Normalisasi Nilai Rating:**
    Nilai rating asli dalam dataset memiliki rentang tertentu (misalnya, dari 2.0 hingga 5.0). Untuk model neural network yang menggunakan fungsi aktivasi Sigmoid pada lapisan outputnya (Sigmoid menghasilkan nilai antara 0 dan 1), nilai rating target perlu dinormalisasi ke dalam rentang yang sama. Normalisasi Min-Max (`(rating - min_rating) / (max_rating - min_rating)`) digunakan untuk mengubah rating asli menjadi nilai antara 0 dan 1. Kolom baru (`normalized_rating`) ditambahkan ke DataFrame data rating untuk menyimpan nilai yang sudah dinormalisasi ini.

4.  **Pembagian Dataset (Train-Validation Split):**
    Data rating yang sudah disiapkan (dengan kolom `user_encoded`, `product_encoded`, dan `normalized_rating`) kemudian dibagi menjadi dua set: data latih (training set) dan data validasi (validation set). Umumnya, data dibagi dengan proporsi tertentu (misalnya, 80% untuk training dan 20% untuk validation). Data training digunakan untuk melatih model, sedangkan data validation digunakan untuk mengevaluasi kinerja model selama pelatihan dan menyetel hyperparameter. Pembagian ini penting untuk memastikan bahwa model dapat menggeneralisasi dengan baik ke data baru dan mencegah *overfitting*.

Alasan mengapa langkah-langkah persiapan data khusus ini diperlukan untuk Collaborative Filtering adalah untuk:
* Menyediakan data interaksi pengguna-produk dalam format yang sesuai (indeks numerik dan rating ternormalisasi) sebagai input untuk arsitektur neural network.
* Mempersiapkan data untuk proses pelatihan model yang efisien dan efektif, serta memungkinkan evaluasi yang objektif terhadap kinerja model pada data yang belum pernah dilihat.


## Modeling and Result

Pada tahap ini, dua model sistem rekomendasi dibangun untuk mengatasi permasalahan *information overload* dan meningkatkan pengalaman pengguna di platform e-commerce: **Content-Based Filtering** dan **Collaborative Filtering**.

### 1. Content-Based Filtering

Content-based filtering adalah metode yang digunakan dalam sistem rekomendasi dan analisis data yang berfokus pada karakteristik atau konten dari item-item yang ingin direkomendasikan atau dianalisis. Pendekatan ini menggunakan atribut-atribut atau fitur-fitur item untuk menentukan kesamaan antara item yang ada dan preferensi pengguna. Dalam konteks rekomendasi, content-based filtering berusaha untuk merekomendasikan item yang mirip dengan item yang telah disukai oleh pengguna berdasarkan karakteristik konten [[4](https://dqlab.id/content-based-filtering-dalam-algoritma-data-science)].

<p align="center">
  <img src="https://github.com/user-attachments/assets/30b99454-8825-44a6-82e7-7a3cac1082e4" alt="Gambar 7. Content-Based Filtering" width="500"/>
</p>

<p align="center"><strong>Gambar 7.</strong>  Content-Based Filtering</p>


Model Content-Based Filtering merekomendasikan produk berdasarkan kemiripan konten antar produk.

*   **Teknik yang Digunakan:**
    *   **TF-IDF (Term Frequency-Inverse Document Frequency):** Digunakan untuk mengubah teks gabungan dari fitur produk (`product_name`, `category`, `about_product`, `review_content`) menjadi representasi numerik dalam bentuk matriks TF-IDF. Matriks ini memiliki bentuk (jumlah produk unik, jumlah fitur teks), di mana setiap nilai merepresentasikan pentingnya sebuah kata dalam sebuah produk relatif terhadap seluruh dataset.
    *   **Cosine Similarity:** Setelah matriks TF-IDF diperoleh, Cosine Similarity dihitung antara semua pasangan produk. Hasilnya adalah matriks persegi (jumlah produk unik x jumlah produk unik) yang menyimpan skor kemiripan konten antara setiap produk dengan produk lainnya.

*   **Cara Kerja Model:**
    Ketika pengguna melihat atau berinteraksi dengan suatu produk, model akan menggunakan matriks Cosine Similarity untuk mencari produk lain yang memiliki skor kemiripan tertinggi dengan produk tersebut. Produk-produk dengan skor kemiripan tertinggi (dan belum pernah dilihat/diulas oleh pengguna) akan direkomendasikan.

*   **Output Top-N Recommendation:**
    Model ini menghasilkan daftar Top-N rekomendasi produk yang paling mirip secara konten dengan produk referensi. Contoh output rekomendasi berdasarkan nama produk atau product ID telah ditampilkan di notebook, menunjukkan produk-produk dengan kategori atau deskripsi yang serupa. Dilakukan Rekomendasi Berdasarkan Nama Produk dan Rekomendasi Berdasarkan Product diproleh saat melakukan Testing Rekomendasi

    
Tabel 3. Rekomendasi berdasarkan nama produk

Recommendations for: AmazonBasics Flexible Premium HDMI Cable (Black, 4K@60Hz, 18Gbps), 3-Foot

| product_id | product_name                                                        | category                                                         | about_product                                                                 | sub_category | combined_features                                                        | similarity_score |
|------------|----------------------------------------------------------------------|-------------------------------------------------------------------|--------------------------------------------------------------------------------|--------------|---------------------------------------------------------------------------|------------------|
| B01M4GGIVU | Tizum High Speed HDMI Cable with Ethernet \| Supports Full HD, 3D... | Electronics\|HomeTheater,TV&Video\|Accessories\|Cables            | Latest Standard HDMI A Male to A Male Cable: Supports Ethernet, 3D, 4K Video  | HDMICables    | Tizum High Speed HDMI Cable with Ethernet \| Supports Full HD, 3D... | 0.617830         |
| B014I8SSD0 | Amazon Basics High-Speed HDMI Cable, 6 Feet - Black                  | Electronics\|HomeTheater,TV&Video\|Accessories\|Cables            | Please select appropriate display resolution & refresh rate for best results  | HDMICables    | Amazon Basics High-Speed HDMI Cable, 6 Feet - Black                  | 0.608048         |
| B014I8SX4Y | Amazon Basics High-Speed HDMI Cable, 6 Feet (2 Pack) - Black         | Electronics\|HomeTheater,TV&Video\|Accessories\|Cables            | HDMI A Male to A Male Cable: Supports Ethernet, 3D, 4K Video and Audio Return | HDMICables    | Amazon Basics High-Speed HDMI Cable, 6 Feet (2 Pack) - Black         | 0.590813         |
| B00GG59HU2 | BlueRigger High Speed HDMI Cable with Ethernet (6 Feet)              | Electronics\|HomeTheater,TV&Video\|Accessories\|Cables            | [Premium Cable] - High-Speed HDMI Cables. Made with 100% pure copper conductors | HDMICables    | BlueRigger High Speed HDMI Cable with Ethernet (6 Feet)              | 0.577854         |
| B075ZTJ9XR | AmazonBasics High-Speed Braided HDMI Cable - 3 Feet                  | Electronics\|HomeTheater,TV&Video\|Accessories\|Cables            | Nylon-braided HDMI cable (A Male to A Male): supports 4K video, Ethernet, ARC | HDMICables    | AmazonBasics High-Speed Braided HDMI Cable - 3 Feet                  | 0.571482         |




Tabel 4. Rekomendasi berdasarkan product ID

Sample product ID: B07JW9H4J1

Reference product details:
| product_id | product_name                                                   | category                                                            | sub_category |
|------------|----------------------------------------------------------------|---------------------------------------------------------------------|--------------|
| B07JW9H4J1 | Wayona Nylon Braided USB to Lightning Fast Charging Cable...   | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables    |

Recommended products:
| product_id | product_name                                                 | category                                                            | sub_category | combined_features                                               |
|------------|--------------------------------------------------------------|----------------------------------------------------------------------|----------------|------------------------------------------------------------------|
| B07JH1CBGW | Wayona Nylon Braided Usb Syncing And Charging ...           | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables      | Wayona Nylon Braided Usb Syncing And Charging ...              |
| B07JW1Y6XV | Wayona Nylon Braided 3A Lightning to USB A Syn...            | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables      | Wayona Nylon Braided 3A Lightning to USB A Syn...              |
| B07JH1C41D | Wayona Nylon Braided (2 Pack) Lightning Fast U...           | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables      | Wayona Nylon Braided (2 Pack) Lightning Fast U...             |
| B07LGT55SJ | Wayona Usb Nylon Braided Data Sync And Chargin...           | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables      | Wayona Usb Nylon Braided Data Sync And Chargin...             |
| B07JPJJZ2H | Wayona Nylon Braided Lightning USB Data Sync &...           | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables      | Wayona Nylon Braided Lightning USB Data Sync &...             |
| B07JGDB5M1 | Wayona Nylon Braided 2M / 6Ft Fast Charge Usb ...           | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables      | Wayona Nylon Braided 2M / 6Ft Fast Charge Usb ...             |
| B095244Q22 | MYVN LTG to USB for Fast Charging & Data Sync ...           | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables      | MYVN LTG to USB for Fast Charging & Data Sync ...             |
| B07JNVF678 | Wayona Nylon Braided USB Data Sync and Fast Ch...           | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables      | Wayona Nylon Braided USB Data Sync and Fast Ch...             |
| B0B2DJDCPX | SWAPKART Fast Charging Cable and Data Sync USB...           | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables      | SWAPKART Fast Charging Cable and Data Sync USB...             |
| B0B8SSC5D9 | AmazonBasics USB C to Lightning Aluminum with ...           | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables      | AmazonBasics USB C to Lightning Aluminum with ...             |


*   **Kelebihan Pendekatan Content-Based Filtering [[5](https://mti.binus.ac.id/2023/05/31/sistem-rekomendasi-dengan-content-based/)]**:
    *   Solusi Cold-Start untuk Produk Baru: Mampu merekomendasikan item baru secara efektif selama informasi deskriptif produk tersedia, tanpa memerlukan riwayat interaksi pengguna sebelumnya.
    *   Transparansi Rekomendasi: Logika rekomendasi dapat dijelaskan secara jelas melalui fitur-fitur produk yang digunakan, meningkatkan kepercayaan pengguna terhadap sistem.
    *   Personalisasi Tinggi: Rekomendasi bersifat independen dari perilaku pengguna lain, memungkinkan personalisasi yang spesifik berdasarkan profil pengguna individu.
    *   Kemampuan Interpretasi: Sistem dapat menyajikan daftar karakteristik produk yang menjadi dasar rekomendasi, memperkuat transparansi dan akuntabilitas.
    *   Skalabilitas: Memiliki performa yang stabil terhadap pertumbuhan jumlah pengguna karena tidak memerlukan data kolaboratif.
    *   Fleksibilitas untuk Niche Market: Dapat menangani kasus khusus dimana pengguna memiliki preferensi unik yang jarang ditemui pada populasi umum.
    *   Keamanan Sistem: Lebih resisten terhadap serangan manipulasi rekomendasi (shilling attacks) dan mencegah penyebaran konten viral yang tidak diinginkan.
      

*   **Kekurangan Pendekatan Content-Based Filtering [[5](https://mti.binus.ac.id/2023/05/31/sistem-rekomendasi-dengan-content-based/)]**:
    *   Efek Filter Bubble: Cenderung menghasilkan rekomendasi homogen yang terbatas pada preferensi historis pengguna, mengurangi kesempatan untuk menemukan item di luar pola konsumsi yang ada.
    *   Ketergantungan pada Kualitas Konten: Memerlukan metadata produk yang lengkap dan deskriptif. Rekomendasi menjadi tidak optimal jika deskripsi produk terlalu singkat, terdapat ketidakonsistenan terminologi, dan informasi fitur produk tidak terstruktur.
    *   Kompleksitas Pemrosesan Konten: Menghadapi tantangan teknis dalam Ekstraksi fitur dari data tidak terstruktur (teks bebas), Normalisasi terminologi produk, dan Penanganan multibahasa.
    *   Skalabilitas Operasional: Proses matching memerlukan komputasi intensif ketika Jumlah produk sangat besar (>1 juta SKU), Update katalog frekuen tinggi, dan Memproses query real-time.
    *   Masalah Over-Specialization: Dampak negatif yang muncul yaitu Kurangnya variasi dalam rekomendasi, Kesulitan memperkenalkan produk baru (low serendipity), dan Potensi bias terhadap produk populer.
    *   Limitasi Profil Pengguna: Keterbatasan dalam pemodelan preferensi yaitu Profil statis tidak menangkap evolusi minat, Pengguna berbeda bisa memiliki profil serupa, dan Kesulitan menangkap preferensi implisit.

---
### 2. Collaborative Filtering

Collaborative Filtering adalah salah satu algoritma dalam data science yang digunakan untuk memberikan rekomendasi kepada pengguna berdasarkan data historis tentang preferensi pengguna lain. Metode ini beroperasi dengan mengidentifikasi pengguna yang memiliki preferensi atau perilaku serupa dengan pengguna yang ingin menerima rekomendasi, dan kemudian memberikan rekomendasi berdasarkan apa yang disukai oleh pengguna-pengguna serupa tersebut [[6](https://dqlab.id/collaborative-filtering-pada-algoritma-data-science)].

<p align="center">
  <img src="https://github.com/user-attachments/assets/16dcf416-cda4-4c08-bceb-0555192a1f49" alt="Gambar 8. Collaborative Filtering" width="500"/>
</p>

<p align="center"><strong>Gambar 8.</strong> Collaborative Filtering</p>


Model Collaborative Filtering memprediksi preferensi pengguna terhadap produk berdasarkan pola interaksi (rating) dari banyak pengguna.

*   **Teknik yang Digunakan:**
    *   **Encoding ID:** `user_id` dan `product_id` diubah menjadi indeks numerik untuk persiapan input model neural network.
    *   **Normalisasi Rating:** Nilai rating dinormalisasi ke dalam rentang 0-1 agar sesuai untuk output model dengan fungsi aktivasi Sigmoid.
    *   **Model-Based CF (RecommenderNet):** Digunakan arsitektur neural network (RecommenderNet) yang mempelajari *embedding* (representasi vektor berdimensi rendah) untuk setiap pengguna dan produk dari data rating. Model memprediksi rating yang dinormalisasi dengan menghitung dot product dari embedding pengguna dan produk, ditambah bias pengguna dan produk.
    *   **Train-Test Split:** Data interaksi dibagi menjadi set training (80%) dan validation (20%) untuk melatih dan mengevaluasi model.
    *   **Hyperparameter Tuning:** Dilakukan pengujian kombinasi `embedding_size` dan `learning_rate` untuk menemukan parameter model yang optimal berdasarkan nilai Validation RMSE terendah.
    *   **Training Model Final:** Model dilatih menggunakan set training dengan *hyperparameter* terbaik dan dievaluasi pada set validation, menggunakan metrik Root Mean Squared Error (RMSE) dan Binary Crossentropy loss. Digunakan Early Stopping untuk mencegah *overfitting*.

*   **Cara Kerja Model:**
    Setelah model dilatih, untuk merekomendasikan produk kepada pengguna tertentu, model akan memprediksi potensi rating pengguna tersebut untuk semua produk yang belum pernah diberi rating. Produk-produk dengan prediksi rating tertinggi akan menjadi rekomendasi utama.

*   **Output Top-N Recommendation:**
    Model Collaborative Filtering yang telah dilatih digunakan untuk memprediksi potensi rating pengguna terhadap produk-produk yang belum pernah mereka interaksikan. Berdasarkan prediksi ini, sistem kemudian menghasilkan daftar Top-N produk yang diprediksi paling disukai oleh pengguna.
    
1. **Generating Recommendations**: Tahap ini menunjukkan proses utama menghasilkan rekomendasi untuk pengguna spesifik. Model menggunakan embedding yang dipelajari untuk memprediksi rating produk yang belum diulas, lalu menampilkan produk dengan prediksi rating tertinggi. Output dari proses ini dapat dilihat pada Tabel 5, yang menampilkan contoh 10 produk teratas yang direkomendasikan untuk seorang pengguna sampel, lengkap dengan detail nama dan kategori produk.

Tabel 5. Top 10 Rekomendasi Produk Berdasarkan Model Collaborative Filtering

Recommendations for user 
AHXVJ4RECEDVRCX2R7BYOMRO7KJQ,AEUNZGZ7IQFCJEFHU647HB57FC2Q,AEUWYI55HVW2GO4GRLWK4PWCTPLQ,AEDRDM7OTIWIAOWELAEAITODC4EA,AEDZ4OLR66LZO57XWMR6F43K736A,AEIXRXVWCR62IELG44BI5F7ZZUSQ,AFMCGE5U34NNKT2AGRY5TPX4OHKQ,AEFVX5GYQ6Y5MQSA25IP2FM2ZKTA:

| product_id | product_name                                                   | category                                                            | sub_category         |
|------------|----------------------------------------------------------------|---------------------------------------------------------------------|----------------------|
| B08CF3B7N1 | Portronics Konnect L 1.2M Fast Charging 3A 8 Pin USB Cable     | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables            |
| B09C6HXFC1 | Duracell USB Lightning Apple Certified (Mfi) Braided Cable     | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables            |
| B01M4GGIVU | Tizum High Speed HDMI Cable with Ethernet                      | Electronics\|HomeTheater,TV&Video\|Accessories\|Cables              | HDMICables           |
| B09W5XR9RT | Duracell USB C To Lightning Apple Certified (Mfi) Cable        | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables            |
| B01GGKYKQM | Amazon Basics USB Type-C to USB-A 2.0 Male Fast Charging Cable | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables            |
| B0BMXMLSMM | Lapster 65W Compatible for OnePlus Dash Warp Charging Cable    | Computers&Accessories\|Accessories&Peripherals\|Cables              | USBCables            |
| B00P93X6EK | Classmate Soft Cover 6 Subject Spiral Binding Notebook         | OfficeProducts\|OfficePaperProducts\|Paper\|Stationery              | WireboundNotebooks   |
| B08LT9BMPP | Logitech G102 USB Light Sync Gaming Mouse                      | Computers&Accessories\|Accessories&Peripherals\|InputDevices        | GamingMice           |
| B0BR4F878Q | Swiffer Instant Electric Water Heater Faucet Tap               | Home&Kitchen\|Heating,Cooling&AirQuality\|WaterHeaters              | InstantWaterHeaters  |
| B09P1MFKG1 | Melbon VM-905 2000-Watt Room Heater (ISI Certified)            | Home&Kitchen\|Heating,Cooling&AirQuality\|RoomHeaters               | FanHeaters           |
---

2. **Evaluasi Tambahan**: Bagian ini memberikan konteks tambahan untuk rekomendasi yang dihasilkan. Selain menampilkan Top-N rekomendasi produk (seperti pada tahap 'Generating Recommendations'), bagian ini juga menunjukkan produk-produk yang sebelumnya telah diberi rating tinggi oleh pengguna sampel. Hal ini memungkinkan perbandingan kualitatif antara rekomendasi model dengan preferensi historis pengguna. Output dari evaluasi tambahan ini disajikan dalam Tabel 6 dan Tabel 7, yang terbagi menjadi dua bagian: daftar produk dengan rating tinggi dari pengguna sampel, diikuti oleh daftar 10 produk teratas yang direkomendasikan oleh model untuk pengguna tersebut.

Showing recommendations for user: AHSGCVKHDAXRUG4R7V3RB6WYLZCQ,AHFTHBS5KCQWNQIYBUXWLMS6VJNA,AGQAZKHJRJ44EBAFG5NLJWB6VORA,AHZO434YNBOOY33A2IHP3RCV6FOQ,AGNUIVLVQZXACC7UBK6KUYONSKFQ,AFHTHDZC4BOFGJAGPN5EGVLT76NQ,AGR7ZWKS6IANTUZJ26FNMG74IUOA,AF2NMGMO6GOFFYU3TYVZYX6KU25Q

Tabel 6. Produk dengan rating tinggi dari user

| product_id | product_name                                                   | category                                                             | discounted_price | actual_price | discount_percentage | rating | rating_count | about_product                                               | user_id                                                | user_name                                    | review_id                                              | review_title                                  | review_content                                       | img_link                                                                 | product_link                                                                 | rating_weighted | sub_category      | main_category |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|------------------|--------------|----------------------|--------|--------------|-------------------------------------------------------------|---------------------------------------------------------|----------------------------------------------|--------------------------------------------------------|------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------|--------------------------------------------------------------------------------|------------------|-------------------|----------------|
| B0756KCV5K | Prestige PIC 15.0+ 1900-Watt Induction Cooktop                 | Home&Kitchen\|Kitchen&HomeAppliances\|SmallKitchenAppliances         | 3180.0           | 5295.0       | 0.4                  | 4.2    | 6919.0       | Concealed and feather touch buttons\|Anti magnetic wall    | AHSGCVKHDAXRUG4R7V3RB6WYLZCQ,AHFTHBS5KCQWNQIYB...       | ASHFAK KHAN,Uday,Amazon Customer,Birendra Rai,... | R2QMIAMI841PRB,R13ESBS8Z3WZG0,RZ8HXGE2HU1O,R39... | Bad servisec,a bit costly,Favourite,Thankyou a... | Work nahi kar raha sahi karwane ke liye call n... | https://m.media-amazon.com/images/I/41jv4fqU1E... | https://www.amazon.in/Prestige-PIC-15-0-1900-W... | 29059.8         | InductionCooktop | Home&Kitchen  |


Tabel 7. Top 10 Rekomendasi Produk
| product_name                                                   | category                                                            | rating |
|----------------------------------------------------------------|---------------------------------------------------------------------|--------|
| Belkin USB C to USB-C Fast Charging Type C Cable               | Computers&Accessories\|Accessories&Peripherals\|Cables              | 4.5    |
| Duracell USB Lightning Apple Certified (Mfi) Braided Cable     | Computers&Accessories\|Accessories&Peripherals\|Cables              | 4.5    |
| Duracell USB C To Lightning Apple Certified (Mfi) Cable        | Computers&Accessories\|Accessories&Peripherals\|Cables              | 4.4    |
| MI Braided USB Type-C Cable for Charging Adapter               | Computers&Accessories\|Accessories&Peripherals\|Cables              | 4.4    |
| Agaro Blaze USBA to micro +Type C 2in1 Braided Cable           | Computers&Accessories\|Accessories&Peripherals\|Cables              | 4.3    |
| TATA SKY HD Connection with 1 month basic pack                 | Electronics\|HomeTheater,TV&Video\|SatelliteEquipment               | 4.3    |
| Portronics Konnect L 1.2M Fast Charging 3A 8 Pin USB Cable     | Computers&Accessories\|Accessories&Peripherals\|Cables              | 4.2    |
| Wayona Nylon Braided USB to Lightning Fast Charging Cable      | Computers&Accessories\|Accessories&Peripherals\|Cables              | 4.2    |
| Tizum High Speed HDMI Cable with Ethernet                      | Electronics\|HomeTheater,TV&Video\|Accessories\|Cables              | 4.2    |
| Storite High Speed Micro USB 3.0 Cable A to Micro B            | Computers&Accessories\|Accessories&Peripherals\|Cables              | 4.2    |


*   **Kelebihan Pendekatan Collaborative Filtering: [[7](https://leravio.com/blog/collaborative-filtering-pengertian-kelebihan-dan-cara-kerjanya/)]**
    *   Penemuan Pola Tersembunyi: Mengidentifikasi hubungan non-intuitif antar item (misal: produk dari kategori berbeda yang sering dibeli bersama) dan Menangkap preferensi implisit pengguna yang tidak terlihat dari metadata produk.
    *   Meningkatkan Serendipity: Memungkinkan rekomendasi yang mengejutkan namun relevan berdasarkan Perilaku pengguna dengan profil serupa dan Pola co-purchasing/co-viewing.
    *   Independensi dari Konten Produk: Tetap efektif meskipun Deskripsi produk minim, Metadata tidak terstruktur, dan Konten sulit dianalisis (misal: produk kreatif/subjektif).
    *   Adaptabilitas Dinamis: Secara otomatis menyesuaikan dengan Perubahan tren pasar, Evolusi preferensi pengguna, dan Musim atau event khusus.


*   **Kekurangan Pendekatan Collaborative Filtering: [[7](https://leravio.com/blog/collaborative-filtering-pengertian-kelebihan-dan-cara-kerjanya/)]**
    *   Cold Start Problem: Tantangan utama pada skenario Pengguna baru yaitu Minim data interaksi dan Item baru sehingga Belum ada riwayat rating.
    *   Solusi potensial dengan Hybrid dengan content-based dan Demographic filtering awal.
    *   Ketergantungan Data Interaksi: Membutuhkan volume signifikan untuk User-user similarity (min. 20 interaksi/user) dan Item-item correlation (min. 50 interaksi/item).
    *   Data Sparsity: Masalah umum ketika Rasio interaksi/katalog < 0.1% dan Distribusi interaksi sangat skewed. Sehingga dampak yang terjadi yaitu akurasi menurun dan coverage terbatas.
    *   Black Box Effect: Kesulitan dalam Explainability rekomendasi, Debugging bias, dan Compliance regulasi.
    *   Vulnerabilitas Manipulasi: Risiko yaitu Shilling attacks, Viral bias, dan Amplifikasi popularitas.

---
Dengan mengimplementasikan kedua pendekatan ini, sistem rekomendasi yang dibangun menawarkan solusi yang komprehensif, memanfaatkan baik informasi konten produk maupun pola perilaku pengguna, untuk memberikan rekomendasi yang relevan dan personal.


## Evaluation

Tahap evaluasi bertujuan untuk mengukur kinerja model sistem rekomendasi yang telah dibangun. Pemilihan metrik evaluasi disesuaikan dengan konteks data (rating produk) dan tujuan proyek (memprediksi preferensi pengguna). Untuk model Collaborative Filtering yang memprediksi nilai rating, metrik yang umum dan sesuai adalah Root Mean Squared Error (RMSE) dan Binary Crossentropy.


### Root Mean Squared Error (RMSE)
Root Mean Squared Error (RMSE) merupakan salah satu cara untuk mengevaluasi model regresi linear dengan mengukur tingkat akurasi hasil perkiraan suatu model. RMSE dihitung dengan mengkuadratkan error (prediksi “ observasi) dibagi dengan jumlah data (= rata-rata), lalu diakarkan. RMSE tidak memiliki satuan. Root Mean Square Error merupakan salah satu kriteria dalam menentukan model peramalan selain MAPE, MAD dan MSE. Nilai RMSE rendah menunjukkan bahwa variasi nilai yang dihasilkan oleh suatu model prakiraan mendekati variasi nilai observasinya. RMSE menghitung seberapa berbedanya seperangkat nilai. Semakin kecil nilai RMSE, semakin dekat nilai yang diprediksi dan diamati [[8](https://dqlab.id/kriteria-jenis-teknik-analisis-data-dalam-forecasting)].


$$
\text{RMSE} = \sqrt{ \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 }
$$

Dimana:
* $$y_i$$ adalah nilai aktual ke-i, 
* $$\hat{y}_i$$ adalah nilai prediksi ke-i, 
* $$n$$ adalah jumlah total data.

RMSE mengukur rata-rata kesalahan kuadrat antara nilai aktual dan prediksi, yang kemudian diakarkan untuk mendapatkan nilai dalam satuan yang sama dengan data asli.


*   **Cara Kerja:**
    RMSE mengukur rata-rata akar kuadrat dari perbedaan antara nilai prediksi dan nilai aktual. Metrik ini memberikan indikasi seberapa besar kesalahan prediksi model secara rata-rata. Nilai RMSE yang lebih rendah menunjukkan bahwa prediksi model lebih dekat dengan nilai aktual, yang berarti model memiliki kinerja yang lebih baik dalam memprediksi rating. Karena kuadrat dari perbedaan diambil, kesalahan yang besar akan memiliki dampak yang lebih signifikan pada RMSE dibandingkan kesalahan yang kecil.

### Binary Crossentropy (Loss Function)

Binary Cross-Entropy Loss digunakan untuk menghitung Loss Function pada model yang melakukan klasifikasi biner [[9](https://rifqimulyawan.com/kamus/loss-function/)]. Rumus ini dinyatakan sebagai:

$$
\text{Loss} = -\frac{1}{n} \sum_{i=1}^{n} \left( y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right)
$$

Dimana:
* $$n$$ adalah jumlah data, 
* $$y_i$$ adalah nilai aktual (0 atau 1), 
* $$\hat{y}_i$$ adalah nilai prediksi (nilai probabilitas antara 0 dan 1).


*   **Cara Kerja:**
    Binary Crossentropy adalah *loss function* yang digunakan selama proses pelatihan model. Meskipun bukan metrik evaluasi *stand-alone* untuk mengukur kinerja akhir model dalam konteks prediksi rating numerik (RMSE lebih cocok untuk itu), nilai *loss* pada data validasi (`val_loss`) penting untuk memantau konvergensi model dan mendeteksi *overfitting*. Model berusaha meminimalkan nilai Binary Crossentropy selama pelatihan. Nilai *loss* yang menurun pada data validasi menunjukkan bahwa model semakin baik dalam memprediksi probabilitas atau nilai target yang dinormalisasi.

### Hasil Proyek Berdasarkan Metrik Evaluasi

Pada model Collaborative Filtering (RecommenderNet), kinerja model dievaluasi menggunakan Root Mean Squared Error (RMSE) pada data training dan validation selama proses pelatihan dan hyperparameter tuning.

*   **Hasil Hyperparameter Tuning:**
    Proses tuning menguji beberapa kombinasi `embedding_size` dan `learning_rate`. Kombinasi parameter terbaik yang ditemukan adalah `embedding_size=50` dan `learning_rate=0.01`, yang menghasilkan **Validation RMSE terendah sebesar sekitar 0.1278**. Hal ini menunjukkan bahwa dengan kombinasi parameter ini, model memiliki tingkat kesalahan prediksi rating rata-rata yang paling rendah pada data yang belum pernah dilihat sebelumnya di antara opsi yang diuji.

*   **Hasil Training Model Final:**
    Model final dilatih menggunakan *hyperparameter* terbaik. Log pelatihan menunjukkan bagaimana nilai Training RMSE dan Validation RMSE berubah di setiap epoch. Dengan menggunakan *Early Stopping* yang memantau `val_root_mean_squared_error`, pelatihan dihentikan ketika nilai ini tidak menunjukkan perbaikan signifikan. Hasil akhir setelah *Early Stopping* (misalnya, pada epoch ke-8 dalam log yang ditampilkan) menunjukkan:
    *   Training RMSE: Sekitar 0.1393
    *   Validation RMSE: Sekitar 0.1722 (Perlu dicatat bahwa *Early Stopping* mengembalikan bobot terbaik, yang mungkin sesuai dengan epoch sebelum epoch terakhir yang ditampilkan jika *validation error* sempat naik kembali). Berdasarkan output tuning, nilai terbaik yang tercatat adalah **0.1278**.

Interpretasi hasil ini menunjukkan bahwa model Collaborative Filtering yang dibangun mampu memprediksi rating produk dengan tingkat kesalahan rata-rata yang relatif rendah pada data validasi (sekitar  0.1253 - 0.1722 pada skala rating 0-1 setelah normalisasi). Nilai RMSE yang lebih rendah mengindikasikan prediksi yang lebih akurat, yang merupakan indikator baik untuk sistem rekomendasi berbasis prediksi rating.

<p align="center">
  <img src="https://github.com/user-attachments/assets/27a3e708-4e1e-459c-85e5-8beae8d89263" alt="Gambar 9. Visualisasi Proses Pelatihan" width="500"/>
</p>

<p align="center"><strong>Gambar 9.</strong> Visualisasi Proses Pelatihan</p>


Untuk model Content-Based Filtering, evaluasi kualitatif dilakukan dengan memeriksa relevansi Top-N rekomendasi yang dihasilkan. Berdasarkan contoh output yang ditampilkan, model Content-Based berhasil merekomendasikan produk-produk yang memiliki kemiripan konten (nama, kategori, deskripsi) dengan produk referensi, yang sesuai dengan tujuan pendekatan ini. Metrik kuantitatif seperti Precision, Recall, atau F1-Score pada Top-N rekomendasi juga dapat digunakan untuk evaluasi yang lebih formal jika data interaksi biner (misalnya, 'klik' atau 'pembelian') tersedia dan relevan. Namun, dalam konteks dataset rating, pemeriksaan relevansi visual dari output rekomendasi adalah cara evaluasi yang umum dan memadai untuk menunjukkan fungsi model.

## Kesimpulan

Proyek ini berhasil membangun sistem rekomendasi produk menggunakan dataset penjualan dan ulasan dari Amazon dengan menerapkan dua pendekatan utama: Content-Based Filtering dan Collaborative Filtering. Melalui serangkaian tahapan yang komprehensif, mulai dari pemuatan dan pemahaman data hingga pemodelan dan evaluasi, sistem ini menunjukkan potensi untuk mengatasi masalah *information overload* di platform e-commerce.

Tahap **Data Understanding** memberikan wawasan penting mengenai struktur, kualitas, dan karakteristik data, termasuk distribusi kategori produk, rata-rata rating, dan pola diskon. Identifikasi nilai yang hilang dan tidak konsisten, serta pembersihan data yang dilakukan, memastikan dataset siap untuk pemodelan. Analisis distribusi rating dan diskon per kategori/sub-kategori juga memberikan *insight* berharga mengenai preferensi pengguna dan strategi promosi.

Pada tahap **Data Preparation**, data disiapkan melalui seleksi fitur yang relevan, penggabungan teks untuk fitur konten, dan vektorisasi teks menggunakan TF-IDF. Untuk model Collaborative Filtering, *user* dan *product ID* di-*encode* dan rating dinormalisasi, mempersiapkan data untuk input model berbasis neural network.

Dua model utama berhasil diimplementasikan:

1.  **Content-Based Filtering:** Model ini memanfaatkan representasi TF-IDF dari konten produk (nama, kategori, deskripsi, ulasan) dan menghitung Cosine Similarity untuk mengukur kemiripan antar item. Model ini efektif dalam merekomendasikan produk yang secara konten sangat mirip dengan produk yang diminati pengguna. Keunggulannya terletak pada kemampuannya merekomendasikan item baru dan transparansi rekomendasi, meskipun rentan terhadap *filter bubble*.
2.  **Collaborative Filtering:** Menggunakan pendekatan Model-Based dengan arsitektur neural network (RecommenderNet), model ini mempelajari *embedding* pengguna dan produk dari data rating untuk memprediksi potensi rating. Setelah melalui proses *hyperparameter tuning* dan pelatihan, model ini mampu memprediksi rating dengan Validation RMSE yang rendah (sekitar 0.1278), menunjukkan akurasi yang baik dalam memprediksi preferensi pengguna pada data yang belum pernah dilihat. Model ini unggul dalam menemukan pola tersembunyi dan memberikan rekomendasi *serendipitous*, namun menghadapi tantangan *cold start* untuk pengguna dan item baru.

**Evaluasi** model Collaborative Filtering menunjukkan kinerja yang baik dalam memprediksi rating, dengan RMSE sebagai metrik utama yang mengukur tingkat kesalahan prediksi. Visualisasi proses pelatihan juga membantu memantau konvergensi dan mendeteksi potensi *overfitting*. Sementara itu, evaluasi kualitatif pada model Content-Based Filtering melalui contoh Top-N rekomendasi menunjukkan bahwa model berhasil mengidentifikasi produk serupa berdasarkan kontennya.

Secara keseluruhan, proyek ini berhasil membangun fondasi yang kuat untuk sistem rekomendasi produk. Kedua pendekatan model yang diimplementasikan menawarkan cara yang berbeda namun saling melengkapi untuk merekomendasikan produk, yang dapat diintegrasikan atau digunakan secara terpisah tergantung pada skenario penggunaan. Hasil proyek ini memberikan bukti bahwa data interaksi dan konten produk dapat secara efektif dimanfaatkan untuk meningkatkan pengalaman pengguna dan potensi penjualan di platform e-commerce.

## Referensi

[1] Y. Prayuti, “Dinamika perlindungan hukum konsumen di era digital: Analisis hukum terhadap praktik e-commerce dan perlindungan data konsumen di Indonesia,” *Jurnal Interpretasi Hukum*, vol. 5, no. 1, pp. 903–913, 2024.

[2] A. Nurcahyadi, “Peran Content Marketing dalam Meningkatkan Loyalitas Pelanggan pada E-Commerce,” *Mutiara: Multidiciplinary Scientific Journal*, vol. 2, no. 7, pp. 632–639, 2024.

[3] Alphasoft, “Apa Manfaat Penggunaan Sistem E-Commerce Bagi Peningkatan Penjualan,” *Alphasoft Blog*, [Online]. Available: https://alphasoft.id/blog/bisnis-5/apa-manfaat-penggunaan-sistem-e-commerce-bagi-peningkatan-penjualan-146. [Accessed: 27-May-2025].

[4] DQLab, “Content-Based Filtering dalam Algoritma Data Science,” *DQLab*, [Online]. Available: https://dqlab.id/content-based-filtering-dalam-algoritma-data-science. [Accessed: 27-May-2025].

[5] BINUS MTI, “Sistem Rekomendasi dengan Content-Based,” *Program Studi Magister Teknik Informatika BINUS*, [Online]. Available: https://mti.binus.ac.id/2023/05/31/sistem-rekomendasi-dengan-content-based/. [Accessed: 27-May-2025].

[6] DQLab, “Collaborative Filtering pada Algoritma Data Science,” *DQLab*, [Online]. Available: https://dqlab.id/collaborative-filtering-pada-algoritma-data-science. [Accessed: 27-May-2025].

[7] Leravio, “Collaborative Filtering: Pengertian, Kelebihan, dan Cara Kerjanya,” *Leravio Blog*, [Online]. Available: https://leravio.com/blog/collaborative-filtering-pengertian-kelebihan-dan-cara-kerjanya/. [Accessed: 27-May-2025].

[8] DQLab, “Kriteria, Jenis, Teknik Analisis Data dalam Forecasting,” *DQLab*, [Online]. Available: https://dqlab.id/kriteria-jenis-teknik-analisis-data-dalam-forecasting. [Accessed: 27-May-2025].

[9] R. Mulyawan, “Loss Function,” *Rifqi Mulyawan Blog*, [Online]. Available: https://rifqimulyawan.com/kamus/loss-function/. [Accessed: 27-May-2025].


**---Ini adalah bagian akhir laporan---**



