# Topologi Jaringan & Perangkat Jaringan
Materi ini penting untuk memahami bagaimana perangkat jaringan saling terhubung. jangan hanya menghafal bentuknya. Yang perlu di pahami adalah alur komunikasi, kelebihan, kekurangan, dan dampak jika salah satu link atau perangkat gagal.

## 1. Topologi Jaringan

### A. Bus Topology
Semua perangkat terhubung pada satu kabel utama.

```
PC1 ─── PC2 ─── PC3 ─── PC4
       Backbone Cable
```
Kelebihan
- struktur sederhana.
- Menggunakan kabel lebih sedikit.
- Biaya relatif murah.

Kekurangan
- Jika kabel utama rusak, jaringan dapat terganggu.
- Sulit melakukan troubleshooting.
- Collision cukup tinggi.
- Tidak cocok untuk jaringan modern.

### B. Ring Topology
Setiap perangkat terhubung membentuk lingkaran.
```
      PC1
    /     \
  PC4     PC2
    \     /
      PC3

```
Data biasanya berjalan dari satu perangkat ke perangkat berikutnya

Kelebihan
- Aliran data teratur.
- Collision lebih rendah dibandingkan Bus.

Kekurangan
- Satu titik putus dapat mengganggu jaringan.
- Penambahan perangkat dapat mengganggu jaringan.
- Troubleshooting lebih sulilt.

### C. Star Topology
Semua perangkat terhubung ke satu perangkat pusat.

```
        PC1
         |
PC2 ── Switch ── PC3
         |
        PC4
```
Ini adalah topology yang paling umum digunakan pada jaringan LAN modern.

Kelebihan
- Mudah dikelola.
- Mudah melakukan torubleshooting.
- Jika satu kabel rusak, perangkat lain tetap berjalan.

kekurangan 
- Jika perangkat pusat rusak, banyak perangkat terdampak.
- Membutuhkan lebih banyak kabel.

### D. Mesh Topology
Setiap perangkat terhubung dengan banyak perangkat lainnya.

```
     R1
   / |  \
  /  |   \
R2───┼───R3
  \  |   /
   \ |  /
     R4
```
Kelebihan
- Redudansi sangat tinggi.
- Banyak jalur alternatif.
- Sangat tahan terhadap kegagalan link.

Kekurangan
- Membutuhkan banyak kabel.
- Konfigurasi lebih kompleks.
- Biaya tinggi.

Biasanya digunakan pada:
- Backbone jaringan.
- Data center.
- Jaringan antar router.

### E. Hybrid Topology
Gabungan dari beberapa topologi 
Contoh:
```
     Star
      |
Bus ──┼── Ring
      |
     Mesh
```

## 2. Perbandingan Topologi
|Topologi|Kelebihan|Kekurangan
|-|-|-|
| Bus|Murah, sederhana|Kabel utama rusak, jaringan terganggu|
|Ring|Aliran data teratur|Putus satu titik bisa berdampak|
|Star|Mudah dikelola|Bergantung pada perangkat pusat|
|Mesh|Redundansi tinggi|Mahal dan Kompleks|
|Hybrid|Fleksibel|Desain dan maintance kompleks|

## 3. Perbedaan Hub, Switch, Bridge, dan Router

### A. Hub
Hub bekerja pada:
> Layer 1 - Physical

Cara kerjanya:
```
PC1 → Hub → PC2
          → PC3
          → PC4
```
Ketika menerima data, Hub mengirimkan data ke semua port.

Karakteristik
- tidak memahami MAC Address
- Tidak melalkukan filtering frame.
- Semua perangkat berada dalam satu Collision Domain.
- Menggunakan Half Duplex.

```
PC1 mengirim
      ↓
    HUB
  ↙ ↓ ↓ ↘
PC2 PC3 PC4
```
Hub sudah jarang digunakan karena switch jauh lebih efisien

### B. Switch
Switch bekerja terutama pada:
> Layer 2 - Data Link

Swtich menggunakan MAC Address Table untuk menentukan ke mana frame harus di kirim.
```
PC1 ──┐
      │
PC2 ──┼── Switch
      │
PC3 ──┘
```

Contoh: 
```
PC1 → Switch → PC3
```

Switch tidak perlu mengirim frame ke PC2 jika mengetahui MAC Address PC3 berada di port tertentu.

Karakteristik
- Memahami MAC Address.
- Menyimpan MAC Address Table.
- Mengurangi collision.
- Setiap port menjadi Collision Domain tersendiri.
- mendukung Full Duplex.

### C. Bridge
Bridge juga bekerja pada:
> Layer 2 Data Link

Fungsi utamanya adalah menghubungkan dan memisahkan dua segmen jaringan.

```
LAN 1 ─── Bridge ─── LAN 2
```

Bridge dapat dianggep sebagai:
> Switch dengan jumlah port yang lebih sedikit.

Pada MikroTik, fitur Bridge dapat digunakan untuk menggabungkan beberapa interface agar berfungsi sebagai satu jaringa Layer 2

### D. Router

Router bekerja pada:

> Layer 3 - Network

Router meneruskan paket berdasarkan:

> IP Address

Contoh:

```
192.168.1.0/24
        |
     Router
        |
192.168.2.0/24
```
Router menghubungkan jaringan yang berbeda.

Contoh:

```
PC1
192.168.1.2
     |
     |
192.168.1.1
   Router
192.168.2.1
     |
     |
192.168.2.2
   PC2
```
Router melihat:
```
Source IP
Destination IP
Routing Table
```

## 4. Perbandingan Utama
|Perangkat |Layer|Menggunakan|Fungsi Utama|
|-|-|-|-|
|Hub|1|Signal|Mengirim ke semua port|
|Bridge|2|MAC Address|Menghubungkan segmen LAN|
|Swtich|2|MAC Address|Meneruskan frame ke port tujuan|
|Router|3|IP Address|Menghubungkan jaringan berbeda|

## 5. Contoh Cara Kerja
Misalnya:
```
PC1
192.168.1.10
   |
Switch
   |
Router
   |
Switch
   |
PC2
192.168.2.10
```

Ketika PC1 mengirim data ke PC2:

Layer 1 :   Bit dikirim melalui kabel.
Layer 2 :   Frame menggunakan MAC Address.
Layer 3 :   Router Melihat IP:
```
192.168.1.10
        ↓
192.168.2.10
```
Router kemudian mencari jalur melalui Routing Table.

## 6. Latihan Identifikasi
Tentukan perangkat yang tepat:
1. Semua data dirikim ke semua port     :   Hub
2. Perangkat menggunakan MAC Address Table  :   Switch
3. Menghubungkan dua jaringan IP Berbeda    :   Router
4. Menghubungkan dua segman LAN pada Layer 2    :   Bridge
5. Satu perangkat pusat menghubungkan banyak PC :   Star Topology
6. Membutuhkan banyak jalur alternatif  :   Mesh Topology
