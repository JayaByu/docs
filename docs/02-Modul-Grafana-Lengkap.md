# Modul Praktikum Instalasi Grafana Menggunakan Docker

## Apa itu Grafana?

Grafana adalah platform visualisasi data dan monitoring yang digunakan untuk menampilkan metrik, log, dan data time-series dalam bentuk dashboard yang mudah dipahami.

Contoh penggunaan:

- Monitoring Server Linux
- Monitoring CPU, RAM, Disk
- Monitoring Database
- Monitoring Network
- Monitoring Kubernetes
- Monitoring IoT

---

# Arsitektur Sederhana

```text
+------------+
| Linux Host |
+------------+
      |
      v
+-------------+
|   Docker    |
+-------------+
      |
      v
+-------------+
|   Grafana   |
| Port 3000   |
+-------------+
      |
      v
Browser User
```

# Prasyarat

- Docker sudah terinstall
- Docker Compose tersedia

# Praktikum 1 - Menjalankan Grafana

## Pull Image Grafana

```bash
docker pull grafana/grafana:latest
```

## Membuat Volume

```bash
docker volume create grafana-storage
```

## Menjalankan Container Grafana

```bash
docker run -d \
--name grafana \
-p 3000:3000 \
-v grafana-storage:/var/lib/grafana \
--restart unless-stopped \
grafana/grafana:latest
```

## Verifikasi

```bash
docker ps
```

# Praktikum 2 - Akses Grafana

URL:

```text
http://IP-SERVER:3000
```

Login:

```text
Username : admin
Password : admin
```

# Praktikum 3 - Docker Compose

```yaml
services:
  grafana:
    image: grafana/grafana:latest
    container_name: grafana

    ports:
      - "3000:3000"

    volumes:
      - grafana-storage:/var/lib/grafana

    restart: unless-stopped

volumes:
  grafana-storage:
```

Jalankan:

```bash
docker compose up -d
```

# Praktikum 4 - Integrasi Prometheus dan Node Exporter

## docker-compose.yml

```yaml
services:

  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"

  node-exporter:
    image: prom/node-exporter
    ports:
      - "9100:9100"

  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
```

## Dashboard ID

```text
1860
```

# Hasil

- CPU Usage
- Memory Usage
- Disk Usage
- Network Traffic
- Load Average
- Uptime

# Kesimpulan

Peserta berhasil melakukan deploy Grafana menggunakan Docker dan menghubungkannya dengan Prometheus.
