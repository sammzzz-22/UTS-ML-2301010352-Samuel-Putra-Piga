# UTS Machine Learning — Jalur B (Regresi)

## Prediksi Harga Produk Tokopedia dengan Regresi Linear

---

## Identitas

| Keterangan | Informasi |
|---|---|
| Nama | Samuel Putra Piga |
| NIM | 2301010352 |
| Kelas | XX |
| Mata Kuliah | Machine Learning |
| Dosen | Dr. I Gede Totok Suryawan, S.Kom., M.T. |
| Program Studi | Informatika |

---

## Ringkasan Proyek

Proyek ini merupakan tugas individu UTS Machine Learning dengan pendekatan **CRISP-DM, Jalur B (Regresi)**, yang berfokus pada prediksi harga produk Tokopedia dalam satuan Rupiah.

Prediksi dilakukan berdasarkan sejumlah fitur, yaitu rating, diskon, jumlah produk terjual, jumlah ulasan, dan lokasi toko. Tiga model dibandingkan menggunakan 5-fold cross-validation pada data latih, yaitu:

- `DummyRegressor` sebagai model baseline.
- Regresi linear sederhana dengan satu fitur (diskon).
- Regresi linear berganda dengan beberapa fitur.

Seluruh proses pembagian data, cross-validation, dan pemodelan menggunakan `SEED = 352` untuk menjaga konsistensi eksperimen.

### Hasil Evaluasi Model

| Model | MAE Uji (Rp) | R² Uji (Log) |
|---|------:|---:|
| Baseline | 407.234 | 0,000 |
| Linear Sederhana | 406.850 | 0,005 |
| **Linear Berganda** | **396.466** | **0,127** |

### Kesimpulan Hasil

- **Model terbaik:** Regresi linear berganda, dengan MAE cross-validation terendah sebesar Rp409.002.
- **Peningkatan terhadap baseline:** Penurunan MAE sebesar 2,6%, yang menunjukkan peningkatan performa masih relatif kecil.
- **Nilai R² pengujian:** 0,127 pada skala log, sehingga model belum mampu menjelaskan variasi harga secara optimal.
- **Overfitting:** Tidak ditemukan indikasi overfitting yang berarti, dengan selisih R² log latih dan uji sebesar 0,015.
- **Penyebab performa:** Fitur yang tersedia belum mencakup informasi penting seperti kategori dan merek produk. Korelasi fitur numerik terhadap harga juga tergolong lemah, dengan nilai absolut korelasi maksimal sebesar 0,09.

Secara keseluruhan, model regresi linear berganda menjadi model terbaik di antara model yang diuji, tetapi performanya masih terbatas dan lebih sesuai digunakan sebagai pembanding atau prediktor kasar.

---

## Sumber Data

- **Dataset:** Indonesia E-Commerce Dataset: Tokopedia Listings
- **Platform:** Kaggle
- **Pengunggah:** pandaa12
- **Link Dataset:** [Kaggle — Indonesia E-Commerce Dataset: Tokopedia Listings](https://www.kaggle.com/datasets/pandaa12/indonesia-e-commerce-dataset-tokopedia-listings)
- **Tanggal akses:** 26 November 2026
- **Lisensi:** Apache 2.0

### Informasi Dataset

| Informasi | Jumlah |
|---|---:|
| Data awal | 29.519 baris |
| Jumlah kolom | 9 |
| Data setelah pembersihan | 28.368 baris |

Kolom nama produk, nama toko, dan URL produk tidak digunakan sebagai fitur pemodelan dan dihilangkan dari proses analisis untuk menghindari penggunaan informasi identitas listing yang tidak diperlukan.

---

## Struktur Repository

```text
UTS-ML-2301010352-Samuel-Putra-Piga/
│
├── README.md
│
├── notebook/
│   └── UTS_ML_2301010352_Samuel-Putra-Piga.ipynb
│
├── data/
│   └── produk_tokopedia.csv
│
└── reports/
    └── Grafik utama dan slide presentasi
```

---

## Cara Menjalankan Notebook

1. Buka notebook menggunakan Google Colab atau Jupyter Notebook.
2. Pastikan dataset tersedia pada lokasi berikut:

   ```text
   C:\ML\produk_tokopedia.csv
   ```

   Jika file tidak ditemukan, notebook akan mencoba mengunduh dataset secara otomatis melalui `kagglehub`.

3. Pastikan library berikut telah tersedia:

   - `pandas`
   - `numpy`
   - `matplotlib`
   - `seaborn`
   - `scikit-learn` (versi 1.1 atau lebih baru)

4. Jalankan seluruh sel notebook melalui menu **Runtime → Run all** di Google Colab.

---

## Keputusan Metodologi

- **Transformasi target:** Harga dimodelkan menggunakan `log(harga)` karena distribusi harga awal sangat miring (*skewed*). Nilai skewness berubah dari 41,9 menjadi 0,13 setelah transformasi log. Hasil prediksi kemudian dikembalikan ke skala Rupiah.
- **Pembagian data:** Data latih dan data uji dipisahkan sebelum proses imputasi, scaling, dan encoding dilakukan.
- **Pipeline pemodelan:** Imputer, scaler, encoder, dan model ditempatkan dalam `Pipeline` atau `ColumnTransformer` untuk mencegah kebocoran data (*data leakage*).
- **Penanganan outlier:** Outlier harga ditangani menggunakan metode IQR. Batas IQR dihitung berdasarkan data latih dan diterapkan sebagai cakupan pemodelan pada data latih maupun data uji.
- **Pemilihan model:** Model terbaik ditentukan berdasarkan skor cross-validation pada data latih, bukan berdasarkan performa data uji.
- **Evaluasi akhir:** Data uji digunakan untuk evaluasi akhir setelah proses pemilihan model selesai.

---

## Keterbatasan

Beberapa keterbatasan dalam penelitian ini meliputi:

- Fitur yang digunakan belum mencakup kategori, jenis, dan merek produk.
- Dataset merupakan hasil pengumpulan data pada satu periode waktu sehingga belum menggambarkan perubahan harga secara dinamis.
- Model yang digunakan masih terbatas pada pendekatan regresi linear.
- Nama lokasi toko belum sepenuhnya seragam, seperti perbedaan penulisan antara "Jakarta Pusat" dan "Kota Administrasi Jakarta Pusat".
- Harga ekstrem telah dikeluarkan dari cakupan pemodelan, sehingga model tidak ditujukan untuk memprediksi produk dengan harga yang sangat murah maupun sangat mahal.

---

## Pernyataan Penggunaan AI

- **Alat AI:** Claude (Anthropic).
- **Penggunaan:** Membantu pembuatan kerangka notebook dan kode, termasuk pra-pemrosesan data, pipeline, cross-validation, evaluasi model, serta penyusunan draf interpretasi hasil dan kesimpulan.
