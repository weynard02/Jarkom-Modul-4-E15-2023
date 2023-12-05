# Jarkom-Modul-4-E15-2023

<table>
    <tr>
        <th colspan=2> Kelompok E15 </th>
    </tr>
    <tr>
        <th>NRP</th>
        <th>Nama Anggota</th>
    </tr>
    <tr>
        <td>5025211014</td>
        <td>Alexander Weynard Samsico</td>
    </tr>
  <tr>
        <td>5025211121</td>
        <td>Frederick Yonatan Susanto</td>
    </tr>
</table>

# Topologi
Topologi awal yang diberikan sebagai berikut:
![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/410ecb71-a113-434e-90d5-5e9b05ce81c1)

Kita diminta untuk melakukan suatu konfigurasi subnetting dan routing pada topologi di atas dengan menggunakan metode
- VLSM (GNS3)
- CIDR (CPT)

# Konfigurasi Awal
Pertama, kita melakukan penentuan subnet terlebih dahulu. Suatu subnet dapat ditentukan antara router sehingga kita mendapatkan subnet sebagai berikut
![subnet](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/bf812727-9c59-422d-ab9d-25919d703029)

Dari hasil ini dapat kita tuliskan dalam bentuk tabel yang disediakan oleh spreadsheet sebagai berikut
| Nama Subnet | Rute                                            | Jumlah IP | Netmask |
| ----------- | ----------------------------------------------- | --------- | ------- |
| A1          | Fern-Switch4-LaubHills-Switch4-AppetitRegion    | 1023      | /21     |
| A2          | Frieren-Switch3-LakeKorridor                    | 25        | /27     |
| A3          | Denken-Switch2-RoyalCapital-Switch2-WilleRegion | 127       | /24     |
| A4          | Flamme-Switch5-RohrRoad                         | 1001      | /22     |
| A5          | Flamme-Fern                                     | 2         | /30     |
| A6          | Frieren-Flamme                                  | 2         | /30     |
| A7          | Aura-Frieren                                    | 2         | /30     |
| A8          | Aura-Denken                                     | 2         | /30     |
| A9          | Flamme-Himmel                                   | 2         | /30     |
| A10         | Eisen-Switch1-Richter-Switch1-Revolte           | 3         | /29     |
| A11         | Aura-Eisen                                      | 2         | /30     |
| A12         | Eisen-Switch0-Stark                             | 2         | /30     |
| A13         | Himmel-Switch6-SchwerMountains                  | 6         | /29     |
| A14         | Lawine-Switch7-BredRegion-Switch7-Heiter        | 31        | /26     |
| A15         | Linie-Lawine                                    | 2         | /30     |
| A16         | Eisen-Linie                                     | 2         | /30     |
| A17         | Eisen-Lugner                                    | 2         | /30     |
| A18         | Lugner-Switch10-TurkRegion                      | 1001      | /22     |
| A19         | Heiter-Switch8-Sein-Switch8-RiegelCanyon        | 512       | /22     |
| A20         | Linie-Switch11-GranzChannel                     | 255       | /23     |
| A21         | Lugner-Switch9-GrobeForest                      | 251       | /24     |
| Total       |                                                 | 4255      | /19

Penjelasan:
- Jumlah IP didapatkan melalui jumlah host + router
- Netmask didapatkan melalui netmask mana yang dapat menampung jumlah IP tersebut

Kemudian untuk mendapatkan pembagian IP, kita akan menggunakan dua metode tersebut

## VLSM
VLSM (Variable Length Subnet Masking) merupakan teknik di mana netmask akan diberikan sesuai kebutuhan jumlah alamat IP dari subnet tersebut. Jadi besar netmask disesuaikan dengan host yang membutuhkan alamat IP.

1. Melakukan pembagian rute
   
Sebelumnya, kita sudah melakukan pembagian rute dari topologi di atas. Kita mendapatkan total kebutuhan ada 4255 IP yang di mana netmask yang diperlukan adalah /19 (max = 8190)

![subnet](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/bf812727-9c59-422d-ab9d-25919d703029)

| Nama Subnet | Rute                                            | Jumlah IP | Netmask |
| ----------- | ----------------------------------------------- | --------- | ------- |
| A1          | Fern-Switch4-LaubHills-Switch4-AppetitRegion    | 1023      | /21     |
| A2          | Frieren-Switch3-LakeKorridor                    | 25        | /27     |
| A3          | Denken-Switch2-RoyalCapital-Switch2-WilleRegion | 127       | /24     |
| A4          | Flamme-Switch5-RohrRoad                         | 1001      | /22     |
| A5          | Flamme-Fern                                     | 2         | /30     |
| A6          | Frieren-Flamme                                  | 2         | /30     |
| A7          | Aura-Frieren                                    | 2         | /30     |
| A8          | Aura-Denken                                     | 2         | /30     |
| A9          | Flamme-Himmel                                   | 2         | /30     |
| A10         | Eisen-Switch1-Richter-Switch1-Revolte           | 3         | /29     |
| A11         | Aura-Eisen                                      | 2         | /30     |
| A12         | Eisen-Switch0-Stark                             | 2         | /30     |
| A13         | Himmel-Switch6-SchwerMountains                  | 6         | /29     |
| A14         | Lawine-Switch7-BredRegion-Switch7-Heiter        | 31        | /26     |
| A15         | Linie-Lawine                                    | 2         | /30     |
| A16         | Eisen-Linie                                     | 2         | /30     |
| A17         | Eisen-Lugner                                    | 2         | /30     |
| A18         | Lugner-Switch10-TurkRegion                      | 1001      | /22     |
| A19         | Heiter-Switch8-Sein-Switch8-RiegelCanyon        | 512       | /22     |
| A20         | Linie-Switch11-GranzChannel                     | 255       | /23     |
| A21         | Lugner-Switch9-GrobeForest                      | 251       | /24     |
| Total       |                                                 | 4255      | /19

2. Pembagian IP
 
Pembagian IP dilakukan dengan menggunakan pohon berdasarkan NID dan netmask. Karena netmask yang diperlukan untuk semua IP adalah /19, kita mulai dengan NID **10.44.0.0/19**

![E15-VLSM-Tree](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/3a27b8fa-8b8f-42ca-88ab-59b9555b1a23)

Penjelasan:
- Kita melakukan subnetting pembagian IP mulai dari yang terkecil terlebih dahulu (/30) sampai dengan yang terbesar yaitu /21.

3. Subnet

Dari pohon itu, kita mendapatkan pembagian IP sebagai berikut
| Subnet | Network ID  | Netmask         | Broadcast    |
| ------ | ----------- | --------------- | ------------ |
| A1     | 10.44.24.0  | 255.255.248.0   | 10.44.31.255 |
| A2     | 10.44.0.64  | 255.255.255.224 | 10.44.0.95   |
| A3     | 10.44.1.0   | 255.255.255.0   | 10.44.1.255  |
| A4     | 10.44.8.0   | 255.255.252.0   | 10.44.11.255 |
| A5     | 10.44.0.0   | 255.255.255.252 | 10.44.0.3    |
| A6     | 10.44.0.4   | 255.255.255.252 | 10.44.0.7    |
| A7     | 10.44.0.8   | 255.255.255.252 | 10.44.0.11   |
| A8     | 10.44.0.12  | 255.255.255.252 | 10.44.0.15   |
| A9     | 10.44.0.16  | 255.255.255.252 | 10.44.0.19   |
| A10    | 10.44.0.40  | 255.255.255.248 | 10.44.0.47   |
| A11    | 10.44.0.20  | 255.255.255.252 | 10.44.0.23   |
| A12    | 10.44.0.24  | 255.255.255.252 | 10.44.0.27   |
| A13    | 10.44.0.48  | 255.255.255.248 | 10.44.0.55   |
| A14    | 10.44.0.128 | 255.255.255.192 | 10.44.0.191  |
| A15    | 10.44.0.28  | 255.255.255.252 | 10.44.0.31   |
| A16    | 10.44.0.32  | 255.255.255.252 | 10.44.0.35   |
| A17    | 10.44.0.36  | 255.255.255.252 | 10.44.0.39   |
| A18    | 10.44.12.0  | 255.255.252.0   | 10.44.15.255 |
| A19    | 10.44.16.0  | 255.255.252.0   | 10.44.19.255 |
| A20    | 10.44.4.0   | 255.255.254.0   | 10.44.5.255  |
| A21    | 10.44.2.0   | 255.255.255.0   | 10.44.2.255  |

4. Setup GNS3
   
Setelah pembagian IP sudah siap, kita dapat melakukan konfigurasi pada GNS3. 

Pertama, kita membuat topologi pada GNS3

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/801c7aad-8e70-43a9-9908-15effe861f60)

Dengan pembagian IP subnet yang sudah dilakukan, kita dapat melakukan assign IP pada interface (Network Configuration) sesuai pada pembagian di atas

Aura
```
auto eth0
iface eth0 inet dhcp

# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.0.13
	netmask 255.255.255.252

# Static config for eth2
auto eth2
iface eth2 inet static
	address 10.44.0.9
	netmask 255.255.255.252

# Static config for eth3
auto eth3
iface eth3 inet static
	address 10.44.0.21
	netmask 255.255.255.252
```

Frieren
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.10
	netmask 255.255.255.252
	gateway 10.44.0.9

# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.0.5
	netmask 255.255.255.252

# Static config for eth2
auto eth2
iface eth2 inet static
	address 10.44.0.65
	netmask 255.255.255.224
```

Flamme
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.6
	netmask 255.255.255.252
	gateway 10.44.0.5

# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.0.1
	netmask 255.255.255.252

# Static config for eth2
auto eth2
iface eth2 inet static
	address 10.44.0.17
	netmask 255.255.255.252

# Static config for eth3
auto eth3
iface eth3 inet static
	address 10.44.8.1
	netmask 255.255.252.0
```

LakeKorridor
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.66
	netmask 255.255.255.224
	gateway 10.44.0.65
```

Fern
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.2
	netmask 255.255.255.252
	gateway 10.44.0.1


# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.24.1
	netmask 255.255.248.0
```

Himmel
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.18
	netmask 255.255.255.252
	gateway 10.44.0.17


# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.0.49
	netmask 255.255.255.248
```

LaubHills
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.24.2
	netmask 255.255.248.0
	gateway 10.44.24.1
```

AppetitRegion
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.24.3
	netmask 255.255.248.0
	gateway 10.44.24.1
```

RohrRoad
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.8.2
	netmask 255.255.252.0
	gateway 10.44.8.1
```

SchwerMountains
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.50
	netmask 255.255.255.248
	gateway 10.44.0.49
```

Denken
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.14
	netmask 255.255.255.252
	gateway 10.44.0.13


# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.1.1
	netmask 255.255.255.0
```

RoyalCapital
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.1.2
	netmask 255.255.255.0
	gateway 10.44.1.1
```

WilleRegion
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.1.3
	netmask 255.255.255.0
	gateway 10.44.1.1
```

Eisen
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.22
	netmask 255.255.255.252
	gateway 10.44.0.21


# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.0.33
	netmask 255.255.255.252

# Static config for eth2
auto eth2
iface eth2 inet static
	address 10.44.0.37
	netmask 255.255.255.252

# Static config for eth3
auto eth3
iface eth3 inet static
	address 10.44.0.25
	netmask 255.255.255.252

# Static config for eth4
auto eth4
iface eth4 inet static
	address 10.44.0.41
	netmask 255.255.255.248
```

Richter
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.42
	netmask 255.255.255.248
	gateway 10.44.0.41
```

Revolte
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.43
	netmask 255.255.255.248
	gateway 10.44.0.41
```

Stark
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.26
	netmask 255.255.255.252
	gateway 10.44.0.25
```

Linie
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.34
	netmask 255.255.255.252
	gateway 10.44.0.33


# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.0.29
	netmask 255.255.255.252

# Static config for eth2
auto eth2
iface eth2 inet static
	address 10.44.4.1
	netmask 255.255.254.0
```

GranzChannel
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.4.2
	netmask 255.255.254.0
	gateway 10.44.4.1
```

Lawine
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.30
	netmask 255.255.255.252
	gateway 10.44.0.29

# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.0.129
	netmask 255.255.255.192
```

BredtRegion
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.131
	netmask 255.255.255.192
	gateway 10.44.0.129
```

Heiter
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.130
	netmask 255.255.255.192
	gateway 10.44.0.129

# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.16.1
	netmask 255.255.252.0
```

Sein
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.16.2
	netmask 255.255.252.0
	gateway 10.44.16.1
```

RiegelCanyon
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.16.3
	netmask 255.255.252.0
	gateway 10.44.16.1
```

Lugner
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.0.38
	netmask 255.255.255.252
	gateway 10.44.0.37

# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.44.12.1
	netmask 255.255.252.0

# Static config for eth2
auto eth2
iface eth2 inet static
	address 10.44.2.1
	netmask 255.255.255.0
```

TurkRegion
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 10.44.12.2
	netmask 255.255.252.0
	gateway 10.44.12.1
```

GrobeForest
```
auto eth0
iface eth0 inet static
	address 10.44.2.2
	netmask 255.255.255.0
    	gateway 10.44.2.1
```

5. Routing
   
Routing dilakukan agar router dapat mengenal NID-NID melalui tetangga routernya. Berikut merupakan konfigurasi routingnya

Aura
```
route add -net 10.44.24.0 netmask 255.255.248.0 gw 10.44.0.10
route add -net 10.44.0.64 netmask 255.255.255.224 gw 10.44.0.10
route add -net 10.44.8.0 netmask 255.255.252.0 gw 10.44.0.10
route add -net 10.44.0.48 netmask 255.255.255.248 gw 10.44.0.10
route add -net 10.44.0.0 netmask 255.255.255.252 gw 10.44.0.10
route add -net 10.44.0.4 netmask 255.255.255.252 gw 10.44.0.10
route add -net 10.44.0.16 netmask 255.255.255.252 gw 10.44.0.10
route add -net 10.44.1.0 netmask 255.255.255.0 gw 10.44.0.14
route add -net 10.44.0.40 netmask 255.255.255.248 gw 10.44.0.22
route add -net 10.44.0.24 netmask 255.255.255.252 gw 10.44.0.22
route add -net 10.44.16.0 netmask 255.255.252.0 gw 10.44.0.22
route add -net 10.44.0.128 netmask 255.255.255.192 gw 10.44.0.22
route add -net 10.44.0.28 netmask 255.255.255.252 gw 10.44.0.22
route add -net 10.44.0.32 netmask 255.255.255.252 gw 10.44.0.22
route add -net 10.44.4.0 netmask 255.255.254.0 gw 10.44.0.22
route add -net 10.44.0.36 netmask 255.255.255.252 gw 10.44.0.22
route add -net 10.44.12.0 netmask 255.255.252.0 gw 10.44.0.22
route add -net 10.44.2.0 netmask 255.255.255.0 gw 10.44.0.22
```

Frieren
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.44.0.9
route add -net 10.44.0.0 netmask 255.255.255.252 gw 10.44.0.6
route add -net 10.44.0.16 netmask 255.255.255.252 gw 10.44.0.6
route add -net 10.44.24.0 netmask 255.255.248.0 gw 10.44.0.6
route add -net 10.44.8.0 netmask 255.255.252.0 gw 10.44.0.6
route add -net 10.44.0.48 netmask 255.255.255.248 gw 10.44.0.6
```

Flamme
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.44.0.5
route add -net 10.44.24.0 netmask 255.255.248.0 gw 10.44.0.2
route add -net 10.44.0.48 netmask 255.255.255.248 gw 10.44.0.18
```

Fern
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.44.0.1
```

Himmel
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.44.0.17
```

Denken
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.44.0.13
```

Eisen
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.44.0.21
route add -net 10.44.16.0 netmask 255.255.252.0 gw 10.44.0.34
route add -net 10.44.0.128 netmask 255.255.255.192 gw 10.44.0.34
route add -net 10.44.0.28 netmask 255.255.255.252 gw 10.44.0.34
route add -net 10.44.4.0 netmask 255.255.254.0 gw 10.44.0.34
route add -net 10.44.12.0 netmask 255.255.252.0 gw 10.44.0.38
route add -net 10.44.2.0 netmask 255.255.255.0 gw 10.44.0.38
```

Lugner
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.44.0.37
```

Linie
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.44.0.33
route add -net 10.44.0.128 netmask 255.255.255.192 gw 10.44.0.30
route add -net 10.44.16.0 netmask 255.255.252.0 gw 10.44.0.30
```

Lawien
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.44.0.29
route add -net 10.44.16.0 netmask 255.255.252.0 gw 10.44.0.130
```

Heiter
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.44.0.129
```

### Result

Testing dilakukan dengan melakukan ping ke IP tujuan. Berikut beberapa testing yang dilakukan

- AppetitRegion(625 Host) ping ke GranzChannel(254 Host)
  
![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/b6073579-2588-498c-be2e-2817150bd696)

- RiegelCanyon(510 Host) ping ke Denken

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/d2fbb2c5-94d5-4701-a676-3bc5972af3cf)

- Fern ping ke TurkRegion(1000host)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/518a07d5-e725-4e0c-bf1a-4c77d26789f9)

- Himmel ping ke Linie
  
![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/52c513de-d305-47a9-805f-65248715a955)

- RoyalCapital(63 Host) ping ke Sein
  
![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/af0bab77-d09e-45c5-bb6f-388af7f6fbaf)

- Sein ping ke Ricther
  
![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/41823ba3-d0c1-4063-8b25-6872b70d8bd9)


- Heiter ping ke Stark
  
![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/2781bcaa-f9be-4268-875f-b190a7da3a67)

https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/8ae7dff7-5d16-4d8e-8028-6cb31d32567f

## CIDR

CIDR, atau Classless Inter-Domain Routing, adalah metode yang digunakan dalam penanganan alamat IP untuk meningkatkan efisiensi alokasi ruang alamat dan rute di Internet. Sistem tradisional pengalamatan IP mengandalkan kelas, seperti Kelas A, B, dan C, yang seringkali menyebabkan penggunaan ruang alamat yang tidak efisien. CIDR, diperkenalkan pada tahun 1990-an, memungkinkan pendekatan yang lebih fleksibel dan scalable. Dalam CIDR, alamat IP tidak lagi terikat secara ketat pada kelas yang telah ditentukan sebelumnya; sebaliknya, notasi panjang awalan digunakan untuk menunjukkan jumlah bit yang signifikan dalam bagian jaringan alamat. Hal ini memungkinkan alokasi alamat IP yang lebih terperinci, mengurangi pemborosan alamat dan memudahkan alokasi berdasarkan kebutuhan jaringan yang sebenarnya.

### Penggabungan Subnet

Inilah pengaturan subnet awal yang akan kita gunakan untuk penggabungan subnet.

##### Kondisi Subnet Awal :

![subnet](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/90879937/bf812727-9c59-422d-ab9d-25919d703029)

| Nama Subnet | Rute                                            | Jumlah IP | Netmask |
| ----------- | ----------------------------------------------- | --------- | ------- |
| A1          | Fern-Switch4-LaubHills-Switch4-AppetitRegion    | 1023      | /21     |
| A2          | Frieren-Switch3-LakeKorridor                    | 25        | /27     |
| A3          | Denken-Switch2-RoyalCapital-Switch2-WilleRegion | 127       | /24     |
| A4          | Flamme-Switch5-RohrRoad                         | 1001      | /22     |
| A5          | Flamme-Fern                                     | 2         | /30     |
| A6          | Frieren-Flamme                                  | 2         | /30     |
| A7          | Aura-Frieren                                    | 2         | /30     |
| A8          | Aura-Denken                                     | 2         | /30     |
| A9          | Flamme-Himmel                                   | 2         | /30     |
| A10         | Eisen-Switch1-Richter-Switch1-Revolte           | 3         | /29     |
| A11         | Aura-Eisen                                      | 2         | /30     |
| A12         | Eisen-Switch0-Stark                             | 2         | /30     |
| A13         | Himmel-Switch6-SchwerMountains                  | 6         | /29     |
| A14         | Lawine-Switch7-BredRegion-Switch7-Heiter        | 31        | /26     |
| A15         | Linie-Lawine                                    | 2         | /30     |
| A16         | Eisen-Linie                                     | 2         | /30     |
| A17         | Eisen-Lugner                                    | 2         | /30     |
| A18         | Lugner-Switch10-TurkRegion                      | 1001      | /22     |
| A19         | Heiter-Switch8-Sein-Switch8-RiegelCanyon        | 512       | /22     |
| A20         | Linie-Switch11-GranzChannel                     | 255       | /23     |
| A21         | Lugner-Switch9-GrobeForest                      | 251       | /24     |
| Total       |                                                 | 4255      | /19     |

#### Posisi Awal Subnet (Dalam bentuk tree)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/3e888bcb-917a-4585-9515-401842001074)

#### Penggabungan Pertama

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/f03844d8-2f37-4dd7-86f5-0ae57aa26999)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/ec03903e-c6f8-479f-82fc-2613e73ee274)

#### Penggabungan Kedua

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/47f34fb4-7de9-4861-82a1-4c2d0cf11bf3)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/bd942b33-ffc1-4020-ad7d-45ff7077a3a2)

#### Penggabungan Ketiga

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/4e14102e-ad7e-43c6-9f6a-30a2fbe34a7d)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/388dbcf1-e078-4bb0-831b-4e2d179c8b36)

#### Penggabungan Keempat

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/3a8c886c-10db-4a51-971e-00cc27a12b34)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/bed2f84e-57bd-4728-be64-4aeff3f1c392)

#### Penggabungan Kelima

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/5f329d8d-3956-4116-bbfe-c996b41bf35d)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/7ead3e2a-4c67-45c2-999b-86745d4dafd3)

#### Penggabungan Keenam

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/92c4f435-0132-44c4-8543-05484a95165c)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/95064f7f-d913-43d5-b8fe-f1566a10cf9c)

#### Penggabungan Ketujuh

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/cca8d101-8ba8-4c54-8578-0c65d6ab22dd)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/41100885-5849-4ed1-a6a5-0c50be9e0b82)

#### Penggabungan Kedelapan

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/04c9d4b4-9fc9-4a5b-b69f-07f90054f104)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/d74c8932-00f7-4e56-b668-e2ac14f0f074)

### Tree

Setelah proses penggabungan subnet selesai, langkah selanjutnya adalah membagi alamat IP dengan menggunakan struktur pohon pada setiap kelompok yang telah dibentuk sebelumnya, seperti pada gambar di bawah ini.

![E15-CIDR-Tree](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/6620b4ce-b563-401c-a199-6e849e85257b)

### Pembagian IP

Inilah output dari pembagian alamat IP berdasarkan struktur pohon yang sudah dibuat sebelumnya.

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/0cce44e5-ac00-4821-91a3-469c4f8544ea)

### Routing 

#### Router Aura

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/3ab80a79-baa5-4990-905c-a4f4b7da3ecc)
![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/ea037059-7b8a-4215-9b06-bc8414ec68c2)
#### Router Frieren

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/0aa23fcb-4712-4368-b211-2b5ddaf68b4c)
#### Router Flamme

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/0af51465-eb3c-4857-910b-d8fcdd15e935)
#### Router Fern

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/45e6cdce-d4ec-4f85-9b31-62df1fd03e17)
#### Router Himmel

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/fab88fd4-8c14-4556-bd72-735cb11c95cd)
#### Router Denken

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/08fbb820-0120-40dd-85bb-d41d88eb66e3)
#### Router Eisen

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/5369fc72-9c14-40e6-a68a-d42767e05621)
#### Router Lugner

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/8b0bf0ca-2e92-4571-a266-91dc2b86a1e5)
#### Router Linie 

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/d7e1d164-3000-4985-984a-92b8d890913a)
#### Router Lawine

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/1ad94df3-0f35-4800-b67f-715c88bcba6a)
#### Router Heiter

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/abdb95eb-32b2-4c4d-aab8-81a543d6af85)

### Result 
![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/f7ffdc05-2d64-45bf-8268-6ca95a3cb3cb)
![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/48c9e649-c16a-43aa-a923-aeb43010eac6)

https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/568e4ac2-8a76-4880-9797-272b6c71bb10

