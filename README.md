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
   
Setelah pembagian IP sudah siap, kita dapat melakukan konfigurasi pada GNS3
## CIDR
