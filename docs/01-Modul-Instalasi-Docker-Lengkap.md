# Modul Praktikum Instalasi Docker

## Pendahuluan
Docker adalah platform containerization yang memungkinkan aplikasi berjalan konsisten di berbagai lingkungan.

## Tujuan Pembelajaran
- Memahami Docker
- Install Docker Engine
- Install Docker Compose
- Menjalankan container
- Memahami image, volume, dan network

# Prasyarat

- Ubuntu 22.04 / 24.04
- RAM 2 GB
- Akses sudo

# Praktikum 1 - Instalasi Docker

## Update Repository

```bash
sudo apt update
sudo apt upgrade -y
```

## Install Dependency

```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

## Tambah GPG Key Docker

```bash
sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

## Tambah Repository Docker

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## Install Docker

```bash
sudo apt update

sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Verifikasi

```bash
docker --version
docker compose version
```

## Test

```bash
docker run hello-world
```

# Praktikum 2 - Docker Dasar

## Pull Image

```bash
docker pull nginx
```

## Menjalankan Container

```bash
docker run -d --name nginx -p 80:80 nginx
```

## Cek Container

```bash
docker ps
```

# Latihan
- Jalankan container Ubuntu
- Jalankan container Apache
- Hapus container dan image

# Kesimpulan

Peserta telah memahami instalasi dan penggunaan Docker dasar.
