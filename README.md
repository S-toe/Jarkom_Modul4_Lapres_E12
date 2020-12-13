# Jarkom_Modul4_Lapres_E12
- Restu Agung Parama - 05111840000123

![Soal Shift Modul 4 svg](https://user-images.githubusercontent.com/58405725/102011866-9aa87300-3d79-11eb-90ab-3c03c240e22a.png)


## UML-VLSM
Untuk tree VLSM yg dibuat dapat dilihat di link berikut:

https://gitmind.com/app/doc/7271300301

Tabel berikut menampilkan subnet dan jumlah IP untuk mendapatkan netmask tiap subnet:

| Subnet        | Jumlah IP     | Netmask |
| ------------- |:-------------:| -------:|
| A1            | 1001          | /22     |
| A2            | 2             | /30     |
| A3            | 2             | /30     |
| A4            | 101           | /25     |
| A5            | 701           | /22     |
| A6            | 2021          | /21     |
| A7            | 2             | /30     |
| A8            | 502           | /23     |
| A9            | 13            | /28     |
| A10           | 521           | /22     |
| A11           | 2             | /30     |
| A12           | 252           | /24     |
| A13           | 721           | /22     |
| TOTAL         | 5841          | /19     |

Dalam perhitungan NID dan Broadcast, saya menghitung ip pertama dan terakhir setiap subnet berdasarkan tabel di modul. Dari hasil perhitungan didapatlah: <br>
(cara membaca)<br>
nama subnet<br>
NID<br>
Netmask<br>
IP Broadcast<br>

```
A1
192.168.4.0
255.255.252.0
192.168.7.255
A2
192.168.0.0
255.255.255.252
192.168.0.3
A3
192.168.0.4
255.255.255.252
192.168.0.7
A4
192.168.0.128
255.255.255.128
192.168.0.255
A5
192.168.8.0
255.255.252.0
192.168.11.255
A6
192.168.24.0
255.255.248.0
192.168.31.255
A7
192.168.0.8
255.255.255.252
192.168.0.11
A8
192.168.2.0
255.255.254.0
192.168.3.255
A9
192.168.0.16
255.255.255.240
192.168.0.31
A10
192.168.12.0
255.255.252.0
192.168.15.255
A11
192.168.0.12
255.255.255.252
192.168.0.15
A12
192.168.1.0
255.255.255.0
192.168.1.255
A13
192.168.16.0
255.255.252.0
192.168.19.255
```
## CPT-CIDR

Untuk tree CIDR yg dibuat dapat dilihat di link berikut:

https://gitmind.com/app/doc/7271300301

Dari hasil perhitungan NID dan Broadcast, didapatlah:
```
A1
192.168.192.0
255.255.252.0
192.168.195.255
A2
192.168.67.0
255.255.255.252
192.168.67.3
A3
192.168.16.0
255.255.255.252
192.168.16.3
A4
192.168.8.0
255.255.255.128
192.168.8.127
A5
192.168.32.0
255.255.252.0
192.168.35.255
A6
192.168.0.0
255.255.248.0
192.168.7.255
A7
192.168.160.0
255.255.255.252
192.168.160.3
A8
192.168.144.0
255.255.254.0
192.168.145.255
A9
192.168.146.0
255.255.255.240
192.168.146.15
A10
192.168.148.0
255.255.252.0
192.168.151.255
A11
192.168.136.0
255.255.255.252
192.168.136.3
A12
192.168.132.0
255.255.255.0
192.168.132.255
A13
192.168.128.0
255.255.252.0
192.168.131.255
```

Untuk implementasi pada UML maka dibuatkan topologi dengan script sebagai berikut.

```
# Switch
uml_switch -unix switch0 > /dev/null < /dev/null &
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch4 > /dev/null < /dev/null &
uml_switch -unix switch13 > /dev/null < /dev/null &
uml_switch -unix switch15 > /dev/null < /dev/null &
uml_switch -unix switch16 > /dev/null < /dev/null &
uml_switch -unix switch17 > /dev/null < /dev/null &
uml_switch -unix switch18 > /dev/null < /dev/null &
uml_switch -unix switch19 > /dev/null < /dev/null &
uml_switch -unix switch20 > /dev/null < /dev/null &
uml_switch -unix switch21 > /dev/null < /dev/null &
uml_switch -unix switch22 > /dev/null < /dev/null &
uml_switch -unix switch25 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.70.53 eth1=daemon,,,switch1 eth2=daemon,,,switch0 eth3=daemon,,,switch3 eth4=daemon,,,switch13 mem=64M &
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch2 eth1=daemon,,,switch19 eth2=daemon,,,switch0 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch15 eth1=daemon,,,switch16 eth2=daemon,,,switch2 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch3 eth1=daemon,,,switch4 eth2=daemon,,,switch21 eth3=daemon,,,switch22 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch22 eth1=daemon,,,switch25 mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch4 eth1=daemon,,,switch17 eth2=daemon,,,switch18 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch17 eth1=daemon,,,switch20 mem=64M &

# Server
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch13 mem=64M &
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch18 mem=64M &

# Klien
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch15 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch16 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch16 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch19 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch22 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch25 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch21 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch20 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch17 mem=64M &

```

Pada file ```/etc/sysctl.conf``` di setiap router yaitu pada UML **SURABAYA**, **PASURUAN**, **PROBOLINGGO**, **BATU**, **KEDIRI**, **MADIUN**, **BLITAR** dibuat agar dapat melakukan packet forwarding IPv4 dengan melakukan *uncomment* pada ```net.ipv4.forward=1``` sebagai berikut.

![image](https://user-images.githubusercontent.com/57692117/100540404-cd2d7880-326f-11eb-96bd-fa4126ab3242.png)

Untuk melakukan pembagian IP pada setiap Host maka dilakukan konfigurasi pada `/etc/network/interfaces` tiap host dan routing untuk setiap router sebagai berikut. (saya menyimpan routing di interface juga agar ketika menyalakan uml tidak perlu routing kembali)

- SURABAYA
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.70.54
netmask 255.255.255.252
gateway 10.151.70.53

auto eth1
iface eth1 inet static
address 192.168.4.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.168.0.1
netmask 255.255.255.252

auto eth3
iface eth3 inet static
address 192.168.0.9
netmask 255.255.255.252

auto eth4
iface eth4 inet static
address 10.151.71.105
netmask 255.255.255.252

up ip route add 192.168.0.4/30 via 192.168.0.2 dev eth2
up ip route add 192.168.0.128/25 via 192.168.0.2 dev eth2
up ip route add 192.168.8.0/22 via 192.168.0.2 dev eth2
up ip route add 192.168.24.0/21 via 192.168.0.2 dev eth2
up ip route add 192.168.2.0/23 via 192.168.0.10 dev eth3
up ip route add 192.168.0.16/28 via 192.168.0.10 dev eth3
up ip route add 192.168.12.0/22 via 192.168.0.10 dev eth3
up ip route add 192.168.0.12/30 via 192.168.0.10 dev eth3
up ip route add 192.168.1.0/24 via 192.168.0.10 dev eth3
up ip route add 192.168.16.0/22 via 192.168.0.10 dev eth3
up ip route add 10.151.71.108/30 via 192.168.0.10 dev eth3
up iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16

```
- PASURUAN
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.5
netmask 255.255.255.252

auto eth1
iface eth1 inet static
address 192.168.8.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.168.0.2
netmask 255.255.255.252

up ip route add 0.0.0.0/0 via 192.168.0.1 dev eth2
up ip route add 192.168.0.128/25 via 192.168.0.6 dev eth0
up ip route add 192.168.24.0/21 via 192.168.0.6 dev eth0

```
- PROBOLINGGO
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.129
netmask 255.255.255.128

auto eth1
iface eth1 inet static
address 192.168.24.1
netmask 255.255.248.0

auto eth2
iface eth2 inet static
address 192.168.0.6
netmask 255.255.255.252

up ip route add 0.0.0.0/0 via 192.168.0.5 dev eth2

```
- BATU
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.10
netmask 255.255.255.252

auto eth1
iface eth1 inet static
address 192.168.0.13
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.12.1
netmask 255.255.252.0

auto eth3
iface eth3 inet static
address 192.168.2.1
netmask 255.255.254.0

up ip route add 0.0.0.0/0 via 192.168.0.9 dev eth0
up ip route add 192.168.0.16/28 via 192.168.2.2 dev eth3
up ip route add 192.168.1.0/24 via 192.168.0.14 dev eth1
up ip route add 192.168.16.0/22 via 192.168.0.14 dev eth1
up ip route add 10.151.71.108/30 via 192.168.0.14 dev eth1

```
- KEDIRI
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.14
netmask 255.255.255.252

auto eth1
iface eth1 inet static
address 192.168.1.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 10.151.71.109
netmask 255.255.255.252

up ip route add 0.0.0.0/0 via 192.168.0.13 dev eth0
up ip route add 192.168.16.0/22 via 192.168.1.2 dev eth1

```
- MADIUN
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.2.2
netmask 255.255.254.0

auto eth1
iface eth1 inet static
address 192.168.0.17
netmask 255.255.255.240

up ip route add 0.0.0.0/0 via 192.168.2.1 dev eth0

```
- BLITAR
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.1.2
netmask 255.255.255.0

auto eth1
iface eth1 inet static
address 192.168.16.1
netmask 255.255.252.0

up ip route add 0.0.0.0/0 via 192.168.1.1 dev eth0
```
Untuk Server menggunakan IP dari DMZ sehingga konfigurasinya sebagai berikut.
- MALANG
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.71.110
netmask 255.255.255.252
gateway 10.151.71.109
```

- MOJOKERTO
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.71.106
netmask 255.255.255.252
gateway 10.151.71.105
```

Untuk client sebagai berikut.

- SAMPANG
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.2
netmask 255.255.252.0
gateway 192.168.4.1
```

- BONDOWOSO
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.130
netmask 255.255.255.128
gateway 192.168.0.129
```

- JEMBER
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.24.2
netmask 255.255.248.0
gateway 192.168.24.1
```

- BANYUWANGI
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.24.3
netmask 255.255.248.0
gateway 192.168.24.1
```

- SIDOARJO
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.8.2
netmask 255.255.252.0
gateway 192.168.8.1

```

- JOMBANG
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.2.3
netmask 255.255.254.0
gateway 192.168.2.1
```

- BOJONEGORO
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.18
netmask 255.255.255.240
gateway 192.168.0.17
```

- NGANJUK
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.12.2
netmask 255.255.252.0
gateway 192.168.12.1
```

- TULUNGAGUNG
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.252.0
gateway 192.168.16.1

```

- LUMAJANG
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.1.3
netmask 255.255.255.0
gateway 192.168.1.1
```
