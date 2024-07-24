****Forecasting Harga Komoditas di Indonesia****

Proyek ini bertujuan untuk memprediksi harga komoditas tertentu di Indonesia, khususnya beras dan minyak, menggunakan tiga model machine learning yang berbeda: Stacking Regressor, Linear Regressor, dan Random Forest Regressor. Dataset yang digunakan berasal dari Kaggle dan mencakup data harga makanan di Indonesia.

Model yang Digunakan

**1. Stacking Regressor**

Model ini menggabungkan dua atau lebih model dasar (base models) dan menggunakan model lain sebagai meta-learner untuk menggabungkan hasil prediksi dari model dasar. Pada proyek ini, Random Forest Regressor dan Linear Regression digunakan sebagai base models, sedangkan Linear Regression digunakan sebagai meta-learner.

**2. Linear Regressor**

Model ini menggunakan pendekatan regresi linear sederhana untuk memprediksi harga komoditas berdasarkan tanggal. Model ini memodelkan hubungan linear antara fitur input (tanggal) dan output (harga).

**3. Random Forest Regressor**

Model ini merupakan ensambel dari banyak pohon keputusan yang dilatih pada subset data yang berbeda dan fitur yang berbeda. Model ini dapat menangkap hubungan non-linear dalam data, membuatnya lebih fleksibel dibandingkan dengan regresi linear sederhana.

**Stacking Regressor**
Define the base models:

`rf = RandomForestRegressor(random_state=42)`

`lr = LinearRegression()`

Dua model dasar ditentukan di sini: Random Forest Regressor (rf) dan Linear Regression (lr).

**Define the stacking ensemble model:**

`estimators = [('rf', rf), ('lr', lr)]`

`stacking_regressor = StackingRegressor(estimators=estimators, final_estimator=LinearRegression())`

Model stacking ensemble didefinisikan dengan menggunakan dua model dasar (rf dan lr) dan menggunakan Linear Regression sebagai estimator final.

Train the stacking model:

`stacking_regressor.fit(X_train, y_train)`

Model stacking dilatih dengan data latih (X_train, y_train).

Make predictions:

`y_pred = stacking_regressor.predict(X_test)`

Prediksi dibuat menggunakan data uji (X_test).

Evaluate the model:

`mse = mean_squared_error(y_test, y_pred)`

`mae = mean_absolute_error(y_test, y_pred)`

Kinerja model dievaluasi menggunakan Mean Squared Error (MSE) dan Mean Absolute Error (MAE).

Linear Regressor

Train the linear regression model:

`lr = LinearRegression()`

`lr.fit(X_train, y_train)`

Model Linear Regression dilatih dengan data latih (X_train, y_train).

Make predictions:

`y_pred = lr.predict(X_test)`

Prediksi dibuat menggunakan data uji (X_test).

Evaluate the model:

`mse = mean_squared_error(y_test, y_pred)`

`mae = mean_absolute_error(y_test, y_pred)`

Kinerja model dievaluasi menggunakan Mean Squared Error (MSE) dan Mean Absolute Error (MAE).

Random Forest Regressor

Define parameter grid for GridSearchCV:

`param_grid = {
    'n_estimators': [100, 200],
    'max_depth': [None, 10, 20],
    'min_samples_split': [2, 5]
}`

Grid parameter didefinisikan untuk GridSearchCV.

Initialize Random Forest Regressor:

`rf = RandomForestRegressor(random_state=42)`

Model Random Forest Regressor diinisialisasi.

Perform Grid Search:

`grid_search = GridSearchCV(rf, param_grid, cv=3, scoring='neg_mean_squared_error')`

`grid_search.fit(X_train, y_train)`

Pencarian grid dilakukan untuk menemukan kombinasi parameter terbaik berdasarkan data latih (X_train, y_train).

Get the best model from grid search:

`best_model = grid_search.best_estimator_`

Model terbaik dari pencarian grid disimpan.

Make predictions:

`y_pred = best_model.predict(X_test)`

Prediksi dibuat menggunakan data uji (X_test) dengan model terbaik.

Evaluate the model:

`mse = mean_squared_error(y_test, y_pred)`

`mae = mean_absolute_error(y_test, y_pred)`

Kinerja model dievaluasi menggunakan Mean Squared Error (MSE) dan Mean Absolute Error (MAE).

Perbandingan Pengolahan Data

Stacking Regressor: Menggunakan dua model dasar (Random Forest dan Linear Regression) dan mengkombinasikannya dengan Linear Regression sebagai estimator final. Data dilatih pada model stacking ini, dan prediksi dibuat berdasarkan kombinasi kedua model dasar.

Linear Regressor: Menggunakan model Linear Regression tunggal untuk melatih data dan membuat prediksi. Ini adalah pendekatan sederhana tanpa kombinasi model lain.

Random Forest Regressor: Menggunakan Random Forest Regressor dengan optimasi parameter melalui GridSearchCV untuk menemukan kombinasi parameter terbaik. Pendekatan ini lebih kompleks dibandingkan dengan Linear Regressor sederhana.

Hasil Yang Di Dapatkan 

**Hasil Evaluasi Stacking Regressor:**

Mean Squared Error for Rice: 2117445.35

Mean Absolute Error for Rice: 1190.17

Mean Squared Error for Oil: 97570691.14

Mean Absolute Error for Oil: 8374.18

Hasil Prediksi:

Rice price forecast (per year):

Year 1: 11648.90

Year 2: 11623.49

Year 3: 11598.08

Year 4: 11572.67

Year 5: 11547.26

Oil price forecast (per year):

Year 1: 20715.48

Year 2: 20714.87

Year 3: 20714.26

Year 4: 20713.65

Year 5: 20713.04

**Hasil Evaluasi Linear Regressor:**

Mean Squared Error for Rice: 2116655.67

Mean Absolute Error for Rice: 1188.75

Mean Squared Error for Oil: 97402773.06

Mean Absolute Error for Oil: 8381.87

Hasil Prediksi:

Rice price forecast (per year):

Year 1: 11704.45

Year 2: 11714.26

Year 3: 11724.06

Year 4: 11733.87

Year 5: 11743.68

Oil price forecast (per year):

Year 1: 20332.70

Year 2: 20328.80

Year 3: 20324.91

Year 4: 20321.01

Year 5: 20317.12

**Hasil Evaluasi Random Forest Regressor:**

Mean Squared Error for Rice: 2123390.45

Mean Absolute Error for Rice: 1179.20

Mean Squared Error for Oil: 97688082.57

Mean Absolute Error for Oil: 8343.03

Hasil Prediksi:

Rice price forecast (per year):

Year 1: 11559.15

Year 2: 11559.15

Year 3: 11559.15

Year 4: 11559.15

Year 5: 11559.15

Oil price forecast (per year):

Year 1: 19875.06

Year 2: 19875.06

Year 3: 19875.06

Year 4: 19875.06

Year 5: 19875.06

Kesimpulan

**Stacking Regressor:**

Menggabungkan model Random Forest dan Linear Regression.

Memberikan hasil evaluasi yang cukup baik tetapi lebih rumit karena menggabungkan dua model dasar.

Prediksi untuk harga minyak lebih stabil dibandingkan dengan model lainnya.

**Linear Regressor:**

Sederhana dan mudah diimplementasikan.

Hasil evaluasi dan prediksi tidak jauh berbeda dengan model Stacking.

Memberikan prediksi harga yang meningkat secara bertahap setiap tahun.

**Random Forest Regressor:**

Menggunakan GridSearchCV untuk mendapatkan model terbaik.

Memberikan hasil evaluasi yang sedikit lebih buruk dibandingkan dengan dua model lainnya.

Prediksi harga cenderung tetap konstan sepanjang tahun.

Alvino Radyo Danisworo
A11.2022.14600
