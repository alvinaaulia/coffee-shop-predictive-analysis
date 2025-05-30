# Coffee Shop Predictive Analysis

![Coffee Shop](https://img.freepik.com/free-photo/coffee-shop-workspace-top-view_23-2149076688.jpg)

Repository ini berisi analisis prediktif untuk mengoptimalkan bisnis coffee shop dengan memanfaatkan data transaksi penjualan.

## Overview
Proyek ini bertujuan untuk:
- Mengidentifikasi **produk terlaris** berdasarkan kategori dan tipe
- Menganalisis **lokasi dengan penjualan tertinggi**
- Memahami **tren penjualan harian**
- Membangun model prediksi penjualan

## Dataset
Data berasal dari [Kaggle - Coffee Sales Dataset](https://www.kaggle.com/datasets/ahmedabbas757/coffee-sales) dengan karakteristik:
- 149.116 transaksi
- 11 fitur termasuk:
  - Tanggal/waktu transaksi
  - Jumlah produk
  - Harga satuan
  - Lokasi toko
  - Kategori produk

## Teknik Analisis
1. **Exploratory Data Analysis (EDA)**
   - Analisis univariat dan multivariat
   - Visualisasi distribusi penjualan
   - Identifikasi pola musiman

2. **Data Preprocessing**
   - Penanganan outlier dengan metode IQR
   - Feature engineering (sales_amount, day_of_week, etc.)
   - Encoding variabel kategorikal

3. **Modeling**
   - Membandingkan 5 model:
     - Linear Regression
     - Random Forest
     - Gradient Boosting
     - K-Nearest Neighbors
     - Decision Tree
   - Evaluasi menggunakan MAE, RMSE, dan R²

4. **Hyperparameter Tuning**
   - Optimasi parameter untuk model terbaik

## Hasil Utama
- **Produk terlaris**: Kategori Coffee (58.414 transaksi)
- **Lokasi terbaik**: Astoria (212,284 total penjualan)
- **Model terbaik**: Gradient Boosting (R² 0.3727)
- **Waktu sibuk**: Jam 12-14 (makan siang)

## 🚀 Cara Menggunakan

1. Clone repository:
```bash
git clone https://github.com/username/coffee-shop-predictive-analysis.git
