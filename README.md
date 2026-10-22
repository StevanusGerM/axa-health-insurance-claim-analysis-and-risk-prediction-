# 🏥 Analisis dan Prediksi Klaim Asuransi Kesehatan Individu

Repositori ini berisi studi kasus, pembersihan data (*data cleaning*), eksplorasi (*EDA*), dan kerangka pemodelan untuk menganalisis tren serta faktor-faktor yang mempengaruhi klaim asuransi kesehatan. Proyek ini dilatarbelakangi oleh lonjakan klaim asuransi kesehatan sebesar 25.5% (Januari–Juni 2025 dibanding periode yang sama tahun 2024) yang berpotensi berdampak pada kenaikan harga premi.

---

## 📂 **Struktur Dataset**
Proyek ini menggabungkan dua sumber data utama:
1. **`Data_Klaim.csv`**: Berisi catatan transaksi klaim (ID Klaim, Nomor Polis, Jenis Klaim [Reimburse/Cashless], Layanan [Inpatient/Outpatient], Diagnosis ICD, Status Klaim, Tanggal Terkait, Nominal Klaim Disetujui, Biaya Rumah Sakit, dan Lokasi RS).
2. **`Data_Polis.csv`**: Berisi informasi profil peserta/pemegang polis (Nomor Polis, *Plan Code*, Jenis Kelamin, Tanggal Lahir, Tanggal Efektif Polis, dan Domisili).

---

## 🎯 **Tujuan Proyek**
1. Melakukan *Exploratory Data Analysis* (EDA) dan pembersihan data klaim asuransi.
2. Mengidentifikasi faktor utama yang mempengaruhi **severitas** (besaran biaya) klaim.
3. Mengidentifikasi faktor utama yang mempengaruhi **frekuensi** klaim.
4. Membangun model *Machine Learning* untuk memprediksi tren frekuensi, severitas, dan nominal klaim.
5. Mengevaluasi performa minimal 2 (dua) model *Machine Learning*.

---

## 🛠️ **Tahapan Penanganan Data (*Data Handling*)**
* **Imputasi *Missing Values*:**
  * **Inpatient/Outpatient:** Diimputasi berdasarkan *Length of Stay* (LOS) yang dihitung dari selisih tanggal masuk dan keluar rumah sakit.
  * **ICD Diagnosis & Description:** Menggunakan *deterministic rule-based imputation* (modus penyakit berdasarkan riwayat nomor polis yang bersangkutan).
  * **Tanggal Pembayaran Klaim:** Diisi menggunakan median keterlambatan pembayaran sejak pasien keluar RS berdasarkan kategori *Reimburse* atau *Cashless*.
  * **Lokasi RS:** Imputasi nilai kosong dengan kategori `'Others'`.
* **Reduksi Kardinalitas (High Cardinality):**
  * Kode diagnosis ICD-10 yang sangat beragam diringkas menggunakan *chapter prefix* (huruf depan ICD) untuk mempertahankan informasi medis utama tanpa menambah kompleksitas dimensi data.
* **Konsistensi Tipe Data:** Konversi seluruh kolom tanggal ke format `datetime` dan pembersihan data anomali (menghapus nilai nominal klaim atau biaya RS bernilai 0).

---

## 📊 **Eksplorasi Data (*EDA*)**
* Analisis distribusi nominal klaim yang disetujui dan biaya riil rumah sakit.
* Pemetaan sebaran lokasi rumah sakit (didominasi oleh fasilitas di Indonesia, Singapura, dan Malaysia).
* Analisis durasi perawatan (*Length of Stay*) terhadap besaran klaim.

---

## 🚀 **Cara Menjalankan**
Pastikan pustaka Python berikut telah terinstal di lingkungan kerja Anda:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels scipy
```
Jalankan notebook secara berurutan mulai dari bagian *Case Overview*, *Data Handling*, hingga *Exploratory Data Analysis*.
