# Nginx Proxy Manager (NPM)

## 📝 Deskripsi
NPM mempermudah pembuatan aturan *Reverse Proxy* beserta pengelolaan sertifikat SSL/TLS secara visual (lewat web GUI) tanpa harus menulis file konfigurasi Nginx secara manual.

## 🛠️ Konfigurasi Jaringan
- **Host IP**: `10.0.0.18`
- **Port HTTP/HTTPS**: `80`, `443`
- **Port Web GUI**: `81`
- **Image Docker**: `jc21/nginx-proxy-manager:latest`

**Alur Kerja**: Klien memanggil domain (contoh: `homer.ogenkz.local`). DNS (Pi-hole) mengarahkan domain tersebut ke `10.0.0.18`. NPM menerima permintaan di port 80/443, lalu meneruskannya ke kontainer aplikasi internal.
