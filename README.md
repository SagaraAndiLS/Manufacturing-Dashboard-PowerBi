# 🏭 Strategic Manufacturing Dashboard (Power BI)

Implementasi **Strategic Manufacturing Dashboard** untuk menganalisis kinerja produksi dan kualitas produk menggunakan **Microsoft Power BI**.

> Tugas praktikum mata kuliah **Kecerdasan Bisnis**
> Program Studi Sains Data, Fakultas Sains dan Teknologi, IKOPIN University (2026)
> Dosen Pengampu: Agus Nugraha, ST., M.Kom.
> Disusun oleh: **Sagara Andi Ladzuardi Suwarsa** (2C2220004)

---

## 📌 Latar Belakang

Data produksi dan kualitas di industri manufaktur sering tersimpan sebagai *raw data* dari berbagai sumber dengan format yang belum seragam. Akibatnya, manajemen kesulitan memantau kinerja produksi, mengevaluasi kualitas, dan mengidentifikasi faktor yang memengaruhi tingkat kecacatan (*defect*).

Proyek ini menjawab pertanyaan berikut:

1. Bagaimana tren produksi dari waktu ke waktu, dan apakah ada pola musiman?
2. Produk dan wilayah mana yang berkontribusi paling besar terhadap total produksi?
3. Bagaimana hubungan antara volume produksi dan tingkat kecacatan?
4. Faktor operasional apa yang perlu diperhatikan untuk meningkatkan efisiensi dan kualitas?

---

## 🖼️ Preview Dashboard

![Dashboard](images/dashboard.png)

KPI utama yang ditampilkan:

| KPI | Nilai |
|---|---|
| Total Quantity Produced | ± 483 ribu unit |
| Total Production Cost | ± 9,08 juta |
| Average Defect Rate | 2,75 % |

---

## 📂 Struktur Repository

```
manufacturing-dashboard-powerbi/
├── README.md                  # Dokumentasi proyek (file ini)
├── .gitignore
├── data/
│   ├── README.md              # Sumber & deskripsi dataset
│   └── raw/                   # Dataset mentah (xlsx / csv)
├── powerbi/
│   └── Strategic_Manufacturing_Dashboard.pbix
├── dax/
│   └── measures.dax           # Seluruh DAX measure
├── docs/
│   └── Laporan_Strategic_Manufacturing_Dashboard.pdf
└── images/
    ├── dashboard.png          # Tampilan dashboard
    ├── data-model.png         # Relationship antar tabel
    └── power-query/           # Screenshot proses ETL
```

---

## 🗃️ Sumber Data

| Dataset | Sumber | Kegunaan |
|---|---|---|
| **Manufacturing Performance** | [GitHub – abhijeet8825](https://github.com/abhijeet8825/Manufacturing_performance_Dashboard_PowerBI/blob/main/Data/ManufacturingDataset1.xlsx) | Data operasional harian: kuantitas, biaya, tipe produk, negara asal, lokasi gudang |
| **Predicting Manufacturing Defects** | [Kaggle – Rabie El Kharoua](https://www.kaggle.com/datasets/rabieelkharoua/predicting-manufacturing-defects-dataset) | Parameter mesin & kualitas: defect rate, downtime, quality score, worker productivity |

---

## 🔄 Metodologi

Pendekatan **Business Intelligence (BI)**:

1. **Data Connectivity** – import data Excel/CSV ke Power BI Desktop.
2. **ETL & Data Cleaning (Power Query)** – ubah tipe data, hapus kolom tidak relevan, tambah kolom waktu (Day, Month Name, Year).
3. **Data Modeling** – hubungkan kedua tabel melalui relationship.
4. **Analisis dengan DAX** – membuat measure untuk KPI dan metrik analitis.
5. **Visualisasi** – menyusun Strategic Manufacturing Dashboard.

### Preprocessing

| Dataset | Transformasi |
|---|---|
| manufacturing_dataset | `ProductionDate` → Date; `ProductionCost` → Whole Number; tambah kolom Day, Month Name, Year |
| manufacturing_defect_dataset | `DefectRate` & `DowntimePercentage` → Percentage; hapus kolom tidak relevan |

### Data Model

| Properti | Nilai |
|---|---|
| Tabel | `manufacturing_dataset[ProductionCost]` ↔ `manufacturing_defect_dataset[ProductionCost]` |
| Cardinality | One-to-one (1:1) |
| Cross-filter direction | Both |
| Status | Active |

---

## 🧮 DAX Measures

Daftar lengkap ada di [`dax/measures.dax`](dax/measures.dax). Ringkasan:

| Measure | Fungsi |
|---|---|
| Total Quantity Produced | Total unit yang diproduksi |
| Total Production Cost | Total biaya produksi |
| Monthly Production | Produksi bulan berjalan (`DATESMTD`) |
| Production by Product Type / Warehouse | Distribusi produksi per tipe produk & gudang |
| Production Cost by Country | Biaya produksi per negara |
| Production Trend | Tren produksi dari waktu ke waktu |
| Average Defect Rate (%) | Rata-rata tingkat kecacatan |
| Average Downtime (%) | Rata-rata downtime mesin |
| Average Quality Score | Rata-rata skor kualitas |
| Average Worker Productivity | Rata-rata produktivitas pekerja |
| Defect Rate by Volume | Defect rate terhadap volume produksi |

---

## 💡 Insight Utama

1. **Produksi keseluruhan** – ± 483 ribu unit dengan biaya ± 9,08 juta, menunjukkan aktivitas operasional yang tinggi.
2. **Tren produksi** – berfluktuasi dari awal 2023 sampai akhir 2025, tetapi tetap dalam rentang yang relatif stabil.
3. **Kinerja produk** – *Textiles* tertinggi, diikuti *Electronics* dan *Automobiles*; *Machinery* terendah.
4. **Distribusi wilayah** – gudang **West** berkontribusi terbesar, **South** terendah.
5. **Analisis kecacatan** – terdapat lonjakan defect rate pada volume produksi tertentu, sehingga kenaikan volume tidak selalu sejalan dengan kualitas. Pengendalian kualitas perlu diperketat pada periode produksi tinggi.

---

## ⚠️ Catatan & Keterbatasan

- Kedua dataset berasal dari **sumber yang berbeda** dan dihubungkan melalui kolom `ProductionCost`, yang bukan kunci unik sejati. Hubungan ini dipakai untuk kebutuhan praktikum, sehingga hasil analisis lintas dataset (mis. biaya vs defect) bersifat **eksploratif**, bukan bukti sebab-akibat.
- Dataset bersifat publik/simulasi dan tidak mewakili data perusahaan nyata.

---

## ▶️ Cara Membuka Proyek

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Windows).
2. Clone repository ini:
   ```bash
   git clone https://github.com/<username>/manufacturing-dashboard-powerbi.git
   ```
3. Buka `powerbi/Strategic_Manufacturing_Dashboard.pbix`.
4. Jika Power BI meminta lokasi data, arahkan ke folder `data/raw/` melalui **Transform data → Data source settings**.

---

## 🛠️ Teknologi

- Microsoft Power BI Desktop (Power Query, DAX, Data Modeling)
- Microsoft Excel / CSV
- Git & GitHub

---

## 📚 Referensi

- abhijeet8825. *Manufacturing_performance_Dashboard_PowerBI*. GitHub.
- Kharoua, R. E. *Predicting Manufacturing Defects Dataset*. Kaggle.

## 📄 Lisensi

Proyek ini dibuat untuk keperluan akademik. Dataset tetap mengikuti lisensi dari pemilik aslinya masing-masing.
