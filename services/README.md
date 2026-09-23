# 🐳 Docker Ecosystem & Services

Raspberry Pi (Node: `10.0.0.18`) didedikasikan secara penuh untuk menjalankan ekosistem Docker. Berikut adalah topologi mendetail dari kontainer yang saling terhubung.

## 🕸️ Arsitektur Kontainer Docker

```mermaid
flowchart TD
    Client((Klien Lokal / Jaringan))

    subgraph RaspberryPi [Raspberry Pi 8GB - Docker Host: 10.0.0.18]
        
        subgraph DNS_Layer [DNS & Ad-Blocking]
            Pihole[Pi-hole<br>Port: 53, 8080]
            Unbound[Unbound<br>Recursive DNS]
            Pihole -->|Upstream| Unbound
        end
        
        subgraph Proxy_Layer [Reverse Proxy]
            NPM[Nginx Proxy Manager<br>Port: 80, 443, 81]
        end

        subgraph App_Layer [Aplikasi & Layanan]
            Homer[Homer Dashboard<br>Port: 8081]
            Uptime[Uptime Kuma<br>Monitoring]
            CLI[CLI Proxy API<br>Port: 8317, 51121]
        end

        NPM -->|Route HTTP/S| Homer
        NPM -->|Route HTTP/S| Uptime
        NPM -->|Route API| CLI
    end

    Client -->|DNS Query| Pihole
    Client -->|Web Traffic| NPM
```

Layanan-layanan di atas diletakkan pada bridge network Docker (termasuk `172.17.0.x`, `172.18.0.x`, dan `172.19.0.x`). NPM bertugas memetakan port internal ke domain agar mudah diakses.
