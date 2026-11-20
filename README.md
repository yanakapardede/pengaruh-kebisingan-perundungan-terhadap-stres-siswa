# PROJECT STATISTIKA INFERENSIAL KELOMPOK 3

# Prediksi Tingkat Stres Siswa Berdasarkan Tingkat Kebisingan dan Perundungan

## Team Members

| Name | NIM |
|---|---|
| Yanaka Sofia Pardede | 24031554065 |
| Ruthtatia Grace Astridia | 24031554072 |
| Sofia Dwi Kinasih | 24031554079 |

## Project Overview

Proyek ini menganalisis pengaruh **tingkat kebisingan** (`noise_level`) dan **perundungan** (`bullying`) terhadap **tingkat stres siswa** (`stress_level`) menggunakan **regresi linear berganda** di R. Pengujian dilakukan secara parsial (uji t) dan simultan (uji F) pada taraf signifikansi 0,05, dilengkapi visualisasi hubungan antarvariabel, termasuk bidang regresi 3D interaktif.

### Tujuan

1. Menganalisis pengaruh tingkat kebisingan terhadap tingkat stres siswa.
2. Mengidentifikasi besar pengaruh perundungan terhadap tingkat stres siswa.
3. Menguji apakah tingkat kebisingan dan perundungan secara bersama-sama berpengaruh signifikan terhadap tingkat stres siswa.

## Dataset Information

- **Dataset:** Student Stress Monitoring Dataset
- **Source:** [Kaggle – Student Stress Monitoring Dataset](https://www.kaggle.com/datasets/mdsultanulislamovi/student-stress-monitoring-datsets)
- **File:** `StressLevelDataset.csv`
- **Total Records:** 1,100
- **Total Variables:** 21 (3 variabel digunakan)

| Variabel | Peran | Keterangan |
|---|---|---|
| `noise_level` | Prediktor (X1) | Tingkat kebisingan |
| `bullying` | Prediktor (X2) | Tingkat perundungan |
| `stress_level` | Respons (Y) | Tingkat stres siswa |

> File dataset tidak diunggah ke repository. Unduh dari Kaggle, lalu sesuaikan path pada script.

## Hipotesis

| Uji | H0 | H1 |
|---|---|---|
| Parsial (X1) | Tingkat kebisingan tidak berpengaruh signifikan terhadap tingkat stres | Tingkat kebisingan berpengaruh signifikan terhadap tingkat stres |
| Parsial (X2) | Perundungan tidak berpengaruh signifikan terhadap tingkat stres | Perundungan berpengaruh signifikan terhadap tingkat stres |
| Simultan | Kebisingan dan perundungan secara bersama-sama tidak berpengaruh signifikan | Kebisingan dan perundungan secara bersama-sama berpengaruh signifikan |

Taraf signifikansi: α = 0,05

## Metode

| Step | Description |
|---|---|
| 1. Load data | Membaca `StressLevelDataset.csv` dengan `read.csv()` |
| 2. Seleksi variabel | Memilih `noise_level`, `bullying`, dan `stress_level` |
| 3. Model | Regresi linear berganda: `lm(stress_level ~ noise_level + bullying)` |
| 4. Uji parsial dan simultan | `summary(model)` (uji t dan uji F) |
| 5. Analisis varians | `anova(model)` |
| 6. Visualisasi | Grafik hubungan, bidang regresi 3D (Plotly), dan prediksi vs aktual |

Persamaan model:

```
stress_level = -0.337 + 0.210 × noise_level + 0.296 × bullying
```

## Results

### Koefisien Regresi

| Variabel | Estimate | Std. Error | t value | p-value |
|---|---:|---:|---:|---|
| (Intercept) | -0.33658 | 0.03465 | -9.713 | < 2e-16 |
| noise_level | 0.21048 | 0.01382 | 15.232 | < 2e-16 |
| bullying | 0.29625 | 0.01199 | 24.713 | < 2e-16 |

### Ringkasan Model

| Ukuran | Nilai |
|---|---:|
| Residual standard error | 0.4932 (df = 1097) |
| Multiple R² | 0.6403 |
| Adjusted R² | 0.6397 |
| F-statistic | 976.4 (df = 2 dan 1097) |
| p-value (uji F) | < 2.2e-16 |

### Tabel ANOVA

| Sumber | Df | Sum Sq | Mean Sq | F value | Pr(>F) |
|---|---:|---:|---:|---:|---|
| noise_level | 1 | 326.52 | 326.52 | 1342.14 | < 2.2e-16 |
| bullying | 1 | 148.58 | 148.58 | 610.75 | < 2.2e-16 |
| Residuals | 1097 | 266.88 | 0.24 | | |

### Keputusan Uji

| Hipotesis | Keputusan | Kesimpulan |
|---|---|---|
| H0₁ (kebisingan) | Ditolak (p < 0,05) | Kebisingan berpengaruh signifikan dan positif terhadap stres |
| H0₂ (perundungan) | Ditolak (p < 0,05) | Perundungan berpengaruh signifikan dan positif terhadap stres |
| H0₃ (simultan) | Ditolak (p < 0,05) | Keduanya bersama-sama berpengaruh signifikan terhadap stres |

## Key Findings

- Setiap kenaikan 1 satuan **kebisingan** meningkatkan tingkat stres rata-rata sebesar 0,21, dengan perundungan dianggap tetap.
- Setiap kenaikan 1 satuan **perundungan** meningkatkan tingkat stres rata-rata sebesar 0,30, dengan kebisingan dianggap tetap.
- Perundungan memiliki koefisien yang lebih besar dibanding kebisingan, sehingga pengaruhnya per satuan lebih kuat.
- Kedua variabel secara bersama-sama menjelaskan sekitar **64%** variasi tingkat stres (R² = 0,6403).
- Semakin tinggi kebisingan dan perundungan, semakin tinggi tingkat stres siswa.

## Visualization

| No. | Visualization |
|---|---|
| 1 | Pengaruh noise level terhadap stress level |
| 2 | Pengaruh bullying terhadap stress level |
| 3 | Pengaruh noise level dan bullying terhadap stress level (bidang regresi 3D interaktif) |
| 4 | Prediksi vs aktual stress level |

## Conclusion

- Hasil menunjukkan **keterkaitan statistik**, bukan hubungan sebab-akibat.
- `stress_level`, `noise_level`, dan `bullying` berupa skala bilangan bulat dari survei, sehingga model linear merupakan pendekatan sederhana. Pengecekan asumsi regresi (normalitas residual, homoskedastisitas, multikolinearitas) belum disertakan dalam analisis ini.
- Sum of squares pada tabel ANOVA bersifat sekuensial (urutan variabel memengaruhi nilainya).
- Grafik prediksi vs aktual dihitung pada data yang sama dengan data pelatihan model, bukan pada data uji terpisah.

## How to Run

1. Unduh dataset dari Kaggle dan simpan sebagai `StressLevelDataset.csv`.
2. Buka `script/analisis_stres.R` di RStudio, lalu ubah `setwd()` sesuai folder kamu.
3. Jalankan seluruh kode secara berurutan.

Kode inti:

```r
data <- read.csv("StressLevelDataset.csv", header = TRUE)
data_selected <- data[, c("noise_level", "bullying", "stress_level")]

model <- lm(stress_level ~ noise_level + bullying, data = data_selected)
summary(model)
anova(model)
```

Paket untuk visualisasi 3D:

```r
install.packages("plotly")
```
