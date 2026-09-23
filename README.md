<div align="center">

# 🏠 Ogenkz Homelab

*Dokumentasi dan catatan troubleshooting eksperimen IT Infrastructure & Homelab*

[![Status: Active](https://img.shields.io/badge/Status-Active-success.svg)](#)
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue.svg)](#)
[![Proxmox](https://img.shields.io/badge/Proxmox-VE-orange.svg)](#)

</div>

---

## 📖 Overview
Repositori ini adalah tempat saya mendokumentasikan perjalanan membangun, mengonfigurasi, dan merawat infrastruktur peladen (*server*) rumahan (Homelab). Tujuan utamanya adalah untuk bereksperimen dengan berbagai teknologi *Self-Hosted*, *Networking*, dan *Virtualization* sekaligus menjadi catatan pribadi ketika melakukan *troubleshooting*.

## 🗺️ Navigasi Dokumentasi

Biar gampang dicari, dokumentasi dibagi ke beberapa bagian:

- 🏗️ **[Arsitektur & Topologi Jaringan](docs/architecture.md)** — Diagram alur jaringan dan sistem.
- 🖥️ **[Spesifikasi Hardware](docs/hardware.md)** — Spesifikasi detail Router, Proxmox, dan Raspberry Pi.
- 🌐 **[Konfigurasi Network](docs/network.md)** — Alokasi IP Address, Port, dan pengaturan Mikrotik.
- 🐳 **[Layanan & Services (Docker / VM)](services/)** — Daftar lengkap layanan yang di-*self-host*.

## 🚀 Layanan Utama (Self-Hosted)

Berikut adalah beberapa core-services yang saat ini berjalan di atas Raspberry Pi (Docker) dan Proxmox:

| Layanan | Keterangan | Lokasi / Node |
| :--- | :--- | :--- |
| **[Pi-hole + Unbound](services/pihole/)** | DNS Resolver lokal dan pemblokir iklan tingkat jaringan. | Raspberry Pi |
| **[Nginx Proxy Manager](services/npm/)** | Reverse proxy untuk mengatur SSL dan routing trafik masuk. | Raspberry Pi |
| **[Homer](services/homer/)** | Halaman depan statis (*Dashboard*) untuk akses cepat layanan. | Raspberry Pi |
| **[Uptime Kuma](services/uptime-kuma/)** | Memantau *uptime* seluruh server dan layanan secara *real-time*. | Raspberry Pi |

## 🛠️ Stack Teknologi

- **Routing / Gateway:** Mikrotik RouterOS
- **Virtualisasi:** Proxmox VE (LXC & KVM)
- **Containerization:** Docker & Docker Compose
- **Sistem Operasi:** Debian / Ubuntu Linux

---
*Dikelola oleh [@ogenkz](https://github.com/ogenkz-tech)*
