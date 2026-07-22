# OSI Layer
Tujuan setelah mempelajari materi ini, kamu harus bisa:
Menjelaskan fungsi Layer 1-7.
Memahami proses encapsulation dan decapsulation.
Menentukan kemungkinan letak gangguan ketika jaringan bermasalah.
### Layer 1 - Physical

Fungsi mengirim bit melalui media fisik.
Contoh perangkat:
```
Kabel UTP
Fiber Optic
RJ45
Hub
Repeater
```
Masalah yang sering terjadi:
```
Kabel putus
NIC mati
Port switch rusak
Lampu Link mati
```
Gejala:
```
Tidak ada link.
Interface down.
Tidak bisa ping sama sekali.
```
### Layer 2 - Data Link
Fungsi mengirim frame berdasarkan MAC Address.
Contoh:
```
Ethernet
Switch
Bridge
VLAN
STP
```
Masalah:
```
MAC tidak terbaca
VLAN salah
Port salah VLAN
STP blocking
```
Gejala:
```
Link hidup tetapi komunikasi gagal.
ARP gagal.
```
### Layer 3 - Network

Fungsi routing berdasarkan IP Address.

Perangkat:
```
Router
Layer 3 Switch
```
Protocol:
```
IP
ICMP
OSPF
RIP
BGP
```
Masalah:
```
Salah IP
Salah subnet
Gateway salah
Routing belum ada
```
Gejala:
```
Ping gateway gagal.
Tidak bisa ke jaringan lain.
```
### Layer 4 - Transport

Fungsi mengirim data menggunakan TCP atau UDP.

Protocol:
```
TCP
UDP
```
Masalah:
```
Port tertutup
Firewall
TCP timeout
```
Gejala:
```
Ping berhasil.
Web tidak bisa dibuka.
SSH gagal.
```
Layer 5 - Session

Fungsi mengelola sesi komunikasi.
Contoh:
```
NetBIOS
RPC
Session SMB
```
Masalah:
```
Session timeout
Login gagal
```
### Layer 6 - Presentation

Fungsi format data.
Contoh:
```
SSL/TLS
Encryption
Compression
JPEG
PNG
```
Masalah:
```
Sertifikat salah
TLS error
Format data rusak
```
Layer 7 - Application

Fungsi berhubungan langsung dengan aplikasi pengguna.

Protocol:
```
HTTP
HTTPS
FTP
DNS
SMTP
SSH
```
Masalah:
```
DNS error
Apache mati
Web server mati
Salah konfigurasi aplikasi
```

### Ringkasan
|Layer	|Nama	|Contoh
|---|---|---|
|7	|Application	|HTTP, FTP, DNS
|6	|Presentation	|SSL, Encryption
|5	|Session	|RPC, SMB
|4	|Transport	|TCP, UDP
|3	|Network	|IP, ICMP, Router
|2	|Data Link	|MAC, Switch, VLAN
|1	|Physical	|Kabel, Fiber, Hub

### Encapsulation
Saat data dikirim dari PC:
```
Application
↓
Presentation
↓
Session
↓
Transport
↓
Network
↓
Data Link
↓
Physical
```
Setiap layer menambahkan informasi (header) sebelum data dikirim.
Contohnya:
```
Data
↓
TCP Header
↓
IP Header
↓
Ethernet Header
↓
Bit
```
### Decapsulation

Saat data diterima:
```
Bit
↓
Ethernet
↓
IP
↓
TCP
↓
Application
```
Setiap layer membuka header hingga data sampai ke aplikasi.

### Latihan Troubleshooting
Kasus 1
```
Lampu LAN mati.
Kemungkinan: Layer 1
```
Kasus 2
```
Kabel terpasang, tetapi interface "down".
Kemungkinan: Layer 1
```
Kasus 3
```
Ping ke gateway gagal.
Kemungkinan: Layer 1, Layer 2, Layer 3

Lakukan pengecekan berurutan:
- Apakah kabel/link aktif? (Layer 1)
- Apakah MAC dan VLAN benar? (Layer 2)
- Apakah IP, subnet mask, dan gateway benar? (Layer 3)
```
Kasus 4
```
Ping gateway berhasil, tetapi tidak bisa internet.
Kemungkinan:
- Layer 3 (routing/default route)
- Layer 7 (DNS jika hanya nama domain yang gagal)
```
Kasus 5
```
Ping 8.8.8.8 berhasil, tetapi google.com gagal.

Kemungkinan: Layer 7 (DNS)
```
Kasus 6
```
Website tidak bisa dibuka, tetapi ping server berhasil.
Kemungkinan:
- Layer 4 (port 80/443 diblokir)
- Layer 7 (web server mati)
```
Kasus 7
```
SSH tidak bisa masuk, tetapi ping berhasil.
Kemungkinan:
- Layer 4 (port 22 diblokir)
- Layer 7 (service SSH tidak berjalan)
- Cara Berpikir Saat Ping Gagal
```

### Jangan langsung menebak. Gunakan urutan OSI dari bawah ke atas.

Layer 1: Apakah kabel, NIC, dan link LED normal?

Layer 2: Apakah VLAN, switch, dan ARP benar?

Layer 3: Apakah IP, subnet, gateway, dan routing sudah benar?

Layer 4-7: Jika ping sudah berhasil tetapi layanan tertentu gagal, baru periksa port, firewall, DNS, atau aplikasi.
