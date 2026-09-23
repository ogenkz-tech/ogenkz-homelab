# Pi-hole + Unbound

## 📝 Deskripsi
Kombinasi Pi-hole dan Unbound digunakan sebagai DNS Server utama untuk jaringan homelab.
- **Pi-hole**: Menerima request DNS dari klien, memblokir domain iklan/tracker berdasarkan *blocklist*.
- **Unbound**: Bertindak sebagai *recursive DNS resolver*. Alih-alih meneruskan request ke DNS publik seperti Google (8.8.8.8) atau Cloudflare (1.1.1.1), Pi-hole akan meneruskan request ke Unbound lokal untuk mencari IP domain secara mandiri dari *root server*. Ini meningkatkan privasi jaringan.

## 🛠️ Konfigurasi Jaringan
- **Host IP**: `10.0.0.18`
- **DNS Port**: `53` (TCP/UDP)
- **Web Interface Port**: `8080` (Akses via NPM atau langsung)
- **Image Docker**: `pihole/pihole:latest` & `mvance/unbound-rpi:latest`
