# TCP/IP

### A. IPv4
Struktur IPv4 terdiri dari 32 bit

contoh:
```
192.168.10.25
```
Setiap angka disebut octet
```
192.168.10.25
 |   |  |  |
 8   8  8  8 bit

 total : 32 bit
```
Pembagian IPv4 terdiri dari ==Network ID== ==Host ID== Misal:
```
192.168.1.20/24
Network = 192.168.1
Host = 20
```
### IPv6 Overview 

IPv6 menggunakan 128 bit
contoh : `2001:db8:1234:1::10`

Kelebihan
- Address sangat banyak
- Tidak membutuhkan NAT
- Lebih aman
- Header lebih sederhana
- Mendukung Auto Coonfiguration

Yang perlu diketahui untuk MTCNA
- Format penulisan
- Prefix
- Link Local
- Global Unicast
- Loopback

Tidak perlu menghafal seluruh RFC

### C. Subnet

Subnet adalah proses membagi jaringan menjadi jaringan yang lebih kecil.

Misalnya:
```
192.168.1.0/24

dibagi menjadi

192.168.1.0/25
192.168.1.128/25
```

Tujuan
- Menghemat IP
- Mempermudah routing
- Mengurangi Broadcast

### D. CIDR

CIDR adalah cara penulisan subnet menggunakan prefix

Contoh:
```
/24     =   255.255.255.0   
/25     =   255.255.255.128 
/26     =   255.255.255.192 
```
Harus hafal minimal

| Prefix  | Mask |
| ------- | ---- |
|/24 | 255.255.255.0 |
|/25 | 255.255.255.128 |
|/26 | 255.255.255.192 |
|/27 | 255.255.255.224 |
|/28 | 255.255.255.240 |
|/29 | 255.255.255.248 |
|/30 | 255.255.255.252 |

### E. Broadcast Address
Broadcast adalah alamat terakhir dalam subnet. 
contoh:
```
192.168.1.0/24
192.168.1.255   =   Broadcast
```

### F. Network Address
Alamat Pertama
contoh:
```
192.168.10.0/24
192.168.10.0       =    Network
```

### G. Host Address
Alamat yang dapat dipakai perangkat.
Contoh:
```
192.168.10.1 Hingga 192.168.10.254
```

### H. Private IP
Tidak dapat digunakan langsung di internet.
```
Range
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

### I. Public IP
Alamat yang diberikan ISP.
contoh:
```
8.8.8.8
1.1.1.
36.xxx.xxx.xxx
```

Public IP bersifat unik di Internet.

### Praktik Subnet Tanpa kalkulator

Misal:
```
192.168.10.35/27
```
Berikut Cara menghitung subnet nya

Cari Block size
```
256-224 =   32
```

Kelipatan
```
0
32
64
128
160
192
224
```

cari posisi IP
```
35 berada di 32-63
```

Jawaban

```
Network     =   192.168.10.32
Broadcast   =   192.168.10.63
Host        =   33  -   62
```

### Berikut 30 Soal untuk latihan hitung Subnet

Mudah
```
1.  192.168.1.25/24
2.  192.168.1.100/25
3.  192.168.1.200/25
4.  10.10.10.45/26
5.  10.10.10.90/26
6.  172.16.10.150/27
7.  172.16.10.50/27
8.  192.168.20.180/28
9.  192.168.20.50/28
10. 192.168.100.10/29
```
Sedang
```
11. 192.168.40.65/26
12. 192.168.40.126/26
13. 192.168.40.200/27
14. 10.20.30.170/28
15. 10.20.30.250/29
17. 172.20.10.140/28
18. 192.168.88.88/30
19. 192.168.88.130/25
20. 192.168.88.190/26
```
Sulit
```
21. 10.0.15.222/27
22. 10.0.15.87/28
23. 10.0.15.33/29
24. 172.31.200.45/26
25. 172.31.200.190/27
26. 192.168.254.200/29
27. 192.168.254.130/30
28. 192.168.254.70/27
29. 192.168.100.240/28
30. 192.168.50.127/25
```

Untuk setiap soal, tentukan :

- Network Address
- Broadcast Address
- First Host
- Last Host
- Jumlah Host
- Subnet Mask
- CIDR

### Lab Praktik

PC1 <---> Mikrotik <---> PC2

Skema IP
```
PC1 
IP      :   192.168.10.2/24
Gateway :   192.168.10.1

Router
ether1  :   192.168.10.1/24
ether2  :   192.168.20.1/24

PC2
IP      :   192.168.20.2/24
Gateway :   192.168.20.1
```

Konfigurasi MikroTik

```
/ip address
add address=192.168.10.1/24 interface=ether2
add address=192.168.20.1/24 interface=ether1

/ip address print
```

Pengujian
```
Dari PC1:
ping 192.168.10.1
ping 192.168.20.1
ping 192.168.20.2

Dari PC2:
ping 192.168.10.2
```

Jika semua berhasil, berarti routing antar dua jaringan sudah berjalan.

