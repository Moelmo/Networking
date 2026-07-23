# MikroTik RouterOS

Installation, Upgrade, Downgrade, License, Netinstall, Reset, Backup, Export & Import.

## 1. Apa itu MikroTik RouterOS
MikroTik RouterOS adalah sistem operasi berbasis Linuz yang dikembangkan oleh MikroTik untuk menjalankan fungsi networking.

RouterOS dapat digunakan pada:
- Perangkat RouterBoard MikroTik.
- MikroTik CHR.
- PC x86
- Mesin Virtual.
- Clound server.

RouterOS memungkinkan sebuah perangkat melakukan berbagai fungsi jaringan seperti:
- Routing
- Switching
- Firewall
- NAT
- DHCP Server
- DHCP Client
- DNS
- VPN
- Wireless
- Hotspot
- QoS
- Monitoring
- User Management

Contoh:
```
PC ----- MikroTik RouterOS ----- Internet
```
RouterOS bertindak sebagai sistem operasi yang mengatur bagaimana perangkat jaringan bekerja.

## 2. Cara Mengakses RouterOS

RouterOS dapat  diakses menggunakan beberapa metode.

### A. WinBox
Winbox merupakan aplikasi GUI untuk mengelola MikroTik.

Kelebihan:
- Mudah digunakan
- Mendukung MAC WinBox.
- Dapat digunakan ketika IP belum dikonfigurasi.

Contoh:
```
WinBox -> MAC Address / IP Address -> Login -> RouterOS
```

### B. WebFIg
WebFig adalah antermuka RouterOS berbasis web.

Akses:
```
http://IP-ROUTER
```

Contoh:
```
http://192.168.88.1
```

### C. SSH
SSH digunakan untuk akses CLI secara remote.
```
ssh admin@192.168.88.1
```

### D. Terminal
Terminal dapat digunakan melalui:
- WinBox
- WebFig
- SSH
- Serial Console

Contoh:
```
/system resource print
```

### E. MAC WinBox
MAC WinBox memungkinkan akses ke router menggunakan MAC Address.

Contoh:
```
MAC Address -> D4:01:C3:AA:BB:CC
```
Keuntungannya:
- Tidak membutuhkan IP Address
- Berguna saat konfigurasi awal.
- Berguna ketika IP Address bermasalah.

## 3. Instalasi RouterOS
RouterOS dapat diinstall pada beberapa platform.

### A. RouterBoard
RouterBoard sudah memiliki RouterOS dari pabrik.

Contoh:
```
MikroTik hAP Lite
MikroTik hEX
MikroTik CCR
```
Ketika perangkat dinyalakan:
```
Hardware -> RouterOS -> MikroTik Router
```
CHR sangat cocok untuk belajar karena tidak membutuhkan perangkat fisik.

### C. RouterOS x86
RouterOS juga dapat dijalankan pada komputer berbasis x86.
Contoh:
```
PC -> RouterOS -> Router
```
PC tersebut kemudian dapat berfungsi sebagai router.

## 4. Upgrade RouterOS
Upgrade adalah proses memperbarui RouterOS ke versi yang lebih baru.

Contoh:
```
RouterOS 7.16 -> RouterOS 7.17
```
Tujuan upgrade:
- Mendapatkan fitur baru.
- Memperbaiki bug.
- Memperbaiki keamanan.
- Mendukung Hardware baru.
- Memperbagiki performa.

### Mengecek versi RouterOS

```
/system resource print
```

Contoh:
```
version : 7.20
```
Atau:
```
/system package print
```

### Mengecek Update
```
/system package update check-for-updates
```
Contoh:
```
channel: stable
installed-version: 7.19
latest-version: 7.20
```

### Menginstal Update
```
/system package update install
```
Router akan:
```
Download Package -> Install Package -> Reboot -> RouterOS Baru
```

### Hal yang Harus Dilakukan Sebelum Upgrade

Sebelum upgrade:

1. Backup
2. Export
3. Cek kompatibilitas
4. Pastikan Listrik stabil
5. Pastikan koneksi tidak terputus

Minimal:
```
/system backup save name=before-upgrade
/export file=before-upgrade
```
## 5. Downgrade RouterOS

Downgrade adalah proses menurunkan versi RouterOS
Contoh:
```
RouterOS 7.20
      ↓
RouterOS 7.19
```

Downgrade biasanya dilakukan ketika:
- Versi baru memiliki bug.
- Fitur tertentu tidak berjalan.
- Hardware memiliki masalah kompatibilitas.
- Membutuhkan versi lama untuk lab tertentu.

### Proses Downgrade
Secara umum:

1. Download package versi lama
2. Upload package ke router
3. Jalnkan downgrade
4. Router reboot

Perintah:
```
/system package downgrade
```

### Upgrade vs Downgrade

|Proses|Arah|
|-|-|
|Upgrade|Versi lama -> Versi Baru|
|Downgrade|Versi Baru -> Versi lama|

Contoh:
```
7.16 → 7.17 = Upgrade

7.17 → 7.16 = Downgrade
```

## 6. RouterOS Package
RouterOS dapat meiliki beberapa package.
Contoh:
```
routeros
wireless
routing
security
container
```
Untuk melihat  package:
```
/system package print
```
Pada RouterOS versi modern, banyak fungsi telah digabungkan ke dalam package utama.

## 7. License RouterOS
Lisensi menentukan fitur dan batasan penggunaan RouterOS
### Pada RouterBoard
Lisensi biasanya sudah terpasang di perangkat.
### Pada CHR
CHR memiliki model lisensi yang berbeda.

Secara umum terdapat:
- Free
- Paid License

Untuk mnegecek lisensi:
```
/system licensi print
```

Contoh infromasi:
```
software-id
system-id
license-level
```

## 8. Netinstall
### Apa itu Netinstall?
Netinstall adalah tool resmi MikroTik untuk:
- Menginstal ulang RouterOS.
- Menghapus konfigurasi.
- Memulihkan perangkat yang bermasalah.
- melakukan reinstall sistem.

Konsepnya:
```
PC
│
│ Ethernet
│
MikroTik
```

PC menjalankan:
```
Netinstall
```
MikroTik melakukan:
```
Boot melalui Network
        ↓
Menerima RouterOS
        ↓
Install ulang
```

### Kapan Menggunakan Netinstall?
Gunakan Netinstall Jika:
- RouterOS rusak.
- Router mengalami boot problem.
- Konfigurasi sangat kacau.
- Reset biasa tidak menyelesaikan masalah.
- Ingin melakukan clean installation.

### Reset vs Netinstall

Reset
```
Konfigurasi dihapus
        ↓
RouterOS tetap
```
Netinstall
```
RouterOS diinstal ulang
        ↓
Konfigurasi dihapus
```

Perbedaan sederhana:
> Reset menghapus konfigurasi. Netinstall menginstal ulang sistem RouterOS.

## 9. Reset RouterOS
Reset mengembalikan konfigurasi router ke kondisi awal.

### Reset melalui CLI
```
/system reset-configuration
```
Router akan meminta konfirmasi.

Reset tanpa default configuration
```
/system reset-configuration no-default=yes
```

Hasilnya:
```
Router
 ↓
Tidak memiliki konfigurasi default
```
Ini sangat berguna untuk lab.

### Reset melalui WinBox
Masuk ke:
```
System -> Reset configuration
```
Kemudian pilih:
- Keep User Configuration
- No Default Configuration.
- Do Not Backup.

## 10. Backup
Backup digunakan untuk menyimpan konfigurasi RouterOS dalam format binary.

Perintah:
```
/system backup save name=backup-lab
```
File:
```
backup-lab.backup
```

### Melihat File
```
/file print
```
Contoh:
```
backup-lab.backup
```

### Restore Backup
```
/system backup load name=backup-lab.backup
```
Router biasanya melakukan reboot.

Alur:
```
Router -> Backup -> Konfigurasi Diubah -> Restore -> Konfigurasi Lama Kembali
```

## 11. Karakteristik Backup

Backup:
- Berformat binary.
- Tidak mduah dibaca manusia.
- Tidak praktis untuk diedit.
- Cocok untuk restore cepat.
- Menyimpan konfigurasi router secara keseluruhan.

Contoh:
```
router.backup
```

## 12. Export
Export menyimpan konfigurasi dalam bentuk teks RouterOS Script

perintah
```
/export file=router-config
```
Hasil:
```
router-config.rsc
```

Contoh isi:
```
/ip address
add address=192.168.10.1/24 interface=ether2

/ip route
add gateway=192.168.10.254
```

Karena berbentuk teks, file dapat:
- Dibaca 
- Diedit
- Dipelajari
- Didokumentasikan
- Digunakan untuk migrasi

## 13. Export Konfigurasi Tertentu
hanya export IP Address:
```
/ip address export
```
Firewall:
```
/ip firewall export
```
Interface:
```
/interface export
```
Routing:
```
/ip route export
```

## 14. Import
Import digunakan untuk menjalankan konfigurasi dari file `.rsc`
```rsc
/import file-name=router-config.rsc
```

Alur:
```
Export -> File .rsc -> Reset -> Import -> Konfigurasi Kemabli
```

## 15. Backup vs Export

|Fitur|Backup|Export|   
|-|-|-|
|Extension|`.backup`| `.rsc`|
|Bisa diedit|Tidak Praktis|Ya|
|Mudah dibaca|Tidak|Ya|
|Restore|Backup Load|Import|
|Cocok Untuk| Restore Cepat|Migrasi & Dokumentasi|

## 16. Contoh Konfigurasi Lab
Topologi:
```
PC1 -> ether2 -> MikroTik -> ether1 -> Internet
```

Konfiguarsi:
```
/import file-name=router-config.rsc
```
Kemudian:
```
/system backup save name=lab-backup
```
Dan:
```
/export file=lab-export
```
Sekarang kamu memiliki:
```
lab-backup.backup
lab-export.rsc
```

## 17. Latihan Reset Router 10 Kali

Latihan ini bertujuan agar kamu benar-benar memahami:
- Bagaimana
- Apa yang hilang setelah reset.
- Bagaimana mengakses router setelah reset.
- Cara membangun kembali konfigurasi

### Siklus Latihan
```
┌──────────────┐
│ Reset Router │
└──────┬───────┘
       ↓
┌──────────────┐
│ Konfigurasi  │
└──────┬───────┘
       ↓
┌──────────────┐
│ Test Ping    │
└──────┬───────┘
       ↓
┌──────────────┐
│ Reset Lagi   │
└──────────────┘
```

Ulangi:
```
1/10
2/10
3/10
...
10/10
```

## 18. Latihan Backup dan Restore

### Skenario
Tahap 1 - konfiguarsi:
```
/ip address
add address=192.168.10.1/24 interface=ether2
```
Tahap 2 - Backup:
```
/system backup save name=before-change
```
Tahap 3 - Ubah konfigurasi:
```
/ip address
add address=10.10.10.1/24 interface=ether2
```
Tahap 4 - Restore:
```
/system backup load name=before-change.backup
```
Tahap 5 - Periksa:
```
/ip address print
```
Pastikan konfigurasi kembali seperti sebelum perubahan.

## 19. Latihan Export dan Import

Tahap 1 - Konfigurasi router:
```
/ip address
add address=192.168.10.1/24 interface=ether2
```
Tahap 2 - Export:
```
/export file=configuration
```
Tahap 3 - Reset router:
```
/system reset-configuration
```
Tahap 4 - Import:
```
/import file-name=configuration.rsc
```
Tahap 5 - Cek:
```
/ip address print
```

## 20. Backup dan Export Tidak Selalu Sama

Hal penting:
> Backup dan Export tidak selalu menghaslingkan konfigurasi yang identik secara sempurna.

Backup adalah snapshot konfigurasi dalam bentuk binary.
Export adalah kumpulan command konfigurasi dalam bentuk scirpt.

Beberapa hal seperti:
- Inofrmasi hardware.
- Certificate tertentu.
- User tertentu/
- Secret.
- Data internal.

dapat memiliki perlakukan beberda tergantung jenis konfigurasi dan versi RouterOS.

Karena itu, praktik terbaik adalah:
```
Backup + Export
```
Bukan hanya salah satunya.

## 21. Best Practice
Sebelum perubahan besar:
```
/system backup save name=before-change
/export file=before-change
```
Setelah konfigurasi berhasil:
```
/system backup save name=working-config
/export file=working-config
```
Contoh struktur backup:
```
backup/
├── before-upgrade.backup
├── before-upgrade.rsc
├── working-config.backup
└── working-config.rsc
```

## 22. Challenge 

Lakukan tanpa melihat catatan:
```
1. Reset router
2. Buat konfigurasi IP
3. Buat DHCP
4. Buat NAT
5. Backup
6. Export
7. Ubah konfigurasi
8. Restore backup
9. Reset router
10. Import export
```
Kemudian bandingkan hasil:
```
Backup → Restore vs Export → Import
```

## 23. Command yang Wajib Hafal

Cek Versi
```
/system resource print
```
Cek Package
```
/system package print
```
Cek Update
```
/system package update check-for-updates
```
Upgrade
```
/system package update install
```
Downgrade
```
/system package downgrade
```
Cek License
```
/system license print
```
Reset
```
/system reset-configuration
```
Backup
```
/system backup save name=backup
```
Restore
```
/system backup load name=backup.backup
```
Export
```
/export file=config
```
Import
```
/import file-name=config.rsc
```
Melihat File
```
/file print
```

