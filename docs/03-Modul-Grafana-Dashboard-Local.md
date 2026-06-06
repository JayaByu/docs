# Modul Praktikum Grafana Dashboard dengan Data Source Lokal

## Tujuan Pembelajaran

Setelah mengikuti praktikum ini, peserta mampu:

- Membuat dashboard Grafana sederhana
- Menggunakan data source lokal bawaan Grafana
- Membuat panel chart, gauge, dan stat
- Menyimpan dashboard sebagai hasil praktikum
- Memahami alur pembuatan dashboard sebelum integrasi ke Prometheus

---

# Pengantar

Pada tahap ini Grafana sudah berhasil dijalankan menggunakan Docker Compose.

Setelah itu, peserta akan belajar membuat dashboard menggunakan **data source lokal** agar fokus pada konsep dashboard terlebih dahulu, tanpa harus bergantung pada server monitoring lain.

Untuk pembelajaran, data source lokal yang paling cocok adalah:

- **TestData DB**  
  Data source bawaan Grafana untuk simulasi data

Karena tentu saja hidup belum cukup bikin pusing, kita sengaja mulai dari data yang aman dulu.

---

# Prasyarat

- Grafana sudah berjalan menggunakan Docker Compose
- Akses ke dashboard Grafana tersedia
- Login ke Grafana berhasil
- Tidak ada firewall yang menghalangi port Grafana

---

# Praktikum 1 - Login ke Grafana

Buka browser:

```text
http://IP-SERVER:3000
```

Contoh:

```text
http://192.168.1.10:3000
```

Login default:

```text
Username: admin
Password: admin
```

Jika diminta, ubah password sesuai kebutuhan.

---

# Praktikum 2 - Mengaktifkan Data Source Lokal

## Masuk ke Menu Data Source

Pada sidebar Grafana:

```text
Connections
→ Add new connection
```

Cari:

```text
TestData DB
```

## Pilih TestData DB

Klik plugin **TestData DB** lalu pilih **Add data source**.

## Simpan Konfigurasi

Klik:

```text
Save & test
```

Jika berhasil, Grafana akan menampilkan status sukses.

---

# Praktikum 3 - Membuat Dashboard Baru

## Buat Dashboard

Pada sidebar:

```text
Dashboards
→ New
→ New dashboard
```

## Tambahkan Panel

Klik:

```text
Add visualization
```

Pilih data source:

```text
TestData DB
```

---

# Praktikum 4 - Membuat Panel Time Series

## Konfigurasi Panel

Gunakan mode data:

```text
CSV Metric Values
```

Contoh data:

```text
Time,Value
now-5m,20
now-4m,35
now-3m,30
now-2m,55
now-1m,48
now,60
```

## Judul Panel

```text
CPU Usage Simulation
```

## Simpan Panel

Klik:

```text
Apply
```

---

# Praktikum 5 - Membuat Panel Stat

## Tambahkan Panel Baru

Klik:

```text
Add visualization
```

Pilih:

```text
Stat
```

Gunakan data simulasi, misalnya:

```text
Disk Usage
```

Contoh nilai:

```text
72
```

Atur unit:

```text
percent (0-100)
```

---

# Praktikum 6 - Membuat Panel Gauge

## Tambahkan Panel Baru

Klik:

```text
Add visualization
```

Pilih:

```text
Gauge
```

Contoh pengaturan:

- Value: `65`
- Unit: `%`
- Min: `0`
- Max: `100`

Judul panel:

```text
Memory Usage
```

---

# Praktikum 7 - Menyusun Dashboard

Setelah beberapa panel dibuat, susun dashboard agar rapi.

Contoh panel yang dapat digunakan:

- CPU Usage Simulation
- Memory Usage
- Disk Usage
- Network Traffic Simulation

Peserta dapat mengatur:

- Posisi panel
- Ukuran panel
- Judul panel
- Tipe visualisasi

---

# Praktikum 8 - Menyimpan Dashboard

Klik tombol:

```text
Save dashboard
```

Isi nama dashboard, misalnya:

```text
Dashboard Monitoring Lokal
```

Simpan ke folder default atau folder praktikum jika tersedia.

---

# Praktikum 9 - Export Dashboard

Untuk dokumentasi praktikum, dashboard dapat diekspor ke JSON.

Langkah:

```text
Dashboard settings
→ JSON model
```

Atau:

```text
Share
→ Export
```

Hasil export dapat disimpan sebagai backup atau lampiran tugas.

---

# Hasil yang Diharapkan

Setelah praktikum ini, peserta dapat:

- Membuka Grafana
- Menambahkan data source lokal
- Membuat dashboard baru
- Menambahkan panel time series
- Menambahkan panel stat
- Menambahkan panel gauge
- Menyimpan dashboard hasil praktikum

---

# Latihan Mandiri

## Soal 1

Buat dashboard dengan nama:

```text
Dashboard Local Monitoring
```

## Soal 2

Tambahkan minimal 3 panel:

- CPU Usage
- Memory Usage
- Disk Usage

## Soal 3

Ubah salah satu panel menjadi:

- Stat
- Gauge
- Time series

## Soal 4

Simpan dashboard lalu export dalam format JSON.

---

# Kesimpulan

Pada praktikum ini peserta telah belajar dasar pembuatan dashboard Grafana menggunakan data source lokal bawaan Grafana.

Tahap ini penting sebelum lanjut ke integrasi data nyata seperti Prometheus dan Node Exporter, karena peserta jadi paham:

- cara membuat panel
- cara memilih visualisasi
- cara menyusun dashboard
- cara menyimpan hasil kerja

Dengan alur ini, pembelajaran jadi bertahap dan lebih mudah diikuti.
