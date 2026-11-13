<p align="center">
  <strong>Customer Segmentation and Product Association Analysis for Online Retail Business Optimization</strong>
</p><p align="center">
  <img src="https://img.shields.io/badge/Python-Data%20Mining-blue?logo=python" alt="Python">
  <img src="https://img.shields.io/badge/Clustering-K--Means-orange" alt="K-Means">
  <img src="https://img.shields.io/badge/Association%20Rules-FP--Growth-green" alt="FP-Growth">
  <img src="https://img.shields.io/badge/Framework-CRISP--DM-purple" alt="CRISP-DM">
</p>Customer Intelligence: RFM Clustering & Market Basket Analysis
1. Project Overview
Project ini menggabungkan dua teknik data mining, yaitu RFM (Recency, Frequency, Monetary) dengan K-Means Clustering dan Market Basket Analysis menggunakan algoritma FP-Growth.

Analisis dilakukan untuk memahami perilaku pelanggan pada bisnis retail online melalui pengelompokan pelanggan dan identifikasi produk yang sering dibeli dalam satu transaksi. Hasil analisis dapat menjadi dasar penyusunan strategi bisnis, seperti mempertahankan pelanggan, mengaktifkan kembali pelanggan yang tidak lagi bertransaksi, serta menyusun penawaran cross-selling dan product bundling.

Dataset yang digunakan adalah Online Retail II dari UCI Machine Learning Repository. Dataset ini mencakup transaksi retail online pada periode Desember 2009 hingga Desember 2011.
2. Business Objectives
Project ini berangkat dari dua pertanyaan utama:
1. Bagaimana segmentasi pelanggan berdasarkan nilai RFM menggunakan K-Means dapat membantu mengenali karakteristik pelanggan dan mendukung strategi retensi?
2. Pola pembelian produk apa yang dapat ditemukan melalui Market Basket Analysis untuk mendukung strategi bundling dan cross-selling?
Tujuan Analisis
- Mengelompokkan pelanggan berdasarkan perilaku transaksi.
- Mengidentifikasi pelanggan loyal dan pelanggan yang berisiko tidak aktif.
- Menemukan produk yang sering dibeli secara bersamaan.
- Menyusun rekomendasi pemasaran berdasarkan data transaksi.
- Menggabungkan hasil segmentasi pelanggan dan asosiasi produk untuk mendukung pengambilan keputusan bisnis.
3. Dataset Description
Dataset Online Retail II berisi catatan transaksi dari perusahaan retail online yang berbasis di United Kingdom.
Informasi Dataset
Informasi	Keterangan
Dataset	Online Retail II
Sumber	UCI Machine Learning Repository
Periode	1 Desember 2009 – 9 Desember 2011
Jumlah data awal	1.067.371 transaksi
Jumlah kolom	8
Data bersih	779.425 baris
Pelanggan unik	5.878
Negara analisis MBA	United Kingdom


Fitur Dataset
Kolom	Deskripsi
Invoice	Nomor transaksi
StockCode	Kode produk
Description	Nama atau deskripsi produk
Quantity	Jumlah produk yang dibeli
InvoiceDate	Tanggal transaksi
Price	Harga per unit
Customer ID	Identitas pelanggan
Country	Negara pelanggan


Catatan: Dataset penelitian dipublikasikan melalui UCI Machine Learning Repository dan juga tersedia di Kaggle untuk keperluan penelitian dan pembelajaran.
4. Methodology
Proses analisis mengikuti kerangka CRISP-DM (Cross-Industry Standard Process for Data Mining) yang terdiri dari enam tahapan:
1. Business Understanding – memahami permasalahan bisnis dan tujuan analisis pelanggan.
2. Data Understanding – mempelajari struktur, karakteristik, dan kualitas dataset.
3. Data Preparation – membersihkan data serta menyiapkan fitur yang diperlukan.
4. Modeling – menerapkan K-Means Clustering dan FP-Growth.
5. Evaluation – mengevaluasi hasil pengelompokan dan aturan asosiasi.
6. Deployment – menerjemahkan hasil analisis menjadi rekomendasi bisnis.
5. Data Preprocessing
Sebelum dianalisis, data dibersihkan agar transaksi yang digunakan memenuhi kebutuhan pengolahan.
Tahapan Preprocessing
- Menghapus 243.007 baris dengan Customer ID kosong.
- Menghapus 18.744 transaksi pembatalan, yaitu invoice yang diawali huruf C.
- Memeriksa transaksi dengan Quantity kurang dari atau sama dengan nol. Tidak ditemukan baris yang perlu dihapus pada tahap ini.
- Menghapus 71 baris dengan Price kurang dari atau sama dengan nol.
- Menghapus 26.124 baris duplikat.
Hasil Data Cleaning
Tahapan	Baris dihapus	Baris tersisa
Data awal	–	1.067.371
Missing Customer ID	243.007	824.364
Transaksi pembatalan	18.744	805.620
Quantity ≤ 0	0	805.620
Price ≤ 0	71	805.549
Duplikat	26.124	779.425
Data bersih final		779.425


Setelah proses pembersihan, terdapat 779.425 baris data, atau sekitar 73,0% dari keseluruhan data awal, yang digunakan dalam analisis.
Feature Engineering
Beberapa fitur tambahan dibuat untuk mendukung proses analisis:
- TotalPrice = Quantity × Price
- Year
- Month
- Hour
- DayOfWeek
6. Customer Segmentation: RFM & K-Means Clustering
6.1 RFM Analysis
Analisis RFM digunakan untuk melihat perilaku pembelian pelanggan melalui tiga dimensi berikut:
Dimensi	Pengertian	Perhitungan
Recency (R)	Jarak waktu sejak pelanggan terakhir bertransaksi	Tanggal referensi dikurangi tanggal transaksi terakhir
Frequency (F)	Seberapa sering pelanggan melakukan pembelian	Jumlah invoice unik
Monetary (M)	Total nilai pembelian pelanggan	Jumlah seluruh TotalPrice


Tanggal referensi yang digunakan adalah 10 Desember 2011, satu hari setelah tanggal transaksi terakhir pada dataset.
6.2 RFM Preprocessing
Sebelum digunakan sebagai input K-Means, nilai RFM melalui dua tahap transformasi:
- Log transformation menggunakan log1p() untuk mengurangi skewness atau kemencengan distribusi data.
- Standardization menggunakan StandardScaler agar setiap fitur memiliki skala yang sebanding.
6.3 K-Means Clustering
K-Means digunakan untuk mengelompokkan pelanggan berdasarkan kemiripan nilai RFM.

Parameter yang digunakan dalam proses pemodelan:
Parameter	Nilai
Algoritma	K-Means
Kandidat cluster	K = 2 sampai K = 10
n_init	10
random_state	42
Evaluasi jumlah cluster	Elbow Method dan Silhouette Score


6.4 Optimal Cluster Evaluation
Elbow Method menunjukkan titik siku pada K=4. Namun, jumlah cluster juga dievaluasi menggunakan Silhouette Score untuk melihat kualitas pemisahan antarkelompok.
Jumlah Cluster (K)	Silhouette Score
2	0,4386
3	0,3477
4	0,3650
5	0,3425
6	0,3348
7	0,3066
8	0,3033
9	0,2925
10	0,2905


Berdasarkan hasil evaluasi, K=2 dipilih sebagai jumlah cluster optimal karena menghasilkan Silhouette Score tertinggi, yaitu 0,4386.
6.5 Customer Segmentation Results
Hasil K-Means membagi pelanggan menjadi dua segmen:
Profil	At-Risk / Lost	Loyal Customers
Jumlah pelanggan	3.558	2.320
Persentase	60,5%	39,5%
Rata-rata Recency	299,65 hari	50,56 hari
Rata-rata Frequency	2,10 transaksi	12,72 transaksi
Rata-rata Monetary	£614,34	£6.546,97


Interpretasi Segmen
1. At-Risk / Lost Customers

Segmen ini terdiri dari 3.558 pelanggan atau 60,5% dari keseluruhan pelanggan. Rata-rata waktu sejak transaksi terakhir mencapai 299,65 hari. Frekuensi pembeliannya sebesar 2,10 transaksi dengan nilai Monetary rata-rata £614,34.

Karakteristik tersebut menunjukkan bahwa kelompok ini sudah cukup lama tidak melakukan pembelian dan perlu mendapatkan perhatian melalui strategi reaktivasi atau win-back campaign.

2. Loyal Customers

Segmen ini terdiri dari 2.320 pelanggan atau 39,5% dari keseluruhan pelanggan. Rata-rata Recency sebesar 50,56 hari, Frequency sebanyak 12,72 transaksi, dan Monetary mencapai £6.546,97.

Kelompok ini memiliki aktivitas pembelian yang relatif lebih tinggi dan nilai transaksi yang lebih besar. Karena itu, pelanggan dalam segmen ini dapat menjadi fokus strategi untuk mempertahankan loyalitas dan meningkatkan nilai pembelian.
7. Market Basket Analysis: FP-Growth
7.1 Overview
Market Basket Analysis digunakan untuk menemukan hubungan antarproduk yang sering dibeli secara bersamaan dalam satu transaksi.

Dalam project ini, algoritma FP-Growth (Frequent Pattern Growth) digunakan untuk menemukan frequent itemsets dan association rules. Analisis difokuskan pada transaksi United Kingdom setelah proses pembersihan data.
7.2 Basket Matrix
Data transaksi diubah menjadi basket matrix dengan rincian berikut:
Komponen	Jumlah
Transaksi	33.541
Produk	5.249
Minimum support	2%
Minimum confidence	30%
Filter lift	> 1


Nilai dalam basket matrix bersifat biner. Angka 1 menunjukkan bahwa produk dibeli dalam transaksi, sedangkan angka 0 menunjukkan bahwa produk tidak dibeli.
7.3 Frequent Itemsets
Dengan minimum support sebesar 2%, algoritma FP-Growth menghasilkan 180 frequent itemsets.

Berikut sepuluh produk dengan nilai support tertinggi:
No.	Produk	Support
1	WHITE HANGING HEART T-LIGHT HOLDER	14,02%
2	REGENCY CAKESTAND 3 TIER	8,52%
3	ASSORTED COLOUR BIRD ORNAMENT	7,47%
4	JUMBO BAG RED RETROSPOT	7,13%
5	PARTY BUNTING	5,79%
6	LUNCH BAG BLACK SKULL.	5,67%
7	REX CASH+CARRY JUMBO SHOPPER	5,49%
8	HOME BUILDING BLOCK WORD	5,27%
9	HEART OF WICKER SMALL	5,16%
10	HEART OF WICKER LARGE	5,13%


7.4 Association Rules
Dari frequent itemsets yang ditemukan, proses ekstraksi menghasilkan 15 association rules dengan minimum confidence 30% dan nilai lift lebih dari 1.

Berikut beberapa aturan asosiasi dengan nilai lift tertinggi:
Antecedent (Produk yang Dibeli)	Consequent (Produk Pasangan)	Support	Confidence	Lift
STRAWBERRY CERAMIC TRINKET BOX	SWEETHEART CERAMIC TRINKET BOX	2,25%	45,62%	13,95
SWEETHEART CERAMIC TRINKET BOX	STRAWBERRY CERAMIC TRINKET BOX	2,25%	68,92%	13,95
WOODEN FRAME ANTIQUE WHITE	WOODEN PICTURE FRAME WHITE FINISH	2,90%	56,54%	11,77
WOODEN PICTURE FRAME WHITE FINISH	WOODEN FRAME ANTIQUE WHITE	2,90%	60,34%	11,77
LOVE BUILDING BLOCK WORD	HOME BUILDING BLOCK WORD	2,28%	52,84%	10,02


7.5 Interpretation
Nilai lift tertinggi, yaitu 13,95, ditemukan pada pasangan produk STRAWBERRY CERAMIC TRINKET BOX dan SWEETHEART CERAMIC TRINKET BOX.

Nilai tersebut menunjukkan adanya asosiasi positif yang kuat antara kedua produk. Pelanggan yang membeli salah satu produk memiliki kecenderungan lebih tinggi untuk membeli produk pasangannya dibandingkan jika pembelian keduanya tidak saling berhubungan.

Temuan ini dapat digunakan sebagai dasar untuk menyusun strategi product bundling dan cross-selling.
8. Business Recommendations
Hasil RFM Clustering dan Market Basket Analysis memberikan gambaran mengenai kelompok pelanggan yang perlu menjadi prioritas serta produk yang berpotensi ditawarkan secara bersamaan.
Rekomendasi Strategi
Segmen	Strategi	KPI Target
Loyal Customers	VIP membership, early access, reward, upselling, bundling, dan email personal	Monetary +20%, Frequency +1 transaksi/kuartal, Retention >90%
At-Risk / Lost	Win-back email, voucher diskon 20%, survei alasan tidak aktif, retargeting, dan penawaran berbatas waktu	Reaktivasi 15–20% dalam 3 bulan


Implementation Roadmap
Waktu	Fase	Aktivitas
Bulan 1	Quick Win	Aktivasi VIP dan pengiriman win-back email dengan voucher
Bulan 2	Growth	Bundling berdasarkan association rules dan kampanye cross-selling
Bulan 2	Growth	Onboarding email dan penawaran free shipping untuk reaktivasi
Bulan 3	Optimize	Evaluasi KPI, pembaruan segmentasi RFM, A/B testing, dan survei kepuasan
Bulan 3	Optimize	Peluncuran referral program untuk pelanggan loyal


Catatan: Target KPI di atas merupakan rekomendasi strategi dan belum berasal dari pengukuran kampanye yang telah dijalankan.
9. Key Findings
Berdasarkan seluruh proses analisis, diperoleh beberapa temuan utama:
- Dataset awal terdiri dari 1.067.371 transaksi dan menghasilkan 779.425 baris setelah preprocessing.
- Sebanyak 5.878 pelanggan unik berhasil dianalisis menggunakan metode RFM.
- K-Means dengan K=2 menghasilkan Silhouette Score tertinggi sebesar 0,4386.
- Hasil segmentasi terdiri dari 3.558 pelanggan At-Risk/Lost dan 2.320 Loyal Customers.
- FP-Growth menghasilkan 180 frequent itemsets dan 15 association rules yang memenuhi kriteria.
- Nilai lift tertinggi sebesar 13,95 ditemukan pada pasangan produk STRAWBERRY CERAMIC TRINKET BOX dan SWEETHEART CERAMIC TRINKET BOX.
- Total revenue pada dataset mencapai £17.374.804.
10. Conclusion
Project ini menunjukkan bahwa RFM Clustering dan Market Basket Analysis dapat digunakan secara bersamaan untuk memahami perilaku pelanggan dari dua sudut pandang yang saling melengkapi.

K-Means Clustering membantu mengidentifikasi kelompok pelanggan yang perlu menjadi sasaran strategi bisnis. Sementara itu, Market Basket Analysis memberikan informasi mengenai produk yang memiliki keterkaitan dalam pola pembelian pelanggan.

Hasil segmentasi menunjukkan bahwa sebagian besar pelanggan termasuk dalam kelompok At-Risk/Lost, yaitu sebesar 60,5%. Temuan ini menunjukkan pentingnya strategi retensi dan reaktivasi pelanggan. Di sisi lain, hasil FP-Growth menemukan pola asosiasi produk yang dapat dimanfaatkan untuk menyusun penawaran bundling dan cross-selling.

Secara keseluruhan, project Customer Intelligence ini memperlihatkan bagaimana data transaksi dapat diolah menjadi informasi yang mendukung pengambilan keputusan bisnis, terutama dalam meningkatkan retensi pelanggan dan mengoptimalkan nilai transaksi.
11. Technology Stack
Teknologi dan library yang digunakan atau berkaitan dengan proses analisis dalam project ini meliputi:
Teknologi	Kegunaan
Python	Bahasa pemrograman untuk pengolahan dan analisis data
Pandas	Mengolah dan memanipulasi dataset
NumPy	Mendukung komputasi numerik
Scikit-learn	Melakukan preprocessing, standardisasi, K-Means, dan evaluasi clustering
FP-Growth	Menemukan frequent itemsets dari data transaksi
Matplotlib / Seaborn	Membuat visualisasi data dan hasil analisis
Jupyter Notebook	Lingkungan untuk menjalankan eksperimen dan mendokumentasikan proses analisis


Catatan: Daftar library di atas mencakup teknologi yang relevan dengan metode penelitian. Pastikan daftar akhir disesuaikan dengan library dan versi yang benar-benar digunakan pada notebook project.
12. Repository Structure
Berikut struktur direktori yang direkomendasikan untuk mengorganisasi file project. Nama file dapat disesuaikan dengan isi repository yang sebenarnya.
customer-intelligence-rfm-mba/
├── README.md
├── requirements.txt
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
│   ├── 01_data_understanding_eda.ipynb
│   ├── 02_data_preprocessing.ipynb
│   ├── 03_rfm_kmeans_clustering.ipynb
│   └── 04_market_basket_fp_growth.ipynb
├── results/
│   ├── customer_segmentation/
│   ├── market_basket_analysis/
│   └── visualizations/
└── models/
13. Installation and Usage
Berikut contoh langkah untuk menjalankan project apabila repository sudah dilengkapi dengan notebook dan file dependensi.
# Clone repository
git clone <URL_REPOSITORY>

# Masuk ke folder project
cd customer-intelligence-rfm-mba

# Buat virtual environment (opsional)
python -m venv venv

# Aktifkan virtual environment di Windows
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Jalankan Jupyter Notebook
jupyter notebook
Pastikan dataset tersedia di direktori yang sesuai dengan lokasi file yang digunakan pada notebook.
14. Limitations and Future Work
Beberapa pengembangan yang dapat dipertimbangkan untuk penelitian selanjutnya:
- Menambahkan dimensi RFM menjadi RFMD atau LRFM agar segmentasi pelanggan lebih terperinci.
- Membandingkan kinerja FP-Growth dengan algoritma Apriori dan ECLAT.
- Menggunakan Random Forest atau XGBoost untuk memprediksi segmen pelanggan baru.
- Mengembangkan dashboard interaktif yang menggabungkan informasi segmentasi pelanggan dan rekomendasi produk.
- Melakukan A/B testing untuk mengukur dampak strategi terhadap tingkat konversi dan retensi pelanggan.
15. References
1. Agrawal, R., & Srikant, R. (1994). Fast algorithms for mining association rules. Proceedings of the 20th International Conference on Very Large Data Bases, 487–499.
2. Buttle, F., & Maklan, S. (2019). Customer Relationship Management: Concepts and Technologies (4th ed.). Routledge.
3. Han, J., Pei, J., & Yin, Y. (2000). Mining frequent patterns without candidate generation. Proceedings of the ACM SIGMOD International Conference on Management of Data, 1–12.
4. Han, J., Kamber, M., & Pei, J. (2011). Data Mining: Concepts and Techniques (3rd ed.). Morgan Kaufmann.
5. Hughes, A. M. (1994). Strategic Database Marketing. Probus Publishing.
6. MacQueen, J. (1967). Some methods for classification and analysis of multivariate observations. Proceedings of the Fifth Berkeley Symposium on Mathematical Statistics and Probability, 1, 281–297.
7. Rousseeuw, P. J. (1987). Silhouettes: A graphical aid to the interpretation and validation of cluster analysis. Journal of Computational and Applied Mathematics, 20, 53–65.
8. Tsai, C. Y., & Chiu, C. C. (2004). A purchase-based market segmentation methodology. Expert Systems with Applications, 27(2), 265–276.
9. Wei, J. T., Lin, S. Y., & Wu, H. H. (2010). A review of the application of RFM model. African Journal of Business Management, 4(19), 4199–4206.
<p align="center">
  <strong>Customer Intelligence | Data Mining | RFM Clustering | Market Basket Analysis</strong>
</p>
