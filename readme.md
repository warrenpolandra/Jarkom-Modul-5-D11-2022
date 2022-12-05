# Jarkom-Modul-5-D11-2022

## Kelompok D11:

- 5025201006 - Afira Rolobessy
- 5025201029 - Beryl
- 5025201233 - Warren Gerald Polandra

## Pembagian Tugas:

- Afira:
- Beryl: 
- Warren: 

## Topologi

![Topologi](https://cdn.discordapp.com/attachments/856609726225973278/1049247946559987743/Topologi.png)

## Keterangan Node:

- Eden adalah DNS Server
- WISE adalah DHCP Server
- Garden dan SSS adalah Web Server
- Jumlah Host pada Forger adalah 62 host
- Jumlah Host pada Desmond adalah 700 host
- Jumlah Host pada Blackbell adalah 255 host
- Jumlah Host pada Briar adalah 200 host

## Pembagian Subnet - VLSM

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

auto eth1
iface eth1 inet static
        address 192.190.0.1
        netmask 255.255.255.252

auto eth2
iface eth2 inet static
        address 192.190.0.5
        netmask 255.255.255.252
```

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
