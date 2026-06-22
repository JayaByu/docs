# Instalasi Docker Offline Oracle Linux 9.7 (Static Binary)
# Catatan

Lokasi instalasi:

```text
/opt/docker
```

Lokasi service:

```text
/etc/systemd/system/docker.service
```

Lokasi Docker Compose:

```text
/opt/docker/docker-compose
```
---

# 1. Persiapan File Docker

Copy file Docker static binary ke server:

```bash
docker-29.6.0.tgz
```

Extract file:

```bash
tar -xzf docker-29.6.0.tgz
```

Pindahkan hasil extract ke direktori target:

```bash
mv docker /opt/docker
```

---

# 2. Konfigurasi PATH

Tambahkan Docker ke environment:

```bash
echo 'export PATH=$PATH:/opt/docker' >> ~/.bashrc
source ~/.bashrc
```

Verifikasi:

```bash
docker --version
```

Output:

```text
Docker version 29.6.0
```

---

# 3. Pembuatan Service Docker

Buat file:

```bash
vi /etc/systemd/system/docker.service
```

Isi file:

```ini
[Unit]
Description=Docker Engine
After=network.target

[Service]
Environment="PATH=/opt/docker:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
ExecStart=/opt/docker/dockerd --userland-proxy=false
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Reload systemd:

```bash
systemctl daemon-reload
```

Enable service:

```bash
systemctl enable docker.service
```

---

# 4. Troubleshooting Docker Service

Start service:

```bash
systemctl start docker.service
```

Cek status:

```bash
systemctl status docker -l
```

Apabila gagal, cek log:

```bash
journalctl -u docker.service -n 100 --no-pager
```

---

# 5. Verifikasi Dependency (Opsional)

Cek binary yang dibutuhkan:

```bash
which containerd
which iptables
which nft
```

Verifikasi iptables:

```bash
ls -l /usr/sbin/iptables
```

Verifikasi nftables:

```bash
which nft
```

---

# 6. Test Docker Daemon Manual

Menjalankan daemon secara foreground:

```bash
/opt/docker/dockerd --userland-proxy=false
```

Pastikan muncul:

```text
API listen on /var/run/docker.sock
Daemon has completed initialization
```

---

# 7. Verifikasi Docker Running

Cek socket:

```bash
ls -l /var/run/docker.sock
```

Cek service:

```bash
systemctl is-active docker
```

Output:

```text
active
```

Cek detail service:

```bash
systemctl show docker -p MainPID -p ActiveState -p SubState
```

---

# 8. Verifikasi Docker Engine

Cek versi:

```bash
docker version
```

Cek informasi:

```bash
docker info
```

Cek container:

```bash
docker ps
```

---

## 9. Instalasi Docker Compose Plugin (Offline)

Download binary Docker Compose dari server yang memiliki internet:

```bash
docker-compose-linux-x86_64
```

Copy ke server Oracle Linux:

```bash
scp docker-compose-linux-x86_64 root@server:/opt/docker/docker-compose
```

Berikan permission executable:

```bash
chmod +x /opt/docker/docker-compose
```

Verifikasi binary:

```bash
/opt/docker/docker-compose version
```

Output:

```text
Docker Compose version v2.x.x
```

---

## 10. Registrasi Docker Compose Sebagai Plugin

Buat direktori plugin Docker:

```bash
mkdir -p /usr/local/lib/docker/cli-plugins
```

Buat symbolic link:

```bash
ln -sf /opt/docker/docker-compose \
/usr/local/lib/docker/cli-plugins/docker-compose
```

Verifikasi:

```bash
ls -l /usr/local/lib/docker/cli-plugins/
```

Output:

```text
docker-compose -> /opt/docker/docker-compose
```

---

## 11. Verifikasi Docker Compose Plugin

Cek plugin:

```bash
docker compose version
```

Output:

```text
Docker Compose version v2.x.x
```

Cek plugin yang terdeteksi Docker:

```bash
docker info
```

Pastikan terdapat informasi Compose pada bagian:

```text
Plugins:
 compose
```

---

## 12. Menjalankan Docker Compose

Menjalankan container:

```bash
docker compose up -d
```

Melihat status:

```bash
docker compose ps
```

Melihat log:

```bash
docker compose logs -f
```

Stop container:

```bash
docker compose down
```
---
