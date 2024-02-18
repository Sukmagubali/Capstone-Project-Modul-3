Model Prediction Saudi Arabia Used Cars
[Sumber data Saudia Arabia Used Cars](https://drive.google.com/drive/folders/1_fR7R0srpZgnFnanbrmELgnK-xmzMAHp) 

### **Contents**

1. Business Problem Understanding
2. Data Understanding
3. Data Preprocessing
4. Modeling
5. Conclusion
6. Recommendation

****
### **Business Problem Understanding**
**Context**

Pasar mobil bekas di Arab Saudi terus mengalami pertumbuhan seiring dengan perubahan dinamika ekonomi dan preferensi konsumen. Dalam beberapa tahun terakhir, meningkatnya permintaan akan mobil bekas mencerminkan dorongan konsumen untuk memiliki kendaraan pribadi tanpa harus mengeluarkan biaya sepenuhnya untuk membeli mobil baru. Faktor-faktor seperti perubahan kondisi keuangan atau kebutuhan mobilitas sehari-hari dapat menjadi pendorong bagi konsumen untuk menjelajahi opsi mobil bekas.
**Problem Statement**

Dalam konteks dataset mobil bekas dari syarah.com, terdapat 5624 rekam data mobil bekas yang mencakup informasi tentang berbagai aspek. Tantangan utama yang dihadapi adalah kesulitan dalam menentukan harga yang optimal untuk mobil bekas. Faktor-faktor seperti jenis transmisi, tipe mobil, jarak tempuh, dan opsi tambahan dapat mempengaruhi harga yang juga menjadi variabel penting. Dalam konteks ini, perlu dikembangkan metode atau model yang dapat memberikan estimasi harga yang akurat dan transparan berdasarkan fitur-fitur mobil bekas yang terdapat dalam dataset, sehingga dapat meningkatkan kejelasan dalam proses jual-beli mobil bekas.
**Goals**

Berdasarkan tantangan penentuan harga optimal pada mobil bekas, diperlukan pengembangan alat atau model prediksi harga yang dapat membantu penjual untuk **menetapkan harga jual yang tepat untuk setiap mobil yang akan dijual**. Dengan mempertimbangkan variasi fitur pada setiap mobil, seperti kondisi mesin, tahun produksi, dan opsi tambahan, prediksi harga yang lebih akurat dapat meningkatkan potensi keuntungan bagi penjual dan tetap bersaing di pasar. Untuk platform mobil bekas, alat prediksi yang memberikan estimasi harga yang adil dapat meningkatkan jumlah penjual dan kendaraan yang terdaftar, yang pada akhirnya dapat meningkatkan pendapatan melalui biaya transaksi, baik dari penjual maupun pembeli.
**Analytic Approach**

Dalam tahap analisis ini, langkah awal dilakukan melalui eksplorasi data untuk mengungkap pola atau perbedaan di antara fitur-fitur yang ada. Proses eksplorasi ini bertujuan memberikan wawasan mendalam mengenai faktor-faktor yang berpotensi memengaruhi harga mobil bekas.

Setelah berhasil mengidentifikasi pola-pola tersebut, langkah selanjutnya adalah merancang dan membangun model regresi. Model ini berperan sebagai alat prediksi harga mobil bekas, dengan fokus utama pada mencegah harga yang terlalu tinggi (overpriced) atau terlalu rendah (underpriced). Pemanfaatan regresi memungkinkan kita untuk menemukan korelasi antara fitur-fitur spesifik dan harga, sehingga pengguna dapat memperoleh estimasi harga yang lebih akurat.
**Metric Evaluation**

Dalam membangun model machine learning ini, diperlukan beberapa evaluasi metrik sebagai berikut :
- RMSE      : Nilai rataan akar kuadrat dari error.
- MAE       : Rataan nilai absolut dari error.
- MAPE      : Rataan persentase error yang dihasilkan oleh suatu model regresi.
- R-Square  : Menjelaskan seberapa besar variasi nilai Y yang dapat dijelaskan oleh model.

Model akan semakin akurat dalam memprediksi harga suatu mobil bekas sesuai dengan limitasi fitur yang dipakai apabila nilai R-Square semakin mendekati nilai 1 dan nilai RMSE, MAE, dan MAPE yang dihasilkan semakin kecil.
### **Data Understanding**
- Dataset berisi catatan mobil bekas yang dikumpulkan dari syarah.com
- Setiap catatan mewakili satu mobil bekas, memberikan detail seperti nama merek, model, tahun pembuatan, asal, opsi, kapasitas mesin, jenis transmisi, jarak tempuh, harga di wilayah tertentu, dan status negosiasi.

**Attributes Information**

| Attribute | Data Type, Length | Description |
| --- | --- | --- |
| Type | Text | Jenis Mobil Bekas |
| Region | Text | Wilayah geografis tempat mobil bekas ditawarkan |
| Make | Text | Nama perusahaan yang memproduksu mobil |
| Gear_Type | Text | Ukuran jenis transmisi mobil |
| Origin | Text | Asal mobil bekas (Gulf / Saudi / Other) |
| Options | Text | Berbagai opsi yang tersedia pada mobil  (Full Options / Semi-Full / Standard) |
| Year | Int | Tahun pembuatan mobil |
| Engine_Size | Float | Ukuran mesin mobil |
| Mileage | Int | Jarak tempuh yang telah ditempuh mobil (dalam km) |
| Negotiable | Bool| Indikator biner (True/False) menunjukkan negosiasi, dengan True menandakan harga yang dapat dinegosiasikan (jika harga 0) |
| Price | Int | Harga yang tertera pada mobil (dalam Riyal) |


### **Data Preprocessing**
Pada tahap ini, kita akan melakukan cleaning pada data yang nantinya data yang sudah dibersihkan akan kita gunakan untuk proses analisis selanjutnya. Beberapa hal yang perlu dilakukan adalah:
- Drop fitur yang tidak memiliki relevansi terhadap permasalahan yang sedang dihadapi. 
- Melakukan treatment terhadap missing value jika ada. Bisa dengan cara men-drop fiturnya jika memang tidak dibutuhkan atau bisa juga dengan mengimputasi dengan nilai yang paling masuk akal berdasarkan kasusnya.
- Mengubah data type yang belum sesuai

**Data Correlation**

Berdasarkan matriks korelasi, kita dapat menyimpulkan bahwa tidak ada fitur yang memiliki korelasi yang signifikan dengan fitur Price. Korelasi tertinggi terjadi antara fitur Year dengan Price. Secara umum, nilai korelasi cenderung positif, namun pada fitur Mileage, korelasinya memiliki arah yang berlawanan.

![image](https://github.com/Sukmagubali/Capstone-Project-Modul-3/assets/151388496/1cd60a64-209d-46ec-a2ef-7377b98de3aa)

Berdasarkan hasil Variance Inflation Factor (VIF), disimpulkan bahwa tidak terdapat indikasi signifikan dari multicollinearity antara variabel "Year", "Engine_Size", "Mileage", dan "Price" dalam model. Semua fitur memiliki nilai VIF di bawah 5, menunjukkan tidak adanya masalah multicollinearity yang signifikan. Oleh karena itu, fitur-fitur tersebut dapat dimasukkan ke dalam model tanpa kekhawatiran tentang masalah multicollinearity.

### **Modeling**
Pada tahapan ini akan digunakan 3 base model dan 3 ensamble model yang akan dipertimbangkan. Model tersebut adalah sebagai berikut :
- **Base Model** (Linier Regression, KNN, Desicion Tree)
- **Ensamble Model** (Random Forest Regression, Gradient Boosting Regression, Xtreme Gradient Boosting Regessor)

**Encoding**

Berdasarkan data yang tersedia, terdapat 5 variabel kategorikal yang perlu diubah menjadi numerikal agar dapat dimanfaatkan dalam pembuatan model. Dalam pemilihan metode encoding, kita mempertimbangkan sifat fitur-fitur tersebut seperti sebagai berikut :

1. One-Hot Encoding untuk variabel `Gear_Type` karena memiliki nilai unik yang berbeda namun tidak memiliki urutan hierarki.  
2. Ordinal Encoding untuk variabel `Options`,  karena nilai-nilainya memiliki tingkatan atau tingkat hierarki yang dapat diurutkan, seperti 'Standard' mungkin merupakan opsi yang lebih dasar atau standar daripada 'Semi Full' dan 'Full'. 
3. Binary Encoding lebih cocok digunakan untuk variabel `Type`, `Region`, dan `Make` karena memiliki nilai unik yang beragam dan tidak memiliki hubungan ordinal yang dapat diurutkan.

![image](https://github.com/Sukmagubali/Capstone-Project-Modul-3/assets/151388496/cc40f1ff-d15e-4d14-87c7-9d0db8fff6d1)

Berdasarkan analisis ini, model Extreme Gradient Boost memiliki kinerja terbaik dengan skor evaluasi yang lebih rendah dan nilai R2 yang lebih tinggi, menunjukkan kemampuan yang lebih baik dalam menjelaskan variasi dalam data target.

#### **Extreme Gradient Boost**
Extreme Gradient Boosting (XGBoost) adalah algoritma machine learning yang merupakan pengembangan dari Gradient Boosting Machine (GBM). XGBoost menggunakan teknik ensemble learning untuk meningkatkan kinerja model prediksi. Algoritma ini bekerja dengan cara menggabungkan beberapa model prediksi yang lemah (weak learners) menjadi satu model yang lebih kuat (strong learner).

XGBoost memiliki beberapa keunggulan, antara lain:
1. **Skalabilitas**: XGBoost dapat diimplementasikan pada dataset yang besar dengan cepat dan efisien.
2. **Regularisasi**: Algoritma ini memiliki mekanisme regularisasi yang dapat mengurangi overfitting.
3. **Penanganan Missing Values**: XGBoost dapat menangani missing values secara otomatis.
4. **Penanganan Variabel Kategorikal**: XGBoost dapat menangani variabel kategorikal tanpa perlu melakukan encoding terlebih dahulu.
5. **Performa yang Tinggi**: XGBoost sering kali memberikan hasil yang lebih baik dibandingkan dengan algoritma machine learning lainnya.

XGBoost juga memiliki beberapa parameter yang dapat diatur untuk meningkatkan kinerja model, seperti learning rate, jumlah pohon (n_estimators), kedalaman pohon (max_depth), dan lain-lain.

#### **Extreme Gradient Boost**
Extreme Gradient Boosting (XGBoost) adalah algoritma machine learning yang merupakan pengembangan dari Gradient Boosting Machine (GBM). XGBoost menggunakan teknik ensemble learning untuk meningkatkan kinerja model prediksi. Algoritma ini bekerja dengan cara menggabungkan beberapa model prediksi yang lemah (weak learners) menjadi satu model yang lebih kuat (strong learner).

XGBoost memiliki beberapa keunggulan, antara lain:
1. **Skalabilitas**: XGBoost dapat diimplementasikan pada dataset yang besar dengan cepat dan efisien.
2. **Regularisasi**: Algoritma ini memiliki mekanisme regularisasi yang dapat mengurangi overfitting.
3. **Penanganan Missing Values**: XGBoost dapat menangani missing values secara otomatis.
4. **Penanganan Variabel Kategorikal**: XGBoost dapat menangani variabel kategorikal tanpa perlu melakukan encoding terlebih dahulu.
5. **Performa yang Tinggi**: XGBoost sering kali memberikan hasil yang lebih baik dibandingkan dengan algoritma machine learning lainnya.

XGBoost juga memiliki beberapa parameter yang dapat diatur untuk meningkatkan kinerja model, seperti learning rate, jumlah pohon (n_estimators), kedalaman pohon (max_depth), dan lain-lain.
Dari perbandingan nilai metrik evaluasi antara data train dan test pada model Extreme Gradient Boost, dapat disimpulkan bahwa tidak ada perbedaan yang signifikan, menunjukkan bahwa model cenderung tidak mengalami overfitting. Kesimpulan tersebut mendukung ide untuk melakukan hyperparameter tuning dengan tujuan meningkatkan kinerja model pada data test.

Setelah melakukan *hyperparameter tuning* pada model Extreme Gradient Boost, diperoleh perubahan sebagai berikut:

- Nilai terbaik (*best_score*) yang berhasil dicapai adalah -11457.24.
- Kombinasi parameter terbaik yang menghasilkan nilai tersebut adalah:
  - "learning_rate" sebesar 0.05,
  - "max_depth" sebesar 7, dan
  - "n_estimators" sebesar 300.
- Hasil ini menunjukkan bahwa model dengan pengaturan parameter tersebut memberikan kinerja optimal dengan nilai *score* yang rendah, menandakan performa prediksi yang baik.

Proses selanjutnya setelah menentukan parameter terbaik melalui *hyperparameter tuning* adalah menerapkan perubahan tersebut ke dalam model yang telah dibangun.

![image](https://github.com/Sukmagubali/Capstone-Project-Modul-3/assets/151388496/0862413e-2dad-4c5d-b52a-571446962711)

![image](https://github.com/Sukmagubali/Capstone-Project-Modul-3/assets/151388496/79603555-1567-4b82-a0f3-b2025bb167ff)

**Limitasi**

Limitasi pada model berdasarkan gambaran informasi fitur (Year, Engine_Size, Mileage) dan label (Price) yang diberikan adalah sebagai berikut:

Berdasarkan informasi tersebut, berikut adalah limitasi model yang direkomendasikan:

1. **Year (Tahun Produksi):**
   - Rentang nilai: 2000 - 2021.
   - Dapat dibatasi untuk mempertimbangkan mobil dengan tahun produksi antara kuartil pertama (Q1) dan kuartil ketiga (Q3), yaitu tahun 2014 - 2018.

2. **Engine_Size (Ukuran Mesin):**
   - Rentang nilai: 1.0 - 6.4.
   - Dapat dibatasi untuk mempertimbangkan mobil dengan ukuran mesin di antara kuartil pertama (Q1) dan kuartil ketiga (Q3), yaitu 2.0 - 3.8.

3. **Mileage (Jarak Tempuh):**
   - Rentang nilai: 1200 - 801500 km
   - Dapat dibatasi untuk mempertimbangkan mobil dengan jarak tempuh di antara kuartil pertama (Q1) dan kuartil ketiga (Q3), yaitu 70000- 198000 km.

4. **Price (Harga):**
   - Rentang nilai: 4,500 - 182,000 SAR.
   - Dapat dibatasi untuk mempertimbangkan mobil dengan harga tertentu, Berdasarkan SCORE MAE, MAPE, dan jumlah data, rentang harga yang paling cocok adalah rentang 20,000 - 150,000 SAR. Rentang ini mencakup sebagian besar data dengan jumlah yang cukup besar untuk memberikan representasi yang baik terhadap variasi harga mobil bekas. Selain itu, rentang ini juga memberikan rentang harga yang cukup luas untuk mencakup berbagai jenis mobil bekas tanpa terlalu mempersempit fokus model
   
Dengan melakukan limitasi pada fitur-fitur dan label tersebut, model dapat difokuskan pada rentang-nilai yang relevan dan lebih akurat dalam memprediksi harga mobil bekas. Setiap langkah limitasi memiliki rentang nilai yang jelas dan dapat diinterpretasikan dengan mudah, sehingga membantu meningkatkan kegunaan model dalam praktiknya.

![image](https://github.com/Sukmagubali/Capstone-Project-Modul-3/assets/151388496/3d65eb90-e58f-41e3-bed9-5d218d417a5f)

### **Kesimpulan**
- Model Extreme Gradient Boost telah mengalami peningkatan yang signifikan dalam akurasi prediksi setelah dilakukan tuning. Terjadi penurunan yang signifikan pada Mean Absolute Error (MAE) dari 11,644.74 menjadi 11,337.55, serta pada Mean Absolute Percentage Error (MAPE) dari 0.2080 menjadi 0.2015. Hal ini menunjukkan bahwa model yang diatur ulang memberikan prediksi dengan tingkat kesalahan yang lebih rendah dan lebih konsisten. Perubahan yang paling signifikan terjadi pada Root Mean Squared Logarithmic Error (RMSLE), yang turun dari 0.2783 menjadi 0.0731 setelah tuning, menunjukkan kemampuan model dalam mengurangi kesalahan logaritmik prediksinya. Dalam rentang nilai yang telah dilatih, perkiraan harga rata-ratanya akan memiliki selisih sekitar 20.15% dari harga yang sebenarnya, seperti terlihat dari MAPE dan MAE.

- Fitur yang memiliki pengaruh paling signifikan pada model ini adalah Engine Size dan Year 

- Analisis performa model berdasarkan rentang harga menunjukkan bahwa performa model cenderung bervariasi tergantung pada rentang harga mobil bekas. Rentang harga tertentu mungkin memerlukan penyesuaian atau pemilihan model yang lebih sesuai untuk meningkatkan akurasi prediksi. Evaluasi terus-menerus diperlukan untuk memastikan konsistensi performa dan identifikasi potensi perbaikan lebih lanjut.

- Model ini kurang cocok untuk mobil dengan harga sangat rendah (<4k SAR) dan sangat tinggi (>150k SAR), seperti yang terlihat dari hasil tabel prediksi rentang harga. Hal ini menunjukkan bahwa model ini lebih baik digunakan untuk memprediksi harga mobil bekas dalam rentang harga yang lebih moderat.
### **Rekomendasi**
Rekomendasi Bisnis:

1. Fokuskan strategi penjualan pada mobil bekas dengan harga moderat, karena model ini kurang cocok untuk memprediksi harga mobil dengan harga sangat rendah (<4k SAR) dan sangat tinggi (>150k SAR). Ini dapat dilakukan dengan memperkuat promosi dan penjualan untuk mobil bekas dengan rentang harga yang sesuai dengan kemampuan model, yaitu dalam rentang harga yang lebih moderat.
2. Gunakan hasil analisis performa model berdasarkan rentang harga untuk menyesuaikan strategi penjualan dan promosi, serta untuk mengidentifikasi peluang pasar yang lebih potensial. Misalnya, jika model menunjukkan performa yang lebih baik pada mobil bekas dengan harga 100k-150k SAR, maka fokuskan upaya pemasaran pada rentang harga ini untuk meningkatkan konversi penjualan.
3. Tingkatkan layanan pelanggan dengan menyediakan informasi yang lebih rinci tentang proses pembelian, garansi, dan layanan purna jual. Hal ini dapat membantu meningkatkan kepercayaan pelanggan dan memperkuat hubungan jangka panjang dengan mereka.
4. Manfaatkan teknologi digital seperti aplikasi seluler atau platform online untuk memperluas jangkauan dan kenyamanan pelanggan. Ini juga dapat membantu dalam mengumpulkan data pelanggan yang lebih rinci untuk analisis lebih lanjut.

Rekomendasi Pengembangan Model:

1. Lanjutkan tuning model untuk meningkatkan akurasi prediksi, terutama pada rentang harga yang kurang sesuai dengan model saat ini. Misalnya, jika model kurang akurat dalam memprediksi harga mobil dengan harga sangat rendah atau sangat tinggi, maka lakukan tuning lebih lanjut untuk meningkatkan performa pada rentang harga ini.
2. Evaluasi kembali fitur-fitur yang memiliki pengaruh paling signifikan pada model, yaitu Engine Size dan Year, untuk memastikan bahwa mereka masih relevan dan memberikan kontribusi yang optimal terhadap prediksi harga mobil bekas. Jika diperlukan, tambahkan fitur-fitur baru yang dapat meningkatkan akurasi prediksi, seperti riwayat perawatan atau informasi kecelakaan.
3. Pertimbangkan untuk menambahkan fitur-fitur baru atau menghapus fitur yang kurang relevan untuk meningkatkan akurasi prediksi dan konsistensi performa model. Misalnya, jika fitur-fitur yang kurang relevan mengganggu performa model, maka pertimbangkan untuk menghapusnya atau menggantinya dengan fitur yang lebih relevan.
4. Pertimbangkan untuk menggunakan metode pemodelan yang lebih kompleks seperti ensemble learning atau neural networks jika diperlukan.




