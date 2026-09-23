# Arsitektur & Topologi Jaringan Homelab

Berdasarkan *mapping* terbaru dari DHCP Lease & ARP Table Mikrotik, jaringan homelab ini terbagi menjadi beberapa segmen fungsi (Infrastruktur, Virtualisasi, Container/SBC, Keamanan/CCTV, dan Perangkat Pengguna).

## 🗺️ Diagram Topologi Lengkap (Mermaid)

```mermaid
flowchart TD
    Internet((Internet)) <--> Modem[Modem ISP<br>192.168.1.1]
    Modem <--> Mikrotik

    subgraph Core_Network [Core Network & Gateway - 10.0.0.0/24]
        Mikrotik{Mikrotik Router<br>IP: 10.0.0.1<br>DHCP/Firewall}
        Ruijie[Ruijie AP<br>IP: 10.0.0.2<br>Access Point Utama]
        Extender[LAN Extender MW302R<br>IP: 10.0.0.8]
        
        Mikrotik --- Ruijie
        Mikrotik --- Extender
    end

    subgraph Servers_Virtualization [Server & Virtualisasi]
        Proxmox[Proxmox VE Server<br>IP: 10.0.0.17]
        
        subgraph Proxmox_VMs [Virtual Machines]
            n8n(n8n Automation<br>10.0.0.20)
            AdGuard(AdGuard DNS<br>10.0.0.33)
            AILokal(AI Lokal<br>10.0.0.34)
        end
        Proxmox --- Proxmox_VMs
    end

    subgraph SBC_Docker [SBC / Docker Nodes]
        RPi1[Raspberry Pi 1 - Network<br>IP: 10.0.0.18<br>Pihole, NPM, Homer]
        RPi2[Raspberry Pi 2 - Hermes<br>IP: 10.0.0.62<br>Seafile, Portainer, Buzz]
    end

    subgraph Security_Surveillance [CCTV & Keamanan]
        NVR[(NVR System<br>10.0.0.93)]
        CCTV1((CCTV Luar 1<br>10.0.0.95))
        CCTV2((CCTV Luar 2<br>10.0.0.96))
        CCTV3((CCTV Garasi<br>10.0.0.86))
        CCTV4((CCTV Teras<br>10.0.0.11))
        
        NVR --- CCTV1 & CCTV2 & CCTV3 & CCTV4
    end

    subgraph SmartHome_Devices [IoT & User Devices]
        SmartTV[Smart TVs<br>Samsung & Xiaomi]
        GoogleHome((Google Home<br>10.0.0.22))
        Printer(Printer Brother<br>10.0.0.40)
        Users([Laptops & Phones<br>MacBook, iPhone, Android])
    end

    Mikrotik -->|LAN/WLAN| Servers_Virtualization
    Mikrotik -->|LAN/WLAN| SBC_Docker
    Mikrotik -->|LAN/WLAN| Security_Surveillance
    Ruijie -->|WLAN| SmartHome_Devices
```

## 🖥️ Daftar Perangkat Jaringan (Network Inventory)

### 1. Perangkat Core & Network
| Perangkat | IP Address | MAC Address | Keterangan |
| :--- | :--- | :--- | :--- |
| **Mikrotik Router** | `10.0.0.1` | - | Gateway utama jaringan. |
| **Ruijie AP** | `10.0.0.2` | `10:82:3D:DB:9C:01` | Access Point penyebar Wi-Fi utama. |
| **LAN Extender** | `10.0.0.8` | `30:16:9D:A3:9B:B4` | Extender jaringan. |

### 2. Server & Node Komputasi
| Perangkat | IP Address | Keterangan |
| :--- | :--- | :--- |
| **Proxmox VE Server** | `10.0.0.17` | Server Virtualisasi Utama (Bare-metal). |
| **VM: n8n** | `10.0.0.20` | Sistem otomasi *workflow*. |
| **VM: AdGuard** | `10.0.0.33` | DNS *ad-blocker* alternatif. |
| **VM: AI Lokal** | `10.0.0.34` | Sistem AI yang berjalan lokal. |
| **Raspberry Pi 1** | `10.0.0.18` | Docker Engine (Pihole, NPM, Uptime Kuma). |
| **Raspberry Pi 2 (Hermes)** | `10.0.0.62` | Docker Engine (Seafile, Buzz, Portainer). |

### 3. Keamanan & CCTV (Surveillance)
| Perangkat | IP Address |
| :--- | :--- |
| **NVR System** | `10.0.0.93` |
| **CCTV Area Luar 1** | `10.0.0.95` |
| **CCTV Area Luar 2** | `10.0.0.96` |
| **CCTV Garasi** | `10.0.0.86` |
| **CCTV Teras Tamu** | `10.0.0.11` |

### 4. Smart Home & IoT
- **Google Home** (`10.0.0.22`)
- **Printer Brother** (`10.0.0.40`)
- **TV Samsung** (`10.0.0.5`)
- **Xiaomi TV** (`10.0.0.50`)

### 5. Klien / User
Terdiri dari berbagai gawai pribadi seperti *MacBook, iPhone, Android, Laptop Dell*, dan *Tablet* yang menggunakan alokasi IP dinamis dari DHCP server Mikrotik.
