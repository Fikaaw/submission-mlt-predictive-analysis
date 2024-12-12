# Laporan Proyek Machine Learning - Ida Sri Afiqah

## Domain Proyek

Proyek ini berfokus pada bidang kesehatan, khususnya memprediksi risiko obesitas pada individu. Dengan meningkatnya prevalensi obesitas dan dampaknya terhadap kesehatan global, identifikasi faktor risiko dan pengembangan model prediktif menjadi langkah penting untuk pencegahan serta intervensi. Data yang digunakan mencakup variabel seperti riwayat keluarga dengan obesitas, kebiasaan makan, aktivitas fisik, dan lainnya, yang kemudian dianalisis untuk mengembangkan wawasan dan rekomendasi.

## Business Understanding

### Problem Statements
- Bagaimana mengidentifikasi faktor utama risiko obesitas?
- Bagaimana membangun model prediktif akurat untuk klasifikasi obesitas?

### Goals
- Mengidentifikasi dan menganalisis minimal 3 faktor utama yang memiliki korelasi kuat dengan risiko obesitas
- Mengembangkan model prediktif dengan tingkat akurasi minimal 85% untuk mengklasifikasikan tingkat obesitas seseorang

### Solution statements
1. Untuk menjawab masalah pertama:
   * Melakukan analisis eksploratori data (EDA) untuk mengidentifikasi pola dan korelasi antar variabel
   * Menggunakan feature importance dari model machine learning untuk menentukan faktor-faktor yang paling berpengaruh

2. Untuk menjawab masalah kedua:
   * Mengembangkan dan membandingkan beberapa model machine learning (Decision Tree, XGBoost, Random Forest, SVM, Logistic Regression, LightGBM )
   * Melakukan evaluasi model menggunakan metrik yang sesuai (akurasi, presisi, recall, dan F1-score) dan memilih model terbaik berdasarkan hasil evaluasi


## Data Understanding
*Dataset yang digunakan pada proyek ini:*  
https://www.kaggle.com/competitions/playground-series-s4e2/data

### Dataset diperoleh dari Kaggle Playground Series yang memuat 17 fitur, termasuk:
- Age, Height, Weight: variabel numerik.
- family_history_with_overweight, FAVC: variabel kategorikal.
- NObeyesdad: target klasifikasi dengan 7 kelas.

### Explorasi Data

1. Corellation Matrix

Correlation matrix diatas merepresentasikan hubungan antar fitur, berikut adalah analisisnya:
- Age dan BMI memiliki korelasi positif sangat kuat
- TUE dan Age memiliki korelasi negatif sangat kuat
- FAF dan BMI memiliki korelasi negatif sangat kuat
- FAF dan Age memiliki korelasi negatif sangat kuat
- TUE dan BMI memiliki korelasi negatif sangat kuat

2. Histogram

Histogram-histogram di atas merepresentasikan distribusi data untuk sembilan fitur, berikut analisisnya:
- Age: Distribusi skewed ke kiri, sebagian besar data berada pada rentang usia 20-30 tahun.
- Height dan Weight: Terdistribusi normal, dengan puncak sekitar tinggi 1.7 meter dan berat 70-90 kg.
- FCVC (Frekuensi konsumsi sayur), NCP (Jumlah porsi), dan CH2O (Asupan air): Distribusi sangat terpusat pada nilai diskrit tertentu, menunjukkan perilaku konsumsi konsisten di beberapa level.
- FAF (Frekuensi aktivitas fisik) dan TUE (Waktu penggunaan teknologi): Skewed, banyak data mendekati nilai 0 untuk aktivitas fisik, sedangkan TUE lebih terdistribusi rata.
- BMI: Distribusi mirip normal dengan puncak sekitar nilai 25-30, menandakan dominasi individu overweight atau obesitas.

3. Rata-Rata BMI Berdasarkan Kategori Obesitas

Gambar diatas menunjukkan Tren BMI dan Obesitas:
- BMI rata-rata tertinggi ditemukan pada kategori Obesity_Type_III (di atas 40), menunjukkan kondisi obesitas paling parah.
- BMI menurun secara bertahap dari kategori obesitas parah hingga Normal_Weight dan Insufficient_Weight.
- Pola ini sejalan dengan klasifikasi BMI di mana nilai lebih tinggi menunjukkan tingkat obesitas yang lebih parah.

4. Distribusi Jenis Kelamin

- Data menunjukkan distribusi hampir seimbang antara Female (50.2%) dan Male (49.8%).

## Data Preparation
- Melakukan encoding untuk fitur kategorikal seperti Gender, family_history_with_overweight, FAVC, FCVC, CAEC, SMOKE, SCC, CALC, MTRANS. Kita perlu melakukan encoding pada fitur kategorikal karena algoritma machine learning umumnya hanya dapat memproses data numerik. Dengan melakukan encoding, kita mengubah variabel kategorikal menjadi representasi numerik yang dapat dipahami oleh model.
- Melakukan standarisasi atau normalisasi untuk fitur-fitur numerik seperti Age, Height, Weight, NCP, CH2O, FAF, TUE. Standarisasi atau normalisasi diperlukan untuk memastikan bahwa semua fitur numerik memiliki skala yang seragam.
- Melakukan Split Data, dataset yang ada dibagi menjadi 2 bagian yaitu data latih dan data uji dengan rasio 80:10. Proses ini dilakukan dengan menggunakan modul train_test_split dari library scikit-learn.

## Modeling

1. Decision Tree
Keunggulan: Interpretasi yang mudah dan mendukung data kategorikal serta numerik[1].

Hasil: Training metrics menunjukkan akurasi sempurna (1.0), tetapi testing metrics lebih rendah (akurasi 83.67%). Model cenderung overfitting pada data training.

2. XGBoost
Keunggulan: Cepat, efisien, dan mampu mengurangi overfitting[2].

Hasil: Testing metrics lebih baik dengan akurasi 89.86%. Model ini lebih seimbang antara performa training dan testing dibandingkan Decision Tree.

3. Random Forest
Keunggulan: Stabil dan tahan terhadap noise.

Hasil: Akurasi testing 89.69% dengan stabilitas tinggi pada beberapa kelas, tetapi cenderung overfit pada data training.

4. Support Vector Machine (SVM)
Keunggulan: Efektif untuk data dengan dimensi tinggi.

Hasil: Testing metrics menunjukkan akurasi 88%, dengan performa baik pada kelas dominan tetapi sedikit kesulitan pada kelas yang lebih kecil.

5. Logistic Regression
Keunggulan: Interpretasi mudah dan sederhana.

Hasil: Akurasi testing 87% dengan performa baik pada beberapa kelas, tetapi kurang efektif dibandingkan metode berbasis pohon seperti XGBoost.

6. LightGBM
Keunggulan: Waktu pelatihan cepat dan performa optimal.

Hasil: Akurasi testing 90%, dengan performa terbaik secara keseluruhan dan minim overfitting.


## Evaluation

### Metrik Evaluasi
Akurasi: Persentase prediksi benar.
Presisi, Recall, F1-Score: Mengukur keseimbangan antara prediksi benar dan salah.

### Hasil Evaluasi

- Pengembangan model prediktif obesitas dapat membantu identifikasi individu berisiko tinggi. 
- Performa terbaik: LightGBM memberikan akurasi tertinggi pada data testing dengan keseimbangan baik antara training dan testing.
- Overfitting: Decision Tree dan Random Forest cenderung overfit pada data training.
- Keandalan: XGBoost dan LightGBM lebih andal dalam mengatasi data yang kompleks.

## Referensi

[1] F. Pedregosa et al., "Scikit-learn: Machine Learning in Python," JMLR, 2011.
[2] T. Chen, C. Guestrin, "XGBoost: A Scalable Tree Boosting System," KDD, 2016.
[3] L. Breiman, "Random Forests," Machine Learning, 2001.
[4] B. Scholkopf et al., "Comparing Support Vector Machines," Neural Computation, 2000.
[5] D. W. Hosmer, S. Lemeshow, "Applied Logistic Regression," Wiley, 1989.
[6] G. Ke et al., "LightGBM: A Highly Efficient Gradient Boosting Decision Tree," NeurIPS, 2017.




