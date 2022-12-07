# Jarkom-Modul-5-D11-2022

## Kelompok D11:

- 5025201006 - Afira Rolobessy
- 5025201029 - Beryl
- 5025201233 - Warren Gerald Polandra

## Pembagian Tugas:

- Afira: Topologi, DHCP (33.33%)
- Beryl: VLSM (33.33%)
- Warren: Firewall (33.33%)

## (A) Topologi

![Topologi](https://cdn.discordapp.com/attachments/856609726225973278/1049247946559987743/Topologi.png)

## Keterangan Node:

- Eden adalah DNS Server
- WISE adalah DHCP Server
- Garden dan SSS adalah Web Server
- Jumlah Host pada Forger adalah 62 host
- Jumlah Host pada Desmond adalah 700 host
- Jumlah Host pada Blackbell adalah 255 host
- Jumlah Host pada Briar adalah 200 host

## (B) Pembagian Subnet - VLSM

![Subnet VLSM](https://cdn.discordapp.com/attachments/856609726225973278/1049249641172062239/Subnet_VLSM.png)

## Penghitungan Jumlah Subnet

| No | Subnet | Jumlah IP | Netmask |
| :---: | :---: | :---: | :---: |
| 1 | A3 | 701 | /22 |
| 2 | A7 | 256 | /23 |
| 3 | A6 | 201 | /24 |
| 4 | A2 | 63 | /25 |
| 5 | A1 | 3 | /29 |
| 6 | A8 | 3 | /29 |
| 7 | A4 | 2 | /30 |
| 8 | A5 | 2 | /30 |
| Total | 8 | 1231 | /21 |

## VLSM Tree

![VLSM Tree](https://cdn.discordapp.com/attachments/856609726225973278/1049256468882395146/VLSM_Tree.png)

## Pembagian IP

| No | Subnet | Network ID | Subnet Mask | Wildcard | IP Broadcast | 
| :---: | :---: | :---: | :---: | :---: | :---: |
| 1 | A3 | 192.190.4.0 | 255.255.252.0  | 0.0.3.255 | 192.190.7.255 |
| 2 | A7 | 192.190.2.0 | 255.255.254.0 | 0.0.1.255 | 192.190.3.255 |
| 3 | A6 | 192.190.1.0 | 255.255.255.0 | 0.0.0.255 | 192.190.1.255 |
| 4 | A2 | 192.190.0.128 | 255.255.255.128 | 0.0.0.127 | 192.190.0.255 |
| 5 | A1 | 192.190.0.16 | 255.255.255.248 | 0.0.0.7 | 192.190.0.23 |
| 6 | A8 | 192.190.0.24 | 255.255.255.248 | 0.0.0.7 | 192.190.0.31 |
| 7 | A4 | 192.190.0.0 | 255.255.255.252 | 0.0.0.3 | 192.190.0.3 |
| 8 | A5 | 192.190.0.4 | 255.255.255.252 | 0.0.0.3 | 192.190.0.7 |

## Network Configuration

### Strix

```
auto eth0
iface eth0 inet dhcp
hwaddress ether 3a:20:6d:d7:5b:79

auto eth1
iface eth1 inet static
        address 192.190.0.1
        netmask 255.255.255.252

auto eth2
iface eth2 inet static
        address 192.190.0.5
        netmask 255.255.255.252
```
**Strix** menggunakan `hwaddress` agar bisa mendapatkan fixed address yang akan digunakan untuk konfigurasi iptables nantinya. Fixed address dari **Strix** adalah `192.168.122.227`

### Westalis

```
auto eth0
iface eth0 inet static
        address 192.190.0.2
        netmask 255.255.255.252
        gateway 192.190.0.1

auto eth1
iface eth1 inet static
        address 192.190.0.17
        netmask 255.255.255.248

auto eth2
iface eth2 inet static
        address 192.190.0.129
        netmask 255.255.255.128

auto eth3
iface eth3 inet static
        address 192.190.4.1
        netmask 255.255.252.0
```

### Ostania

```
auto eth0
iface eth0 inet static
        address 192.190.0.6
        netmask 255.255.255.252
        gateway 192.190.0.5

auto eth1
iface eth1 inet static
        address 192.190.1.1
        netmask 255.255.255.0

auto eth2
iface eth2 inet static
        address 192.190.0.25
        netmask 255.255.255.248

auto eth3
iface eth3 inet static
        address 192.190.2.1
        netmask 255.255.254.0
```

### Eden

```
auto eth0
iface eth0 inet static
        address 192.190.0.18
        netmask 255.255.255.248
        gateway 192.190.0.17
```

### WISE

```
auto eth0
iface eth0 inet static
        address 192.190.0.19
        netmask 255.255.255.248
        gateway 192.190.0.17
```

### SSS

```
auto eth0
iface eth0 inet static
        address 192.190.0.26
        netmask 255.255.255.248
        gateway 192.190.0.25
```

### Garden

```
auto eth0
iface eth0 inet static
        address 192.190.0.27
        netmask 255.255.255.248
        gateway 192.190.0.25
```

## (C) Routing

Pada Strix

```
route add -net 192.190.0.16 netmask 255.255.255.248 gw 192.190.0.2
route add -net 192.190.0.128 netmask 255.255.255.128 gw 192.190.0.2
route add -net 192.190.4.0 netmask 255.255.252.0 gw 192.190.0.2

route add -net 192.190.1.0 netmask 255.255.255.0 gw 192.190.0.6
route add -net 192.190.0.24 netmask 255.255.255.248 gw 192.190.0.6
route add -net 192.190.2.0 netmask 255.255.254.0 gw 192.190.0.6
```

## (D) DHCP

Pada **Forger**, **Desmond**, **Blackbell**, dan **Briar** dilakukan network configuration seperti berikut

```
auto eth0
iface eth0 inet dhcp
```

### DHCP Server

1. Pada **WISE** sebagai DHCP Server, dilakukan instalasi DHCP Server

```
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update
apt-get install isc-dhcp-server -y
```

2. Konfigurasi file `/etc/default/isc-dhcp-server` pada **WISE** sebagai DHCP Server

```
INTERFACES="eth0"
```

3. Konfigurasi file `/etc/dhcp/dhcpd.conf` pada **WISE** sebagai DHCP Server

```
# Forger (A2)
subnet 192.190.0.128 netmask 255.255.255.128 {
        range 192.190.0.130 192.190.0.254;
        option routers 192.190.0.129;
        option broadcast-address 192.190.0.255;
        option domain-name-servers 192.190.0.18;
        default-lease-time 600;
        max-lease-time 7200;
}

# Desmond (A3)
subnet 192.190.4.0 netmask 255.255.252.0 {
        range 192.190.4.2 192.190.7.254;
        option routers 192.190.4.1;
        option broadcast-address 192.190.7.255;
        option domain-name-servers 192.190.0.18;
        default-lease-time 600;
        max-lease-time 7200;
}

# Briar (A6)
subnet 192.190.1.0 netmask 255.255.255.0 {
        range 192.190.1.2 192.190.1.254;
        option routers 192.190.1.1;
        option broadcast-address 192.190.1.255;
        option domain-name-servers 192.190.0.18;
        default-lease-time 600;
        max-lease-time 7200;
}

# Blackbell (A7)
subnet 192.190.2.0 netmask 255.255.254.0 {
        range 192.190.2.2 192.190.3.254;
        option routers 192.190.2.1;
        option broadcast-address 192.190.3.255;
        option domain-name-servers 192.190.0.18;
        default-lease-time 600;
        max-lease-time 7200;
}

# WISE menuju Westalis (A1)
subnet 192.190.0.16 netmask 255.255.255.248 {
        option routers 192.200.0.17;
}
```

4. Menjalankan DHCP Server

```
service isc-dhcp-server start
```

### DHCP Relay

Dengan topologi yang ada, **Westalis** dan **Ostania** akan bekerja sebagai DHCP Relay

1. Pada **Westalis** dan **Ostania** sebagai DHCP Relay, dilakukan instalasi DHCP Relay

```
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update
apt-get install isc-dhcp-relay -y
```

2. Konfigurasi file `/etc/default/isc-dhcp-relay` pada **Westalis** dan **Ostania** sebagai DHCP Relay

```
SERVERS="192.190.0.19"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
```

### DNS Forwarder

Pada **Eden** sebagai DNS Server, dilakukan instalasi Bind9

```
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update
apt-get install bind9 -y

service bind9 start
```

Kemudian konfigurasi DNS Forwarder pada file `/etc/bind/named.conf.options`

```
options {
        directory \"/var/cache/bind\";

         forwarders {
                192.168.122.1;
         };

        allow-query{any;};
        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};
```

Setelah itu restart bind9 dengan `service bind9 restart`

### Testing

#### Forger

![DHCP Forger](https://cdn.discordapp.com/attachments/856609726225973278/1049322570123579422/image.png)

#### Desmond

![DHCP Desmond](https://cdn.discordapp.com/attachments/856609726225973278/1049322771928330340/image.png)

#### Briar

![DHCP Briar](https://cdn.discordapp.com/attachments/856609726225973278/1049322929411866624/image.png)

#### Blackbell

![DHCP Blackbell](https://cdn.discordapp.com/attachments/856609726225973278/1049323163168813066/image.png)

## (1) iptables pada **Strix** tanpa `MASQUERADE`

`MASQUERADE` dapat diganti dengan `SNAT` dengan tambahan `--to-source` dengan IP dari Strix sendiri yaitu `192.168.122.227`, syntaxnya adalah

```
iptables -t nat -A POSTROUTING -s 192.190.0.0/21 -o eth0 -j SNAT --to-source 192.168.122.227
```

### Testing

#### Pada **Strix**

![Ping Google Strix](https://cdn.discordapp.com/attachments/856609726225973278/1049325340335546389/image.png)

#### Pada **Westalis**

![Ping Google Westalis](https://cdn.discordapp.com/attachments/856609726225973278/1049325595240185899/image.png)

#### Pada **WISE**

![Ping Google WISE](https://cdn.discordapp.com/attachments/856609726225973278/1049325941039562752/image.png)

#### Pada **Briar**

![Ping Google Briar](https://cdn.discordapp.com/attachments/856609726225973278/1049326318887649411/image.png)


## (2) Drop semua TCP dan UDP pada DHCP Server

Pada **Strix** dilakukan konfigurasi firewall sebagai berikut

```
iptables -A FORWARD -p tcp -d 192.190.0.19 -i eth0 -j DROP # Drop semua TCP
iptables -A FORWARD -p udp -d 192.190.0.19 -i eth0 -j DROP # Drop semua UDP
```

iptables di atas akan melalukan drop pada semua TCP dan UDP dengan tujuan **WISE** yang memiliki IP address `192.190.0.19`

### Testing

#### Ping google.com pada WISE setelah iptables

![Ping Firewall](https://cdn.discordapp.com/attachments/856609726225973278/1049355613160882186/image.png)

#### Netcat **WISE** dengan **Strix** menggunakan port 18

![Netcat Strix](https://cdn.discordapp.com/attachments/856609726225973278/1049356285952393286/image.png)

![Netcat WISE](https://cdn.discordapp.com/attachments/856609726225973278/1049356571903283330/image.png)

## (3) Membatasi DHCP dan DNS Server hanya boleh menerima maksimal 2 koneksi ICMP secara bersamaan

Limit koneksi ICMP dengan iptables pada **WISE** sebagai DHCP Server dan **Eden** sebagai DNS Server

```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 2 --connlimit-mask 0 -j DROP
```

### Testing ping Eden (192.190.0.18) sebagai DNS Server dengan 3 client

![Ping Forger](https://cdn.discordapp.com/attachments/856609726225973278/1049358966699860019/image.png)

![Ping Desmond](https://cdn.discordapp.com/attachments/856609726225973278/1049359050351050812/image.png)

![Ping Briar](https://cdn.discordapp.com/attachments/856609726225973278/1049359380866416730/image.png)


## (4) Akses menuju Web Server hanya diperbolehkan disaat jam kerja yaitu Senin sampai Jumat pada pukul 07.00 - 16.00

Pada **Garden** dan **SSS** sebagai Web Server, dibuat firewall sebagai berikut

```
iptables -A INPUT -m time --timestart 07:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j REJECT
```

### Testing

Ping **Garden** (192.190.0.27) pada jam kerja

![Ping Jam Kerja](https://cdn.discordapp.com/attachments/856609726225973278/1049978185523134525/image.png)

Ping **Garden** (192.190.0.27) pada hari libur

![Ping Hari Libur](https://cdn.discordapp.com/attachments/856609726225973278/1049978394185576488/image.png)

## (5) Setiap request dari client yang mengakses Garden dengan port 80 akan didistribusikan secara bergantian pada SSS dan Garden secara berurutan dan request dari client yang mengakses SSS dengan port 443 akan didistribusikan secara bergantian pada Garden dan SSS secara berurutan

Pada **Ostania** dilakukan konfigurasi iptables sebagai berikut

```
iptables -t nat -A PREROUTING -p tcp -d 192.190.0.27 --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.190.0.26:80
```

## (6) Logging paket yang di-drop dengan standard syslog level

```
iptables -N LOGGING
iptables -A INPUT -j LOGGING
iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
iptables -A LOGGING -j DROP
```
