# **LAPORAN ANALISIS DATA UNIVERSITAS MENGGUNAKAN KNIME**

## **1. Pendahuluan**

Proyek ini dilakukan untuk memenuhi tugas UAS dengan tujuan membangun sebuah workflow analisis data menggunakan KNIME. Analisis dilakukan pada dataset universitas dengan tahapan meliputi data preparation, data processing, visualisasi, hingga klasifikasi menggunakan algoritma Decision Tree. Selain menghasilkan model prediksi, proyek ini juga memberikan insight berbasis visualisasi serta interpretasi terhadap pola yang ditemukan pada dataset.

---

## **2. Dataset**

Dataset yang digunakan berisi informasi mengenai berbagai universitas, termasuk variabel:

* Faculty Ratio
* Tuition
* Graduation Rate
* Percent PhD Faculty
* Acceptance Rate
  dan beberapa variabel numerik terkait kualitas institusi.

Dataset diinputkan melalui node **CSV Reader** di KNIME.

---

## **3. Metodologi Workflow di KNIME**

### **3.1 Data Preparation**

Tahapan ini bertujuan menyiapkan data agar siap dianalisis dan dimodelkan.
Node yang digunakan:

1. **CSV Reader**
   Digunakan untuk membaca dataset mentah.
2. **Missing Value**
   Mengatasi nilai kosong pada kolom numerik.
3. **Column Filter**
   Memilih kolom yang diperlukan untuk analisis visual dan modeling.
4. **Rule Engine (Pembuatan Label)**
   Digunakan untuk membuat variabel kategori berdasarkan Graduation Rate:

   * “High” jika Graduation Rate ≥ 70
   * “Low” jika < 70
5. **Normalizer**
   Menormalkan variabel numerik agar memiliki skala yang seragam.

---

### **3.2 Exploratory Data Analysis (EDA)**

Visualisasi dilakukan untuk memahami pola dasar dalam data.
Node yang digunakan:

* **Statistics** – Menampilkan ringkasan statistik seperti mean, median, minimum, maksimum, dan standar deviasi.
* **Linear Correlation** – Mengetahui hubungan antar variabel numerik.
* **Box Plot** – Membandingkan Tuition pada kategori High vs Low Graduation Rate.
* **Scatter Plot** – Menganalisis hubungan antara **Faculty Ratio** dan **Graduation Rate**.

---

### **3.3 Pembagian Data (Train-Test Split)**

Karena node *Partitioning* tidak tersedia, digunakan node:

* **Row Sampler**

  * *Top fraction* (~70%) → Data Training
  * *Bottom fraction* (~30%) → Data Testing

Kedua bagian dapat dinormalisasi ulang jika diperlukan.

---

### **3.4 Modeling**

1. **Decision Tree Learner**

   * Input: Data training
   * Target: Label High/Low yang dibuat melalui Rule Engine
   * Output: Model klasifikasi berbasis pohon keputusan

2. **Decision Tree Predictor**

   * Input: Data testing
   * Output: Prediksi kategori High/Low untuk setiap baris data

---

### **3.5 Evaluasi Model**

Evaluasi dilakukan menggunakan node:

* **Scorer**
  Menghasilkan confusion matrix, accuracy, precision, dan recall.

Contoh hasil (sesuai workflow):

* Prediksi High dan Low sepenuhnya akurat terhadap data uji
* Tidak ditemukan misclassification (nilai 0 pada false positive dan false negative)

---

### **3.6 Visualisasi Model**

* **Decision Tree to Image**
  Digunakan untuk menampilkan struktur pohon keputusan dalam bentuk gambar yang mudah dipresentasikan.

---

## **4. Hasil dan Insight**

### **4.1 Insight dari Scatter Plot (Faculty Ratio vs Graduation Rate)**

* Terlihat pola bahwa universitas dengan **Faculty Ratio lebih baik** (lebih banyak dosen per mahasiswa) cenderung memiliki **Graduation Rate yang lebih tinggi**.
* Titik data kategori “High” lebih banyak muncul pada Faculty Ratio yang rendah (rasio ideal).
* Sebaliknya, universitas dengan Faculty Ratio tinggi (dosen lebih sedikit) lebih sering masuk kategori “Low”.

---

### **4.2 Insight dari Box Plot (Tuition vs Graduation Rate)**

* Kategori “High Graduation Rate” umumnya memiliki nilai Tuition yang lebih tinggi.
* Hal ini menunjukkan bahwa universitas dengan biaya kuliah lebih tinggi cenderung memiliki fasilitas dan kualitas akademik yang lebih baik.
* Kategori “Low” memiliki rentang tuition yang lebih rendah secara konsisten.

---

### **4.3 Insight dari Model Klasifikasi (Decision Tree)**

* Model Decision Tree mampu membedakan kategori High dan Low dengan akurasi sempurna.
* Hal ini mengindikasikan bahwa variabel input, terutama Faculty Ratio, memiliki pengaruh signifikan terhadap Graduation Rate.
* Struktur pohon menunjukkan bahwa pemisahan berdasarkan Faculty Ratio dan variabel terkait sangat efektif membentuk dua grup kelulusan.

---

### **4.4 Insight dari Scatter Plot (Graduation Rate vs New Stud from Top 10%)**

Terdapat korelasi positif yang kuat antara persentase mahasiswa baru dari 10% teratas SMA dengan tingkat kelulusan (Graduation Rate).
Universitas yang menerima mahasiswa dengan kualitas akademik tinggi (berasal dari top 10%) cenderung memiliki Graduation Rate yang lebih tinggi (di atas 60-80%).
Sebaliknya, universitas dengan proporsi mahasiswa top 10% yang rendah (0-30%) cenderung memiliki Graduation Rate yang lebih rendah dan tersebar (20-50%).
Interpretasi: Kualitas input mahasiswa merupakan faktor penting yang memengaruhi keberhasilan kelulusan. Universitas dengan seleksi masuk yang lebih ketat dan menerima siswa berkualitas tinggi memiliki peluang lebih besar untuk menghasilkan lulusan tepat waktu.
Pola ini menunjukkan bahwa kemampuan awal mahasiswa menjadi prediktor yang signifikan terhadap tingkat kelulusan institusi.

## **5. Kesimpulan**

Melalui workflow pada KNIME, proses analisis data dapat berjalan secara sistematis mulai dari pembersihan data, eksplorasi visual, pembuatan label, normalisasi, pembagian data, pembangunan model hingga evaluasi.
Hasil analisis menunjukkan bahwa:

* **Faculty Ratio berhubungan kuat dengan Graduation Rate**, dan menjadi indikator penting untuk memprediksi performa universitas.
* Universitas dengan Tuition lebih tinggi cenderung memiliki Graduation Rate yang lebih baik.
* Model Decision Tree yang dibangun memberikan kinerja sempurna pada dataset ini, menunjukkan pola data yang sangat terstruktur.

Workflow ini berhasil memberikan insight yang informatif dan model klasifikasi yang akurat.

---

## **6. Lampiran**

1. **Screenshot lengkap workflow KNIME**
   ![Decision Tree Output](https://github.com/c14250136-cmd/LAPORAN-ANALISIS-DATA-UNIVERSITAS-MENGGUNAKAN-KNIME/blob/main/Screenshot%202025-12-03%20113041.png)
3. **Screenshot Statistics node**
   ![Decision Tree Output](https://github.com/c14250136-cmd/LAPORAN-ANALISIS-DATA-UNIVERSITAS-MENGGUNAKAN-KNIME/blob/main/Screenshot%202025-12-03%20102851.png)
5. **Screenshot Linear Correlation**
   ![Decision Tree Output](https://github.com/c14250136-cmd/LAPORAN-ANALISIS-DATA-UNIVERSITAS-MENGGUNAKAN-KNIME/blob/main/Screenshot%202025-12-03%20102641.png)
7. **Screenshot Box Plot (Tuition vs Graduation Rate)**
   ![Decision Tree Output](https://github.com/c14250136-cmd/LAPORAN-ANALISIS-DATA-UNIVERSITAS-MENGGUNAKAN-KNIME/blob/main/Screenshot%202025-12-03%20103000.png)
9. **Screenshot Scatter Plot (Faculty Ratio vs Graduation Rate)**
    ![Decision Tree Output](https://github.com/c14250136-cmd/LAPORAN-ANALISIS-DATA-UNIVERSITAS-MENGGUNAKAN-KNIME/blob/main/Screenshot%202025-12-03%20103132.png)
11. **Screenshot Scatter Plot (Graduation Rate vs New Stud from Top 10%)**
    ![Decision Tree Output](https://github.com/c14250136-cmd/LAPORAN-ANALISIS-DATA-UNIVERSITAS-MENGGUNAKAN-KNIME/blob/main/Screenshot%202025-12-03%20111354.png)
13. **Screenshot Decision Tree Predictor**
    ![Decision Tree Output](http://github.com/c14250136-cmd/LAPORAN-ANALISIS-DATA-UNIVERSITAS-MENGGUNAKAN-KNIME/blob/main/Screenshot%202025-12-03%20113839.png)
15. **Screenshot Scorer (confusion matrix)**
    ![Decision Tree Output](https://github.com/c14250136-cmd/LAPORAN-ANALISIS-DATA-UNIVERSITAS-MENGGUNAKAN-KNIME/blob/main/Screenshot%202025-12-03%20114058.png)
17. **Gambar Decision Tree (hasil dari Decision Tree to Image)**
    ![Decision Tree Output](https://github.com/c14250136-cmd/LAPORAN-ANALISIS-DATA-UNIVERSITAS-MENGGUNAKAN-KNIME/blob/main/Screenshot%202025-12-03%20114135.png)
