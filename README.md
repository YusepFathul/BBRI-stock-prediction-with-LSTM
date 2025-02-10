# Proyek Deep Learning - Yusep Fathul Anwar

## Domain Proyek
Dalam dunia investasi dan perdagangan saham, prediksi harga saham menjadi aspek penting untuk pengambilan keputusan. Model prediksi berbasis deep learning, seperti Long Short-Term Memory (LSTM), telah banyak digunakan karena kemampuannya dalam menangani data deret waktu. Proyek ini bertujuan untuk memprediksi harga saham **Unilever Indonesia (UNVR.JK)** menggunakan model LSTM.

### Mengapa Masalah Ini Perlu Diselesaikan?
- Prediksi harga saham dapat membantu investor dalam mengambil keputusan yang lebih baik.
- LSTM mampu menangani data sekuensial dengan dependensi jangka panjang yang berguna dalam analisis keuangan.

### Referensi
- Hochreiter, S., & Schmidhuber, J. (1997). Long short-term memory. Neural computation.
- Brownlee, J. (2018). Deep Learning for Time Series Forecasting. Machine Learning Mastery.

---

## Business Understanding

### Problem Statements
1. Bagaimana model deep learning seperti LSTM dapat digunakan untuk memprediksi harga saham Unilever Indonesia?
2. Seberapa baik kinerja model dalam memprediksi harga saham berdasarkan metrik evaluasi?

### Goals
1. Membangun model LSTM untuk memprediksi harga saham.
2. Mengevaluasi performa model menggunakan metrik MAE, RMSE, dan MAPE.

### Solution Statement
- Menggunakan model LSTM dengan arsitektur dua lapisan untuk menangkap pola dalam data harga saham.
- Melakukan normalisasi data menggunakan **MinMaxScaler**.
- Memanfaatkan teknik **Early Stopping** untuk mencegah overfitting.

---

## Data Understanding

Dataset yang digunakan diperoleh dari **Yahoo Finance** menggunakan library `yfinance`.  
Data mencakup harga saham harian **Unilever Indonesia (UNVR.JK)** dari tahun 2005 hingga 2025.

<p align="center">
  <img src="https://github.com/user-attachments/assets/0f2315ee-9759-44a8-a669-47004fd99169" width="600">
  <img src="https://github.com/user-attachments/assets/8fdca856-3edc-4ede-a0dd-683be4fbbbb7" width="600">
</p>

### Variabel dalam Dataset:
- **`Open`** : Harga pembukaan saham.
- **`High`** : Harga tertinggi saham pada hari tersebut.
- **`Low`** : Harga terendah saham pada hari tersebut.
- **`Close`** : Harga penutupan saham.
- **`Volume`** : Jumlah saham yang diperdagangkan.

Visualisasi awal dilakukan untuk melihat **tren harga saham** dalam periode yang dipilih.
<p align="center">
  <img src="https://github.com/user-attachments/assets/fd000e44-a608-4e08-b556-f7c53d6430bd" width="800">
</p>

---

## Data Preparation

Langkah-langkah data preprocessing:
1. **Normalisasi Data**: Harga saham `Close` dinormalisasi menggunakan **MinMaxScaler**.
2. **Split Data**:
   - 80% data digunakan untuk pelatihan (training set).
   - 20% data digunakan untuk pengujian (test set).
3. **Membentuk Data Sequences**:
   - Menggunakan pendekatan **sliding window** untuk membuat input `X` dan target `y`.
   - `look_back = 1`, artinya model akan menggunakan harga saham sebelumnya untuk memprediksi harga berikutnya.
<p align="center">
  <img src="https://github.com/user-attachments/assets/b29bb0b0-2175-422c-a9c9-301106279760" width="600">
  <img src="https://github.com/user-attachments/assets/872d89e0-a08a-4add-8cff-51f06b18c5c0" width = "600">
</p>


---

## Modeling

Model yang digunakan adalah **LSTM berbasis TensorFlow/Keras** dengan arsitektur sebagai berikut:
1. **LSTM Layer (128 units, return_sequences=True)** → Menangkap pola dalam data deret waktu.
2. **Dropout (0.2)** → Mencegah overfitting.
3. **LSTM Layer (64 units)** → Mengurangi dimensi fitur yang diekstraksi.
4. **Dropout (0.2)** → Lapisan regulasi tambahan.
5. **Dense Layer (32 neurons, ReLU activation)** → Mengolah fitur yang diekstraksi dari LSTM.
6. **Output Layer (1 neuron)** → Memproduksi nilai prediksi harga saham.

Model dikompilasi dengan:
- Optimizer: `Adam (learning_rate=0.0001)`
- Loss function: `Huber Loss`
- Metrik evaluasi: `Mean Absolute Error (MAE)`

Model dilatih selama **200 epoch** dengan **batch_size=32** dan menggunakan **Early Stopping** dengan `patience=10`.
<p align="center">
  <img src="https://github.com/user-attachments/assets/d96ced44-c4ab-43f6-a36d-f779022eb9d9" width="600" style="margin-bottom: 20px;">
  <br>
  <img src="https://github.com/user-attachments/assets/3d0eb094-e9a2-40f2-9976-eda00a627dc7" width="600">
  <br>
  <img src="https://github.com/user-attachments/assets/e0b9ab97-d24a-4df9-a56b-384db595d1fd" width="600">
</p>

---

## Evaluation

Metrik evaluasi yang digunakan:
- **Mean Absolute Error (MAE)** → Rata-rata kesalahan absolut antara nilai aktual dan prediksi.
- **Root Mean Squared Error (RMSE)** → Menghitung deviasi antara nilai aktual dan prediksi.
- **Mean Absolute Percentage Error (MAPE)** → Persentase rata-rata kesalahan relatif terhadap nilai aktual.

Hasil evaluasi model pada data uji:
```plaintext
MAE: 0.01369470420225656
RMSE: 0.016755807441956847
MAPE: 0.03321364355690878
```

Grafik hasil prediksi menunjukkan perbandingan antara nilai aktual dan nilai prediksi, menggambarkan bagaimana model menangkap tren harga saham.
<p align="center">
  <img src="https://github.com/user-attachments/assets/0e4c7d1b-6fe3-4e6a-8e2d-729b15a664ec" width="800" style="margin-bottom: 20px;">
</p>

---

## Kesimpulan
- Model **LSTM** berhasil digunakan untuk memprediksi harga saham Unilever Indonesia.
- Performa model dapat ditingkatkan lebih lanjut dengan **tuning hyperparameter** atau menggunakan **lag lebih panjang**.
- Bisa juga dipertimbangkan pendekatan **ensemble learning** atau model hybrid dengan ARIMA/LSTM.

---

## Referensi
- Hochreiter, S., & Schmidhuber, J. (1997). Long short-term memory. Neural computation.
- Brownlee, J. (2018). Deep Learning for Time Series Forecasting. Machine Learning Mastery.

---
