# UTS_DataMining_2304020127
Langkah-Langkah
A. PERSIAPAN DATA
1. Import Data
2. Load Data
3. Cek Struktur Data

B. PEMBERSIHAN DATA
1. Cek Missing Value
2. Exploratory Data Analysis (EDA)
a. Distribusi Target
b. Korelasi Fitur
3. Preprocessing
a. Pemisahan fitur dan target
Langkah ini merupakan tahap Data Validation Strategy dengan membagi data menjadi training set dan validation set. Parameter `test_size=0.2` mengalokasikan 20% data untuk validasi, `random_state=42` memastikan hasil konsisten, dan `stratify=y` menjaga proporsi kelas tetap seimbang. Hal ini penting agar model dilatih dan divalidasi pada distribusi data yang adil serta menghindari bias akibat ketidakseimbangan kelas.
b. Split data
Langkah ini merupakan tahap Data Validation Strategy dengan membagi data menjadi training set dan validation set. Parameter `test_size=0.2` mengalokasikan 20% data untuk validasi, `random_state=42` memastikan hasil konsisten, dan `stratify=y` menjaga proporsi kelas tetap seimbang. Hal ini penting agar model dilatih dan divalidasi pada distribusi data yang adil serta menghindari bias akibat ketidakseimbangan kelas.
c. Feature scaling
Langkah ini merupakan tahap **Feature Scaling** menggunakan **StandardScaler** untuk menyamakan skala fitur agar memiliki mean 0 dan standar deviasi 1. Hal ini penting agar fitur dengan nilai besar tidak mendominasi, terutama pada algoritma seperti KNN dan Regresi Logistik. Proses dilakukan dengan `fit_transform` pada **X_train** dan `transform` pada **X_val** untuk mencegah *data leakage* sehingga evaluasi model tetap objektif.
d. Data testing
Langkah ini merupakan tahap Final Data Preparation untuk memastikan data testing memiliki struktur dan skala yang sama dengan data pelatihan. Kolom `Id` dihapus agar konsisten, kemudian dilakukan `scaler.transform` menggunakan parameter dari data latih untuk menjaga objektivitas dan mencegah *data leakage*. Selain itu, `test_ids` disimpan untuk menghubungkan hasil prediksi dengan data asli. Tahap ini memastikan hasil prediksi valid dan bebas dari kesalahan teknis.

C. PEMBUATAN MODEL
1. Model Desicion Tree
Tahap ini merupakan proses Model Implementation and Validation menggunakan Decision Tree dengan `max_depth=10` untuk membatasi kompleksitas dan `random_state=42` agar hasil konsisten. Model dilatih dengan `.fit()` lalu diuji pada data validasi. Hasil akurasi sebesar 56,39% menunjukkan performa yang masih moderat, kemungkinan dipengaruhi oleh kompleksitas data dan ketidakseimbangan kelas, sehingga dapat dijadikan baseline untuk dibandingkan dengan model yang lebih kuat seperti Random Forest.
2. Model Random Forest
Tahap ini merupakan proses pelatihan dan evaluasi model Random Forest dengan 200 pohon keputusan (`n_estimators=200`) untuk meningkatkan stabilitas dan akurasi prediksi. Parameter `max_depth=15` digunakan agar model mampu menangkap pola yang lebih kompleks. Model dilatih menggunakan data yang sudah diskalakan, kemudian diuji pada data validasi. Hasil akurasi 57,55% menunjukkan peningkatan dibanding model sebelumnya karena Random Forest lebih baik dalam menangani hubungan non-linear dan mengurangi varians, meskipun performa masih dipengaruhi oleh ketidakseimbangan kelas pada dataset.
3. Model Logistic Regression
Tahap ini merupakan **Model Comparison** yang membandingkan performa beberapa algoritma dalam bentuk tabel dan grafik batang untuk menentukan model terbaik. Hasilnya menunjukkan **Logistic Regression** memiliki akurasi tertinggi (61,05%), diikuti **Random Forest** (57,56%) dan **Decision Tree** (56,40%). Dari perbandingan ini dapat disimpulkan bahwa model linear lebih efektif untuk dataset ini, sehingga Logistic Regression menjadi pilihan utama untuk tahap prediksi akhir.
4. Model K-Nearest Neighbors (KNN)
Tahap ini merupakan proses implementasi algoritma K-Nearest Neighbors (KNN)** dengan `n_neighbors=5`, yang menentukan label berdasarkan kedekatan jarak antar data. Model dilatih menggunakan data yang telah melalui *feature scaling* agar perhitungan jarak lebih adil. Hasil akurasi sebesar **48,25%** menunjukkan performa terendah dibanding model lain, mengindikasikan bahwa data cenderung saling tumpang tindih atau terlalu kompleks untuk dipisahkan hanya berdasarkan jarak, sehingga KNN kurang efektif pada dataset ini.
5. Perbandingan Keempat Model
Tahap ini merupakan fase **Model Comparison and Selection**, di mana performa seluruh model dirangkum dan divisualisasikan untuk menentukan yang terbaik. Hasilnya menunjukkan **Logistic Regression** memiliki akurasi tertinggi (**61,04%**), diikuti Random Forest (**57,55%**), Decision Tree (**56,39%**), dan KNN (**48,25%**). Hal ini menunjukkan bahwa pola data lebih sesuai dengan pendekatan linear, sehingga Logistic Regression dipilih sebagai model final. Namun, akurasi yang masih di kisaran 60% mengindikasikan adanya pengaruh ketidakseimbangan kelas terhadap performa model.
6. Evaluasi Model Terbaik (Logistic Regression)

7. Cross Validation

8. Hyperparameter Tuning

D. PREDIKSI DATA UJI
1. Prediksi Data Testing
2. Menyimpan CSV
3. Mendownload CSV
4. Verifikasi

E. KESIMPULAN
Berdasarkan hasil analisis, dapat disimpulkan bahwa Logistic Regression merupakan model terbaik untuk mengklasifikasikan kualitas anggur dibandingkan Decision Tree, Random Forest, dan KNN, dengan akurasi tertinggi sebesar **61,05%**, yang menunjukkan bahwa pola dalam data cenderung linear sehingga lebih sesuai dimodelkan menggunakan pendekatan linear. Meskipun model menunjukkan performa yang cukup baik dan stabil dalam memprediksi data, masih terdapat potensi bias terutama pada kelas kualitas menengah yang disebabkan oleh ketidakseimbangan distribusi kelas dalam dataset, sementara fitur kimia seperti kadar alkohol dan tingkat keasaman diduga memiliki pengaruh yang signifikan terhadap hasil prediksi. Secara keseluruhan, proses preprocessing, pemodelan, serta evaluasi yang dilakukan secara sistematis telah menghasilkan model yang cukup andal dan dapat digunakan sebagai dasar untuk analisis lebih lanjut, meskipun masih terdapat ruang untuk peningkatan performa melalui optimasi model dan penyeimbangan data.
