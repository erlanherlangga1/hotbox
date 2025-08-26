# Metode Deteksi Bearing Berdasarkan Data Sensor Suhu

## Deskripsi Umum
Kode ini digunakan untuk memetakan posisi **bearing**  pada kereta berdasarkan data suhu sensor (misalnya sensor BL) yang tersimpan dalam file CSV.  
Proses ini melibatkan:
- Deteksi awal dan akhir kereta
- Perhitungan kecepatan berdasarkan panjang kereta
- Konversi jarak ke indeks sampel
- Visualisasi dengan menandai posisi bearing dan axle pada grafik suhu

---

## Struktur Fungsi

### 1. `meter_ke_index(x_m, start_idx, sampling_interval, v_mps)`
Mengubah jarak (meter) dari kepala kereta menjadi index sampel.  
- **Input**:
  - `x_m`: Jarak dari kepala kereta (meter)  
  - `start_idx`: Index awal kereta  
  - `sampling_interval`: Interval sampling (detik)  
  - `v_mps`: Kecepatan kereta (m/s)  
- **Output**: Index sampel sesuai jarak `x_m`.

### 2. `index_ke_meter(idx, start_idx, sampling_interval, v_mps)`
Mengubah index sampel menjadi jarak (meter).  
- **Input**:
  - `idx`: Index sampel  
  - `start_idx`: Index awal kereta  
  - `sampling_interval`: Interval sampling (detik)  
  - `v_mps`: Kecepatan kereta (m/s)  
- **Output**: Jarak (meter).

### 3. `plot_bearing_mapping(csv_file, panjang_gerbong, jarak_bogie, jarak_axle)`
Fungsi utama untuk membaca data CSV, mendeteksi kereta, menghitung kecepatan, dan memetakan posisi bearing/axle pada grafik.  
- **Input**:
  - `csv_file`: Path file CSV  
  - `sensor_col`: Kolom sensor pada raw data csv (string)  
- **Output**: Grafik suhu dengan penanda posisi kereta dan bearing

---

## Bagian Penting `plot_bearing_mapping`
1. Deteksi awal kereta (`start_kereta`) saat suhu > rata-rata - 5.  
2. Hitung interval sampling dari timestamp.  
3. Deteksi akhir kereta (`stop_kereta`) saat suhu turun di bawah rata-rata.  
4. Hitung kecepatan kereta = panjang kereta ÷ durasi lewat.  
5. Plot grafik suhu dengan penanda start/stop, bearing, axle.  
6. Fungsi tambahan `axle_positions_from_gerbong` menghitung posisi axle tiap gerbong.  

---

## Cara Penggunaan
1. Siapkan file CSV berisi data suhu sensor.  
2. Tentukan parameter `csv_file` dan `sensor_col`.  
3. Jalankan fungsi:  

```python
csv_file = "data/log000_241105060417.csv"
plot_bearing_mapping(csv_file, sensor_col="BL")
