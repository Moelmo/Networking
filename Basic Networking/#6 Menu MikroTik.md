# Mengenal Menu MikroTik RouterOS
---
## Gambaran Besar RouterOS
Secara sederhana, RouterOS dapat dipahami seperti ini:
```
┌─────────────────────────────────────┐
│           MikroTik RouterOS         │
├─────────────────────────────────────┤
│ Interfaces → Port & Interface       │
│ Bridge     → Layer 2                │
│ IP         → Layanan IP             │
│ Routing    → Jalur Paket            │
│ PPP        → PPP & VPN              │
│ Wireless   → WiFi                   │
│ Queue      → Bandwidth              │
│ Firewall   → Security               │
│ System     → Sistem Router          │
│ Tools      → Monitoring & Utility   │
└─────────────────────────────────────┘
```
## 1. Interfaces
### Fungsi 
Menu Interfaces digunakan untuk melihat dan mengatur seluruh interface jaringan pada router.

Contoh:
```
ether1
ether2
ether3
wlan1
bridge1
vlan10
```
Contoh topologi:
```
Internet -- ether1 -- MikroTik -- ether2 -- LAN
```
### Informasi yang Dapat Dilihat
- Nama interface.
- Status running.
- MAC Address.
- MTU.
- RX Traffic.
- TX Traffic.
- Link status.
- Speed.
- Duplex.

Contoh status:
```
R = Running
X = Disabled
```
### Fitur Penting
```
Interfaces
├── Ethernet
├── VLAN
├── Bonding
├── Bridge
├── Loopback
├── GRE
├── EoIP
└── WireGuard
```
Contoh CLI
```
/interface print
```
Melihat detail:
```
/interface ethernet print
```

## 2. Bridge
### Fungsi 
Menu Bridge digunakan untuk menggabungkan beberapa interface ke dalam satu jaringan Layer 2.

Contoh:
```
ether2 ─┐
        │
ether3 ─┼── bridge1
        │
ether4 ─┘
```
Ketiganya dapat berada dalam satu broadcast domain.

Struktur Bridge
```
Bridge
├── Bridge
├── Ports
├── VLANs
├── Hosts
├── Filters
└── Settings
```

### Contoh
Membuat bridge:
```
/interface bridge add name=bridge-lan
```
Menambahkan port:
```
/interface bridge port add bridge=bridge-lan interface=ether2

/interface bridge port add bridge=bridge-lan interface=ether3
```
Hasil:
```
ether2 ─┐
        ├── bridge-lan
ether3 ─┘
```

### Bridge Digunakan Untuk
- Menggabungkan port LAN.
- Membuat jaringan Layer 2.
- VLAN Filtering.
- STP/RSTP.
- Swtiching berbasis software.

## 3. IP
Menu IP adalah salah satu menu paling penting di RouterOS, Disinilah banyak fungsi jaringan utama berada.

```
IP
├── Addresses
├── DHCP Client
├── DHCP Server
├── DNS
├── Firewall
├── Hotspot
├── Neighbors
├── Pool
├── Routes
├── Services
└── ARP
```
### A. IP Address
Digunakan untuk memberikan IP Address pada interface.
```
/ip address add address=192.168.10.1/24 interface=ether2
```
Contoh:
```
ether2 --> 192.168.10.1/24
```

### B. DHCP Client
Router mendapatkan IP secara otomatis dari perangkat lain.
```
ISP
 │
 │ DHCP
 │
MikroTik
```
Contoh:
```
/ip dhcp-client add interface=ether1
```

### C. DHCP Server
Router memberikan IP kepada client.
```
MikroTik
    │
    ├── PC1 → 192.168.10.10
    ├── PC2 → 192.168.10.11
    └── PC3 → 192.168.10.12
```

### D. DNS
Mengatur DNS resolver pada router.

Contoh:
```
/ip dns print
```
Router dapat digunakan sebagai DNS cache untuk client.

### E. ARP
Melihat hubungan IP Address dengan MAC Address
```
/ip arp print
```
Contoh:
```
IP Address       MAC Address
192.168.10.10    AA:BB:CC:11:22:33
```

### F. Services
Mengatur layanan akses router.
 
Contoh:
```
WinBox
SSH
HTTP
HTTPS
Telnet
FTP
```
Sangat penting untuk keamanan.

## 4. Routing
### Fungsi
Menu Routing digunakan untuk mengatur bagaimana paket berpindah dari satu jaringan ke jaringan lain.

Contoh:
```
Network A
192.168.1.0/24
       │
       ▼
    Router
       │
       ▼
Network B
192.168.2.0/24
```

### Konsep Utama
Router menggunakan Routing Table.

Contoh:
```
Destination       Gateway
0.0.0.0/0         192.168.1.254
192.168.2.0/24    10.0.0.2
```

### Routing Dapat Mencakup
- Connected Route.
- Static Route.
- Default Route.
- Policy Routing.
- Dynamic Routing.

Contoh static route:
```
/ip route add dst-address=192.168.20.0/24 gateway=192.168.10.2
```

### Protokol Routing
RouterOS mendukung berbagai protokol seperti:
- RIP
- OSPF
- BGP
- IS-IS

Untuk tahap awal, fokus pada:
```
Connected Route
Static Route
Default Route
```

## 5. PPP
### Fungsi
Menu PPP digunakan untuk protokol Point-to-Point dan berbagai layanan VPN.

Contoh:
```
PPP
├── Interfaces
├── Profiles
├── Secrets
├── Active Connections
└── AAA
```

### Digunakan Untuk

- PPPoE
- PPTP
- L2LP
- SSTP
- PPP
- VPN tertentu

Contoh:
```
Client
   │
   │ PPP / VPN
   │
MikroTik
```
### PPP Secrets
Digunakan untuk membuat akun PPP atau VPN.

Contoh konsep:
```
Username: user1
Password: password
Service: l2tp
```

### PPP Profil
Mengatur parameter koneksi PPP seperti:
- Local Address
- Remote Address
- DNS
- Rate Limit
- Encryption

## Wireless
> Catatan: tampilan dan fitur Wireless dapat berbeda tergantung perangkat, versi RouterOS, dan paket wireless yang digutnakan.

### Fungsi
Menu Wireless digunakan untuk mengatur koneksi WIFI.

Contoh:
```
MikroTik AP
    )))))
      )))))
        )))))
       PC / HP
```

### Konfigurasi Penting
- Mode
- SSID
- Band
- Frequency
- Channel

### Mode Wireless
Contoh:
```
AP Bridge
Station
Station Bridge
Station Pseudobridge
```

Konsep sederhana:
```
AP
 │
 │ Wireless
 │
Station
```

### Contoh Pengaturan
```
SSID      : LAB-MIKROTIK
Band      : 2GHz / 5GHz
Frequency : Auto / Manual
Security  : WPA2 / WPA3
```

## 7. Queue
### Fungsi
Menu Queue digunakan untuk mengatur bandwidth.

Contoh:
```
Internet 100 Mbps
       │
     Router
    ┌──┴──┐
 PC1    PC2
10 Mbps 5 Mbps
```

### Queue Digunakan Untuk
- Membatasi bandwidth.
- Membagi bandwitdh.
- Prioritas trafik.
- QoS.
- Mengatur upload/download.

### Simple Queue
Contoh:
```
Target: 192.168.10.10
Max Limit: 10M/5M
```
Artinya client dapat dibatasi sesuai konfigurasi upload dan download.

### Queue Tree
Digunakan untuk pengaturan bandwidth yang lebih kompleks.

Biasanya digunakan bersama:
- Mangle
- Packet Mark
- Connection Mark

## 8. Firewall

### Fungsi
Firewall digunakan untuk mengontrol trafik jaringan.

Konsep:
```
Internet
   │
   ▼
┌─────────┐
│Firewall │
└─────────┘
   │
   ▼
LAN
```

### Bagian Utama FIrewall
```
IP
└── Firewall
    ├── Filter Rules
    ├── NAT
    ├── Mangle
    ├── Raw
    └── Connections
```

### A. Filter
Digunakan untuk:
- Accept
- Drop
- Reject

Contoh:
```
Trafik
  ↓
Firewall
  ↓
Accept / Drop
```

### B. NAT
Digunakan untuk translaasi alamat.

Contoh:
```
LAN
192.168.10.0/24
       │
       ▼
   MikroTik
       │
       ▼
Internet
```

Masquerade:
```
/ip firewall nat
add chain=srcnat out-interface=ether1 action=masquerade
```

### C. Mangle
Digunakan untuk menandai:
- Connection
- Packet
- Routing

Contoh:
```
Packet
  ↓
Mangle
  ↓
Packet Mark
  ↓
Routing / Queue
```

## 9. System
### Fungsi
Menu System digunakan untuk mengantur sistem operasi RouterOS

```
System
├── Resources
├── Packages
├── Clock
├── Identity
├── Users
├── Backup
├── Reset Configuration
├── License
└── RouterBOARD
```

### A. Resources
Melihat
- CPU
- RAM
- Storage
- Uptime

```
/system resource print
```

### B. Identity
Mengubah nama router.

Contoh:
```
MikroTik --> R1-LAB
```

### C. Users
Mengatur user RouterOS

Contoh:
```
admin
network-admin
readonly
```
Hak akses dapat dibatasi berdasarkan:
- Full
- Read
- Write
- Policy

### D. Backup
membuat backup:
```
/system backup save name=backup
```

### E. Reset
```
/system reset-configuration
```

### F. Clock
Mengatur waktu router.

Waktu yang benar penting untuk:
- Log
- Certificate
- VPN
- Troubleshooting

## 10. Tools
Menu Tools berisi berbagai alat untuk monitoring dan troubleshooting

```
Tools
├── Ping
├── Traceroute
├── Torch
├── Packet Sniffer
├── Bandwidth Test
├── Profile
├── Netwatch
└── MAC Server
```

### A. Ping
Menguji konektivitas.
```
/ping 8.8.8.8
```
### B. Traceroute
Melhat jalur paket.
```
/tool traceroute 8.8.8.8
```
### C. Torch
Melihat trafik secara real-time
```
Interface --> Torch --> Traffic Monitor
```
Dapat melihat:
- Source
- Destination
- Protocol
- Port
- TX
- RX

### D. Packet Sniffer
Menangkap paket jaringan, Dapat digunakan untuk menganalisis:
- ARP
- ICMP
- TCP
- UDP
- DNS
- DHCP

### E. Bandwidth Test
MEnguji performa jaringan antara perangkat MikroTik

### F. Profil
Melihat penggunaan CPU berdasarkan proses.

Berguna untuk:
```
CPU tinggi --> Profile --> Cari penyebab
```

### G. Netwatch
Memantau status host.
contoh:
```
Host --> Ping --> UP/DOWN
```
Dapat digunakan untuk menjalankan script ketika host berubah status.

## Hubungan Antar-Menu
contoh ketika membuat jaringan LAN:
```
Interfaces --> Bridge --> IP Address --> DHCP Server --> Firewall NAT --> Queue
```
Contoh lengkap:
```
┌──────────────┐
│ Interfaces   │
└──────┬───────┘
       ↓
┌──────────────┐
│ Bridge       │
└──────┬───────┘
       ↓
┌──────────────┐
│ IP Address   │
└──────┬───────┘
       ↓
┌──────────────┐
│ DHCP Server  │
└──────┬───────┘
       ↓
┌──────────────┐
│ Firewall NAT │
└──────┬───────┘
       ↓
    Internet
```

### Skenario PC tidak bisa internet

Gunakan menu berikut:
```
1. Interfaces
   ↓
   Cek link

2. IP
   ↓
   Cek IP Address

3. IP → DHCP Client
   ↓
   Cek IP WAN

4. Routing
   ↓
   Cek Default Route

5. IP → DNS
   ↓
   Cek DNS

6. Firewall → NAT
   ↓
   Cek Masquerade

7. Tools → Ping
   ↓
   Test koneksi
```

### Skenario Bandwith Client Terlalu Besar

Masuk ke:
```
Queue
```
Gunakan:
- Simple Queue.
- Queue Tree.

### Skenario ingin Memblokir Trafik
Masuk ke:
```
IP
 ↓
Firewall
 ↓
Filter Rules
```

### Skenario ingin Melihat Trafik
Masuk ke:
```
Tools
 ↓
Torch
```
Atau
```
Tools
 ↓
Packet Sniffer
```

## Peta Hafalan Menu RouterOS
```
INTERFACES
↓
Port & Interface

BRIDGE
↓
Layer 2

IP
↓
Address & Services

ROUTING
↓
Jalur Paket

PPP
↓
PPP & VPN

WIRELESS
↓
WiFi

QUEUE
↓
Bandwidth

FIREWALL
↓
Security & NAT

SYSTEM
↓
RouterOS

TOOLS
↓
Monitoring & Troubleshooting
```
## Latihan
### Latihan 1 - Eksplorasi Menu

Buka setiap menu dan catat:

|Menu	|Fungsi|
|-|-|
Interfaces|	Interface dan port
Bridge|	Layer 2
IP	|Layanan IP
Routing	|Jalur paket
PPP	|PPP dan VPN
Wireless|	WiFi
Queue	|Bandwidth
Firewall|	Security
System	|Sistem RouterOS
Tools	|Monitoring

### Latihan 2 - Temukan Menu Berdasarkan Masalah

Jawab tanpa melihat catatan:
```
1. Mengatur IP Address?
IP → Addresses
2. Mengatur DHCP Server?
IP → DHCP Server
3. Membuat Static Route?
IP → Routes

atau menu Routing sesuai tampilan versi RouterOS.

4. Membatasi bandwidth?
Queue
5. Melihat trafik real-time?
Tools → Torch
6. Mengatur user?
System → Users
7. Melakukan backup?
System → Backup
8. Membuat aturan blokir?
IP → Firewall → Filter Rules
9. Membuat VPN berbasis PPP?
PPP
10. Menghubungkan beberapa port Layer 2?
Bridge
```