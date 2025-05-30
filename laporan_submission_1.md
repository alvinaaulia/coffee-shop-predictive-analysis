# Laporan Proyek Machine Learning - ALVINA AULIA NISA
## Domain Proyek
Industri kopi telah berkembang secara signifikan dalam beberapa tahun terakhir dengan pertumbuhan coffee shop yang meningkat di berbagai lokasi. Pemilik bisnis coffee shop perlu memahami pola penjualan, preferensi konsumen, dan strategi optimal untuk meningkatkan pendapatan. Analisis prediktif dapat membantu pemilik dan pengelola coffee shop untuk mengoptimalkan inventaris, merencanakan staf, dan merancang strategi pemasaran yang lebih efektif.

Dalam lingkungan bisnis yang kompetitif saat ini, keputusan berbasis data menjadi kunci keberhasilan. Menurut penelitian dari National Coffee Association, konsumsi kopi di luar rumah terus meningkat sehingga memahami pola pembelian konsumen sangat penting untuk keberhasilan bisnis. Dengan memanfaatkan analisis prediktif, coffee shop dapat mengantisipasi permintaan konsumen dan menyesuaikan operasional mereka secara tepat.

## Business Understanding
### Problem Statements
- **Produk dengan performa penjualan terbaik**: Bagaimana mengidentifikasi produk kopi mana yang memiliki performa penjualan terbaik selama periode tertentu? Informasi ini penting untuk fokus pada produk yang menghasilkan pendapatan terbesar dan meningkatkan strategi pemasaran.
- **Lokasi dengan penjualan tertinggi**: Di lokasi atau cabang mana penjualan kopi mencapai nilai tertinggi? Mengetahui lokasi dengan penjualan terbesar dapat membantu alokasi sumber daya dan pengembangan pasar secara lebih efisien.
- **Tren penjualan per hari**: Bagaimana pola tren penjualan kopi dari hari ke hari? Dengan memahami tren ini, bisnis dapat merencanakan stok, promosi, dan operasional yang lebih optimal sesuai dengan waktu puncak penjualan.

### Goals
- **Menentukan produk kopi dengan performa penjualan terbaik**: Menghasilkan daftar produk kopi yang memiliki penjualan paling tinggi secara kuantitas dan nilai selama periode dataset, guna mendukung pengambilan keputusan produk unggulan.
- **Mengidentifikasi lokasi penjualan tertinggi**: Menemukan cabang atau lokasi penjualan yang paling produktif sehingga bisnis dapat fokus pada pengembangan lokasi tersebut dan memperbaiki lokasi dengan penjualan rendah.
- **Memahami tren penjualan per hari**: Menggambarkan pola fluktuasi penjualan harian secara visual maupun statistik untuk mengantisipasi kebutuhan stok dan merancang strategi promosi harian yang efektif.

### Solution Statements
- **Analisis Data Deskriptif dan Visualisasi**: Melakukan eksplorasi data (EDA) dengan grafik batang, heatmap, dan time series untuk melihat performa produk, lokasi penjualan, dan tren harian. Ini membantu memahami pola dasar dan insight awal.
- **Segmentasi dan Klasterisasi Produk/Lokasi**: Menggunakan metode clustering untuk mengelompokkan produk atau lokasi berdasarkan performa penjualan, sehingga dapat memudahkan identifikasi segmen unggulan dan segmen yang perlu ditingkatkan.
- **Model Prediktif Penjualan**: Membangun model time series forecasting untuk memprediksi tren penjualan harian ke depan sehingga dapat membantu bisnis dalam perencanaan stok dan promosi yang lebih tepat.
- **Evaluasi dan Monitoring Kinerja**: Menetapkan metrik evaluasi seperti total penjualan, rata-rata penjualan per hari, dan growth rate untuk mengukur keberhasilan strategi yang diambil berdasarkan hasil analisis.

## Data Understanding
Dataset yang digunakan dalam proyek ini berasal dari Kaggle dengan judul Coffee Sales yang dapat diakses melalui tautan berikut: ```https://www.kaggle.com/datasets/ahmedabbas757/coffee-sales```

Dataset ini berisi catatan transaksi penjualan kopi dalam skala besar dengan total 149.116 baris data dan 11 kolom fitur. Dataset ini menyediakan informasi lengkap terkait detail transaksi mulai dari waktu transaksi, lokasi penjualan, hingga detail produk.

**Variabel-variabel pada dataset:**
- ```transaction_id```: Nomor unik yang mengidentifikasi setiap transaksi penjualan (tipe data: integer).
- ```transaction_date```: Tanggal terjadinya transaksi (tipe data: datetime). Informasi ini penting untuk analisis tren penjualan per hari.
- ```transaction_time```: Waktu transaksi dalam format string, merekam jam atau waktu spesifik transaksi terjadi.
- ```transaction_qty```: Jumlah unit produk yang terjual dalam transaksi tersebut (tipe data: integer).
- ```store_id```: ID unik yang mengidentifikasi toko atau cabang tempat transaksi berlangsung (tipe data: integer).
- ```store_location```: Nama lokasi atau daerah dari toko tempat penjualan terjadi (tipe data: objek/string). Fitur ini digunakan untuk analisis penjualan berdasarkan lokasi.
- ```product_id```: ID unik produk yang dijual dalam transaksi tersebut (tipe data: integer).
- ```unit_price```: Harga per unit produk pada saat transaksi (tipe data: float).
- ```product_category```: Kategori produk kopi, misalnya kopi bubuk, kopi biji, atau kopi kemasan (tipe data: objek/string).
- ```product_type```: Jenis produk yang lebih spesifik, dapat berupa varian atau rasa kopi tertentu (tipe data: objek/string).
- ```product_detail```: Keterangan atau detail tambahan terkait produk, misalnya ukuran kemasan atau spesifikasi khusus (tipe data: objek/string).

## Exploratory Data Analysis (EDA)
### Analisis Univariat
Analisis univariat dilakukan untuk memahami distribusi masing-masing variabel secara terpisah:
- **Transaction Quantity**: Mayoritas transaksi melibatkan pembelian 1-3 unit produk, dengan beberapa outlier yang menunjukkan pembelian dalam jumlah besar.
- **Unit Price**: Menunjukkan beberapa tingkatan harga yang berbeda, menandakan adanya kategori produk dengan variasi harga.
- **Product Category**: Kategori “Coffee” mendominasi penjualan dengan jumlah transaksi terbanyak, diikuti oleh kategori lainnya seperti “Tea” dan “Bakery”.
- **Store Location**: Data menunjukkan transaksi terjadi di tiga lokasi utama: Lower Manhattan, Hell’s Kitchen, dan Astoria, dengan distribusi yang bervariasi.

### Analisis Multivariat
Penjualan berdasarkan Kategori dan Lokasi:
- Lower Manhattan memiliki ```sales_amount``` tertinggi di beberapa kategori produk terutama pada “Drinking Chocolate”.
- Astoria memiliki ```sales_amount``` terendah di sebagian besar kategori namun unggul pada kategori “Bakery”.
- Hell’s Kitchen menunjukkan pola penjualan yang berbeda kemungkinan karena demografi pelanggan yang berbeda.

Tren Penjualan per Jam dan Hari:
- Puncak penjualan terjadi sekitar jam 12-14 (waktu makan siang) di semua lokasi.
- Penjualan terendah terjadi di pagi hari (jam 6-8) dan malam (jam 18-20).
- Pada weekdays (Senin-Jumat), pola penjualan menunjukkan puncak yang jelas pada jam makan siang.
- Pada weekend (Sabtu-Minggu), penjualan lebih tersebar sepanjang hari dengan puncak yang lebih lebar.

Korelasi antar Variabel Numerik:
- Korelasi kuat antara ```transaction_qty``` dan ```sales_amount``` (0.76) yang menunjukkan bahwa peningkatan jumlah transaksi berkorelasi langsung dengan peningkatan pendapatan.
- ```unit_price``` dan ```sales_amount``` juga menunjukkan korelasi positif namun tidak sekuat korelasi dengan ```transaction_qty```.

## Data Preparation
Beberapa langkah data preparation yang dilakukan:
- **Penanganan Missing Values**: Tidak ditemukan missing values dalam dataset yang dapat mempengaruhi analisis.
- **Penanganan Outliers**: Outliers diidentifikasi menggunakan metode IQR (Interquartile Range) dan dipertahankan karena representatif terhadap variasi transaksi yang terjadi di dunia nyata.
- **Feature Engineering**: 
    * Menambahkan kolom ```sales_amount``` sebagai hasil perkalian ```transaction_qty``` dan ```unit_price```
    * Mengekstrak fitur waktu ```day_of_week```, ```month```, ```hour``` dari timestamp
    * Menambahkan fitur ```is_weekend``` untuk membedakan hari kerja dan akhir pekan
    * Mengkategorikan jam dalam ```time_of_day``` (Morning, Midday, Afternoon, Evening)
- **Encoding**:
    * Label Encoding untuk variabel kategorikal ordinal
    * Variabel kategorikal nominal diubah menjadi fitur numerik menggunakan teknik one-hot encoding dengan ```pd.get_dummies()```
- **Feature Selection**: Memilih fitur yang relevan untuk model termasuk ```store_id```, ```product_id```, ```store_location_encoded```, ```product_category_encoded```, ```product_type_encoded```, ```day_of_week_encoded```, ```month```, ```hour```, ```is_weekend```, ```time_of_day_encoded```
- **Train-Test Split**: Data dibagi menjadi 80% training set dan 20% testing set dengan stratifikasi berdasarkan binning dari target variable untuk mempertahankan distribusi.
- **Standardization**: Variabel numerik distandardisasi menggunakan StandardScaler untuk model yang sensitif terhadap skala (Linear Regression dan KNN).

## Modeling
Dalam proyek ini, beberapa model machine learning diterapkan untuk memprediksi ```sales_amount```:
- **Linear Regression**: Model dasar untuk menangkap hubungan linear antara fitur dan target.
- **Decision Tree Regressor**: Model non-linear yang mempartisi data menjadi segmen-segmen berdasarkan nilai fitur.
- **Random Forest Regressor**: Ensemble model yang menggabungkan multiple decision trees untuk meningkatkan performa dan mengurangi overfitting.
- **Gradient Boosting Regressor**: Ensemble model yang membangun tree secara sekuensial, dengan setiap tree baru memperbaiki kesalahan prediksi tree sebelumnya.
- **K-Neighbors Regressor**: Model berbasis instance yang memprediksi berdasarkan kesamaan dengan data training terdekat.

### Model 1: Linear Regression
**Cara Kerja**: Linear Regression memodelkan hubungan antara fitur dan target sebagai garis lurus (kombinasi linier). Model ini mencari koefisien terbaik untuk setiap fitur agar error prediksi minimum (menggunakan metode OLS – Ordinary Least Squares).

Parameter Awal:
* ```fit_intercept=True (default)```: menambahkan bias ke model
* ```normalize=False (default)```

> **Kelebihan**: Sederhana, cepat dilatih, mudah diinterpretasi. </br>
> **Kekurangan**: Tidak bisa menangkap hubungan non-linier dan rentan terhadap outlier. </br>
> **Konteks Dataset**: Cocok sebagai baseline model, namun kurang mampu menangani kompleksitas data penjualan yang fluktuatif.

### Model 2: Decision Tree Regressor
**Cara Kerja**: Membangun struktur pohon berdasarkan fitur yang membagi data menjadi kelompok homogen terhadap target (sales_amount), menggunakan pengukuran seperti Mean Squared Error (MSE) untuk membuat split terbaik.

Parameter Awal:
* ```max_depth=5```
* ```min_samples_split=20```
* ```min_samples_leaf=10```

> **Kelebihan**: Mudah diinterpretasikan, bisa menangkap hubungan non-linier. </br>
> **Kekurangan**: Cenderung overfitting jika tidak dibatasi. </br>
> **Konteks Dataset**: Dapat menangani variabel kategorikal dan numerik secara langsung, namun performa terbatas jika dibanding model ensemble.

### Model 3: Random Forest Regressor
**Cara Kerja**: Merupakan ensemble dari banyak pohon keputusan (bagging). Setiap pohon dilatih pada subset acak data dan hasil akhir adalah rata-rata prediksi semua pohon.

Parameter Awal:
* ```n_estimators=100```
* ```max_depth=5```
* ```min_samples_split=10```
* ```min_samples_leaf=5```
* ```max_features='sqrt'```

> **Kelebihan**: Tahan terhadap overfitting, bekerja baik di banyak jenis data. </br>
> **Kekurangan**: Kurang interpretatif dibanding pohon tunggal. </br>
> **Konteks Dataset**: Cocok untuk data kompleks seperti penjualan dengan banyak fitur kategori.

### Model 4: Gradient Boosting Regressor
**Cara Kerja**: Model dibangun secara sekuensial, setiap model baru fokus memperbaiki kesalahan dari model sebelumnya. Menggunakan gradient descent untuk mengurangi loss.

Parameter Awal (sebelum tuning):
* ```n_estimators=100```
* ```max_depth=3```
* ```learning_rate=0.1```
* ```subsample=0.8```
* ```min_samples_split=10```
* ```min_samples_leaf=5```

> **Kelebihan**: Akurasi tinggi, bisa menangani hubungan non-linear kompleks. </br>
> **Kekurangan**: Waktu pelatihan lebih lama, rentan overfitting jika tidak dituning. </br>
> **Konteks Dataset**: Performa terbaik dalam memprediksi sales_amount.

### Model 5: K-Nearest Neighbors Regressor
**Cara Kerja**: Untuk data baru, model mencari k tetangga terdekat di data latih berdasarkan jarak (misal, Euclidean), lalu menghitung rata-rata nilai target dari tetangga tersebut.

Parameter Awal:
* ```n_neighbors=5```

> **Kelebihan**: Sederhana, tidak memerlukan pelatihan eksplisit.</br>
> **Kekurangan**: Sensitif terhadap skala data, tidak efisien untuk dataset besar. </br>
> **Konteks Dataset**: Kurang cocok untuk data berukuran besar dan banyak fitur, tetapi digunakan untuk perbandingan baseline.


## Evaluation
Beberapa metrik evaluasi digunakan untuk menilai performa model:
- **Mean Absolute Error (MAE)**: Rata-rata nilai absolut dari error menunjukkan seberapa dekat prediksi dengan nilai aktual.
- **Mean Squared Error (MSE)**: Rata-rata kuadrat error memberikan bobot lebih pada error yang besar.
- **Root Mean Squared Error (RMSE)**: Akar kuadrat dari MSE dalam unit yang sama dengan variabel target.
- **R-squared (R²)**: Menunjukkan proporsi variasi dalam variabel dependen yang dapat dijelaskan oleh model.

Hasil evaluasi menunjukkan:
- **Gradient Boosting** memberikan performa terbaik dengan RMSE terendah (1.5634) dan R² tertinggi (0.3727).
- **Linear Regression** memberikan performa terburuk dengan R² hanya 0.0627.
- **K-Neighbors** menunjukkan tanda-tanda overfitting dengan perbedaan signifikan antara performa training dan testing.
- **Random Forest** dan **Decision Tree** menunjukkan performa moderat.

Visualisasi Actual vs Predicted untuk model Gradient Boosting menunjukkan:
- Model cenderung memprediksi nilai yang lebih rendah (underprediction) terutama untuk nilai penjualan aktual yang tinggi.
- Mayoritas prediksi berada di bawah garis prediksi sempurna (garis merah putus-putus).
- Prediksi cenderung terkonsentrasi pada rentang 3-7 meskipun nilai aktual mencapai 14.

Analisis feature importance menunjukkan:
- ```product_id``` memiliki pengaruh terbesar (65.35%) dalam prediksi.
- ```product_category_encoded``` (17.17%) dan ```product_type_encoded``` (15.76%) juga memberikan kontribusi signifikan.
- Fitur temporal ```(hour, day_of_week, month)``` memiliki pengaruh yang relatif kecil.

## Kesimpulan
Berdasarkan analisis yang dilakukan, beberapa kesimpulan utama dapat diambil:
- **Produk dengan performa penjualan terbaik**: Kategori “Coffee” merupakan produk dengan performa penjualan tertinggi dengan total penjualan mencapai 269,918.45 dan jumlah transaksi terbanyak (58,414).
- **Lokasi dengan penjualan tertinggi**: Astoria merupakan lokasi dengan total penjualan tertinggi sebesar 212,284.00 dan jumlah transaksi terbanyak (49,364).
- **Tren penjualan per hari**: Hari Senin dan Kamis menunjukkan angka penjualan tertinggi dengan puncak penjualan terjadi pada jam makan siang (12-14).
- **Model prediktif**: Gradient Boosting memberikan performa terbaik dalam memprediksi ```sales_amount``` meskipun nilai R² yang masih relatif rendah (0.3727) menunjukkan bahwa model masih bisa ditingkatkan.
- **Limitasi model**: Model cenderung underpredicting untuk nilai penjualan yang tinggi yang menunjukkan bahwa mungkin diperlukan pendekatan yang berbeda atau fitur tambahan untuk memprediksi transaksi dengan nilai tinggi.

## Rekomendasi
- **Peningkatan model**: Mengeksplorasi teknik feature engineering yang lebih kompleks atau mencoba model deep learning untuk meningkatkan akurasi prediksi.
- **Segmentasi pelanggan**: Menambahkan fitur segmentasi pelanggan untuk memahami pola pembelian berbagai kelompok konsumen.
- **Optimasi inventaris**: Menggunakan hasil prediksi untuk mengoptimalkan inventaris produk kategori “Coffee” terutama pada jam-jam sibuk.
- **Strategi pemasaran**: Merancang promosi khusus untuk meningkatkan penjualan di lokasi dengan performa rendah dan pada waktu-waktu sepi (pagi dan malam hari).
- **Model time series**: Mengembangkan model time series yang lebih spesifik untuk memprediksi tren penjualan harian dan musiman dengan lebih akurat.