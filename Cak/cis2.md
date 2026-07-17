# CIS prat 2

# FILE SYSTEM KERNEL MODULE

## file system kernel modules

## patern

```
nvim /etc/modprobe.d/[namafile].conf
```

```
blacklist [nama_module]
install [nama_mdoule] /bin/false
```


### object

- cramfs
- freefs
- shfs
- hfsplus
- jfss2
- overlayfs
- squasfs
- udfkernel
- usbstorage
## example

```
nvim /etc/modprobe.d/cramfs.conf
```

```
blacklist cramfs
install crafs /bin/false
```

```
nvim /etc/modprobe.d/hfs.conf
```

```
blacklist hfs
install hfs /bin/false
```

### file system partition

## patern
semua partisi harus terpisah


### object


| partition      | option              |
| -------------- | ------------------- |
| /tmp           | nodev,nosuid,noexec |
| /var           | nodev,nosuid        |
| /var/log       | nodev,nosuid,noexec |
| /var/log/audit | nodev,nosuid,noexec |
| /var/tmp       | nodev,nosuid,noexec |
| /home          | nodev,nosuid        |


### validation

```
lsblk
```

```

    ├─base-root 254:1    0    15G  0 lvm   /
    ├─base-home 254:2    0    15G  0 lvm   /home
    ├─base-main 254:3    0   150G  0 lvm   /home/adzani
    ├─base-proc 254:4    0   512M  0 lvm   /var/lib/virtqemu
    ├─base-vars 254:5    0     5G  0 lvm   /var
    ├─base-vpac 254:6    0     5G  0 lvm   /var/cache/pacman
    ├─base-flat 254:7    0    20G  0 lvm   /var/lib/flatpak
    ├─base-vlog 254:8    0     1G  0 lvm   /var/log
    ├─base-vaud 254:9    0   512M  0 lvm   /var/log/audit
    ├─base-vtmp 254:10   0     2G  0 lvm   /var/tmp
    ├─base-swap 254:11   0     4G  0 lvm   [SWAP]
    └─base-temp 254:12   0     2G  0 lvm   /tmp
```

# Services 

## patern

```
systemctl mask [service_name]
```

### object

- autofs
- avahi
- dhcp
- dns
- dnsmasq
- ftp
- ldap
- massage access
- network file system
- nis server
- print server
- rpcbind
- rsync
- samba file server
- snmp
- tftp server
- web proxy server
- web server
- xinetd
- X window server
- mail transfer agent

## manual patern
```
firewall-cmd --list-all-zone
```

### object

| zone     | port | service                             | protocol |
| -------- | ---- | ----------------------------------- | -------- |
| pulic    |      | dhcpv6-client ssh                   |          |
| dmz      |      | ssh                                 |          |
| block    |      |                                     |          |
| drop     |      |                                     |          |
| external |      | ssh                                 |          |
| home     |      | dhcpv6-client mdns samba-client ssh |          |
| internal |      | dhcpv6-client mdns samba-client ssh |          |
| trusted  |      |                                     |          |
| work     |      | dhcpv6-client ssh                   |          |
|          |      |                                     |          |
### rumus untuk port

```
firewall-cmd --zone=[nama_zone] --remove-port=[port_number]/[protocol] --permenanet
```

```
firewall-cmd --reload
```

### rumus untuk service

```
firewall-cmd --zone=[nama_zone] --remove-servcice=[namservice] --permenanet
```


**rumus untuk protocol**

```
firewall-cmd --zone=[nama_zone] --remove-protocol=[protocol_name] --permenanet
```


```
nvim /etc/modprobe.d/hfs.conf
```

```
blacklist hfs
install hfs /bin/false
```

## service

- autofs
- avahi-daemon.socket
- avahi-daemon.service
- cockpit.service
- kea-dhcp-ddns.services
- kea-dhcp4.service
- kea-dhcp6.service

Pattern
```
systemctl stop <nama service>.service
```

```
systemctl mask <nama service>
```

## client services

- ftp 
- ldap
- telnet
- tftp

### Pattern
```
pacman -Rs <nama service>
```

## synchronize 
```bash
sudo timedatectl set-ntp true
```

```bash
sudo timedatectl set-timezone Asia/Jakarta
```

```bash
sudo timedatectl
```

# Network
### Configure Network Device

```bash
nvim /etc/sysctl.d/40-ipv6.conf
```

```bash
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
```

```bash
sudo sysctl --system
```

### network methods 2

```
pacman -Rs iwd impala wpa_suplicant
```

## bluetooth
```
pacman -Q bluez
```

> _output_-nya `error: package 'bluez' was not found`, berarti sistemmu sudah aman (PASS).

> _output_-nya menampilkan versi `bluez` (misal: `bluez 5.72-2`), berarti paket terpasang dan kamu harus mengecek status layanannya.


### Cek apakah layanannya aktif:
```bash
systemctl is-enabled bluetooth.service 2>/dev/null
```

```bash
systemctl is-active bluetooth.service 2>/dev/null
```

### atau jika gamau ribet 

```
sudo pacman -Rns bluez
```

### network module
## patern

```
nvim /etc/modprobe.d/[namafile].conf
```

```
blacklist [nama_module]
install [nama_mdoule] /bin/false
```


### object

- ddcp
- tipc
- rds
- sctp
## example

```
nvim /etc/modprobe.d/vader.conf
```

```
blacklist ddcp
install ddcp /bin/false
```
