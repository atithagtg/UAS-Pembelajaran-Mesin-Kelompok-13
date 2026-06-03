# Prediksi Konsumsi Energi Bangunan Menggunakan Machine Learning

## Deskripsi Proyek
Proyek ini bertujuan untuk memprediksi konsumsi energi bangunan berdasarkan karakteristik bangunan, faktor cuaca, dan pola waktu menggunakan pendekatan Machine Learning.

Analisis dilakukan dengan menggabungkan data konsumsi energi bangunan (`train.csv`), metadata bangunan (`building_metadata.csv`), dan data cuaca (`weather_train.csv`). Selain itu, dilakukan penyesuaian preprocessing agar lebih relevan dengan kondisi Indonesia, khususnya pada variabel temperatur udara.

---

## Tujuan Proyek
1. Melakukan eksplorasi data (EDA) untuk memahami pola konsumsi energi bangunan.
2. Mengidentifikasi pengaruh faktor bangunan, cuaca, dan waktu terhadap konsumsi energi.
3. Melakukan preprocessing data agar lebih sesuai untuk pemodelan Machine Learning.
4. Membangun model prediksi konsumsi energi bangunan.


## Dataset
Dataset yang digunakan terdiri dari:

| Dataset | Deskripsi |
| `train.csv` | Data konsumsi energi bangunan |
| `building_metadata.csv` | Informasi karakteristik bangunan |
| `weather_train.csv` | Data cuaca berdasarkan lokasi dan waktu |

Dataset berukuran besar sehingga tidak diunggah ke repository GitHub.

## Tahapan Pengerjaan

### 1. Data Loading
- Memuat dataset utama
- Optimasi penggunaan memori (`reduce_mem_usage()`)

### 2. Data Merging
- Menggabungkan data bangunan dengan data konsumsi energi
- Menggabungkan data cuaca berdasarkan:
  - `site_id`
  - `timestamp`

### 3. Exploratory Data Analysis (EDA)
Analisis dilakukan terhadap:

#### Distribusi Target
- Distribusi `meter_reading`
- Log distribution untuk melihat skewness

#### Analisis Temporal
- Konsumsi energi berdasarkan jam
- Konsumsi energi berdasarkan hari
- Konsumsi energi berdasarkan bulan

#### Analisis Bangunan
- Konsumsi energi berdasarkan fungsi bangunan (`primary_use`)
- Luas bangunan (`square_feet`)

#### Analisis Cuaca
- Air temperature
- Dew temperature
- Wind speed
- Sea level pressure

#### Korelasi Variabel
- Hubungan antar variabel numerik terhadap konsumsi energi

---

## Preprocessing
Tahapan preprocessing yang dilakukan:

### Missing Value Handling
- `wind_direction` dihapus
- `floor_count` dihapus karena memiliki missing value sangat tinggi (~79%)

Missing value lain ditangani menggunakan median imputation:

- `year_built`
- `cloud_coverage`
- `precip_depth_1_hr`
- `sea_level_pressure`
- `wind_speed`
- `dew_temperature`

### Filtering Temperatur Indonesia
Dilakukan filtering suhu udara agar lebih relevan dengan kondisi Indonesia.

Rentang temperatur disesuaikan berdasarkan referensi BMKG dan distribusi data: 15°C – 40°C

Pertimbangan:
- Mayoritas wilayah Indonesia memiliki suhu tropis
- Suhu sangat rendah hanya terjadi pada daerah tertentu seperti dataran tinggi Dieng dan jaya wijaya
- Temperatur ekstrem tinggi dapat mencapai hampir 40°C pada wilayah tertentu

### Feature Engineering
Ekstraksi fitur waktu dari `timestamp`:

- `hour`
- `dayofweek`
- `month`
- `is_weekend`