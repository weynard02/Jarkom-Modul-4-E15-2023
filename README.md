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

Kemudian kita untuk mendapatkan pembagian IP, kita akan menggunakan dua metode tersebut

## VLSM
VLSM (Variable Length Subnet Masking) merupakan teknik di mana netmask akan diberikan sesuai kebutuhan jumlah alamat IP dari subnet tersebut. Jadi besar netmask disesuaikan dengan host yang membutuhkan alamat IP.

1. Melakukan pembagian rute
   
Sebelumnya, kita sudah melakukan pembagian rute dari topologi di atas. Kita mendapatkan total kebutuhan ada 4255 IP yang di mana netmask yang diperlukan adalah /19 (max = 8190)

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
	netmask 255.255.255.0
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
	address v
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
   
## CIDR

### Penggabungan IP

Inilah pengaturan awal yang akan kita gunakan untuk menyatukan alamat IP.
![topo](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/4e995f91-f509-4894-934e-60b2f03391be)

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

#### Posisi Awal (Dalam bentuk tree)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/c7fd1453-3d2b-474d-af55-274bb13a8a61)

#### Penggabungan Pertama

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/284c959c-416d-4ca8-a0e1-c22acb8fce49)

#### Penggabungan Kedua

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/6cecaa24-ce56-4ca9-95e5-9fa832b38025)

#### Penggabungan Ketiga

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/74aa1743-ae44-4f64-afe6-e9a96a4e3907)

#### Penggabungan Keempat

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/1fa2e84d-d13c-4ccf-816a-f84566b1680e)

#### Penggabungan Kelima

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/5e485a31-5d90-4617-b731-87839419dd3f)

#### Penggabungan Keenam

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/65069af3-3447-4440-b5eb-ccca62b59e77)

#### Penggabungan Ketujuh

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/c49db125-d246-4d1f-9dc4-90b75354f18c)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/6fbaef6a-89ac-4389-bb75-e03aa3cf859d)

![image](https://github.com/weynard02/Jarkom-Modul-4-E15-2023/assets/106955551/15b1fffc-a941-4021-b08c-b918214f8d45)
