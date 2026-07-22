# Ethernet

## 1. Ethernet

Ethernet merupakan teknologi jaringan Layer 2 (Data Link Layer) yang digunakan untuk menghubungkan perangkat dalam satu Local Area Network (LAN).

Ethernet bekerja menggunakan MAC Address, bukan IP Address.

Contoh komunikasi:
```
PC1 > Switch > Router > Switch > PC2
```
Ketika PC1 ingin mengirim data ke PC2, perangkat akan mengirim Ethernet Frame yang berisi alamat MAC tujuan dan alamat MAC sumber.

## 2. MAC Address

MAC (Media Access Control) Address adalah alamat fisik yang dimiliki setiap Network Interface Card (NIC).

Panjang MAC Address adalah 48 bit (byte).

Contoh:
```
D4:01:3C:7A:5B:11 atau D4-01-C3-7A-5B-11
```

Struktur:
```
D4:01:C3    |   7A:5B:11
Vendor      |   Device
```

- 24 bit pertama = OUI (Vendor)
- 24 bit terakhir = Nomor unik perangkat

### Fungsi MAC Address

- identitas perangkat pada jaringan LAN.
- Digunakan Switch untuk meneruskan frame.
- Digunakan ARP untuk memetakan IP ke MAC.

## 3. ARP (Address Resolution Protocol)

ARP digunakan untuk mengetahui MAC Address dari sebuah IP Address dalam jaringan yang sama.

Contoh:

PC1 ingin menghubungi:
```
192.168.10.20
```
Tetapi PC1 hanya mengetahui IP.

Langkahnya:
1. PC1 mengirim ARP Request (Broadcast)
2. Semua perangkat menerima paket tersebut
3. Hanya perangkat dengan IP tujuan yang membalas (ARP Reply).
4. PC1 menyipan hasilnya ke ARP Table.

Contoh ARP
```
Who has 192.168.10.20?
Tell 192.168.10.10
```

Balasan:
```
192.168.10.20 is at
D4:01:C3:7A:5B:11
```

## 4. Broadcast

Broadcast adalah paket yang dikirim ke seluruh perangkat dalam satu jaringan.

MAC Broadcast:
```
FF:FF:FF:FF:FF:FF
```
Contoh protocol yang menggunakan Broadcast:
- ARP Requst
- DHCP Discover

Broadcast tidak melewati Router secara default.

## 5. Collision

Collision terjadi ketika dua perangkat mengirim data pada media yang sama secara bersamaan.

Dulu sering terjadi pada:

- HUB
- Coaxial Ethernet

Saat collision terjadi:

- Data Rusak.
- Pengiriman diulang 
- Performa jaringan menurun.

Switch modern hampir menghilangkan collision karena setiap port menjadi collision domain sendiri.

## 6. Duplex

### Half Duplex
pengiriman data hanya satu arah dalam satu waktu.

Contoh:
```
PC ------- Switch
Kirim Atau Terima
```
Tidak bisa bersamaan.

### Full Duplex
pengiriman data penerimaan data dapat dilakukan secara bersamaan.

```
PC <---------------> Switch
```
inilah mode yang digunakan hampir semua jaringan Ethernet modern.

### Ringkasan

| Konsep | Fungsi |
| ------ | ------ |
| Ethernet | Komunikasi Layer 2 |
| MAC Address | Identitas fisik perangkat |
| ARP | Mencari MAC dari IP |
| Broadcast | Mengirim ke semua perangkat |
| Collision | Tabrakan data pada media bersama |
 Duplex | Mode komunikasi jaringan |

## Praktik MikroTik
### 1. melihat ARP Table
Masuk ke Terminal:
```
/ip arp print
```

Contoh hasil:
| ADDRESS | MAC-ADDRESS | INTERFACE |
|-|-|-|
|192.168.10.2|  08:00:27:AA:11:22| ether2|
|192.168.10.3| 08:00:27:BB:22:33| ether2|

Penjelasan:
- Address = IP perangkat
- MAC Address = Alamat fisik
- Interface = Port Tempat Perangkat terhubung

### 2. Menggunakan Torch
Torch digunakan untuk memonitor trafik jaringan secara real-time.

Melalui WinBox:
```
Tools > Tocrch
```
Pilih interface:
```
ether2
```
Kemudian klik Start.

informasi yang ditampilkan:

- Source Address
- Destination Address
- MAC Address
- Protocol
- Port
- TX/RX Rate
- Packer per Second

### Latihan
Lakukan ping dari PC1 ke PC2.

Amati:

- IP Source
- IP Destination
- Protocol ICMP
- Besar trafik


### 3. Menggunakan Packet Sniffer
Masuk:
```
Tools > Packet Sniffer

Pilih : Interface = ether2

Klik Start
```

Lakukan aktivitas:

- Ping
- Buka Website
- DHCP Request

`Kemudian STOP`

Lihat hasil capture.

Packet Sniffer dapat digunakan untuk melihat:

- ARP
- ICMP
- TCP
- UDP
- DNS
- DHCP
- HTTP
- HTTPS (header, bukan isi terenkripsi)


### Lab Praktik

Topologi

```
PC1 ----- MikroTik ------ PC2
```

Langkah

1. Berikan IP pada PC1 dan PC2
2. Konfigurasi IP pada Mikrotik
3. PAstikan kedua PC dapat saling ping.
4. Jalankan `/ip arp print` dan amati ARP table.
5. Jalankan Torch pada interface yang terhubung ke PC1, lalu lakukan ping dan lihat trafik ICMP.
6. Jalankan `Packet Sniffer`, ulangi ping kemudian identifikasi paket ARP Request, ARP Reply, dan ICMP Echo Request/Reply yang muncul.
