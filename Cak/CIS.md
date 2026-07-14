# CIS

# 1. Initial setup
## 1.1.1 configure file system kernel module
### pattern 
```
blacklist [nama_module]
install [nama_module] /bin/false
```
### object

| no  | object |
| -----|-------|
| 1     |  carmfs |
| 2     |  freevxfs |  
| 3     |  hfs     |
| 4     |  hfsplus |
| 5     |  jffs2   |
| 6     | overlay  |
| 7     | squashfs   |
| 8     | udf      |
| 9     | firewire-core |
| 10    | usb storage |

## 1.1.2 file system partition
## pattern 
```
[device] [mount_target] [mount_option] 0 0
```
## object
| no  | mount path | mount option | 
| ---------|-----------|----------|
| 1     |   /tmp     | nodev,nosuid,noexec |
| 2     |   /dev/shm |  nodev,nosuid,noexec |
| 3     |   /home    | nodev,nosuid |
| 4     |   /var     | nodev,nosuid |
| 5     | /var/tmp   | nodev,nosuid,noexec |
| 6     | /var/log   | nodev,nosuid,noexec |
| 7     | /var/log/audit | nodev,nosuid,noexec |
```
 jadinya itu /home dan /var -> nodev,nosuid
 /tmp /dev/shm /var/tmp /var/log /var/log/audit -> nodev,nosuid,noexec
```
## 1.2 pattern package management
> regulaly update arch linux
```
pacman -Syu
```
## 1.5 additional hardening 
| nama  | path | value |
| ------|------|-------|
| core  | /etc/security/limits.d/60-limits.conf | * hard core 0 |
| fs.protected_hardlinks | /etc/sysctl.d/fs-prottected.conf | fs.protected_hardlinks = 1 |
| fs.protected_symlinks | /etc/sysctl.d/fs-symlink.conf | fs.protected_symlinks = 1 |
| fs.suid_dumpable | /etc/sysctl.d/fs-dumpable.conf | fs.suid_dumpable = 0 |
| kernel.dmesg_restrict | /etc/sysctl.d/fs-dmesg.conf | kernel.dmesg_restrict = 1 |
| kernel.kptr_restrict | ... | ... |
| kernel.yama.ptrace_scope | .. | ... |
| kernel.randomize_va_space | ... | ... |
| systemd-coredump ProcessSizeMax | ... | ... |
| systemd-coredump Storage | ... | ... |

# 2. Services
## pattern
```
systemctl stop [nama_service]
systemctl mask [nama_service]
```
## object
| no  | service |
| ----|---------|
| 1 | autofs.service |
| 2 | avahi-daemon.socket |
| 3 | avahi-daemon.service |
| 4 | cockpit.socket |
| 5 | cockpit.service |
| 6 | kea-dhcp-ddns.service |
| 7 | kea-dhcp4.service |
| 8 | kea-dhcp6.service |

## 2.2 configure client service
```
pacman -Rs ftp ldap telnet tftp
```
# 3. Network
## 3.2 configur network kernel module 
## patterrn
```
blacklist [nama_module]
install [nama_module] /bin/false
```
## object
| no  | object |
| ----|--------|
| 1| atm |
| 2 | can |
| 3 | dccp |
|4 | tipc |
| 5 | rds |
| 6 | sctp |
## 3.3 Network Kernel Parameters
## 3.3.1 IPv4
| name  | path | value |
| ------|------|-------|
| net.ipv4.ip_forward | /etc/sysctl.d/ipv4.ip_forward.conf  | net.ipv4.ip_forward = 0 |
| net.ipv4.conf.all.forwarding | /etc/sysctl.d/ipv4.conf.all.forwarding.conf | net.ipv4.conf.all.forwarding = 0 | 
| net.ipv4.conf.default.forwarding | /etc/sysctl.d/ | net.ipv4.conf.default.forwarding = 0 |
| net.ipv4.conf.all.accept_redirect | /etc/sysctl.d/ | net.ipv4.conf.all.accept_redirect = 0 |

## 3.3.2 ipv6
| name  | path | value |
| ------|------|-------|

# 4. Firewall
```
pacman -S firewalld
```
```
pacman -S nftables
```

```
systemctl enable firewalld
```
# 5. Acecss
| access  | alphabet | numerik |
| ------|------|-------|
| read | r | 4 |
| write | w | 2 |
| execution | x | 1 |
> contohnyaa
>- chmod 0600 /etc/ssh/sshd_config
>- agoy.txt
>- chmod 2 agoy.txt
>- pemilik file = write and read
>- group 4 = write
>- other = write


## pattern
```
chown [user]:[group] [file_path]
chmod [modoption] [file_path]
```
## object 
| user  | group | modoption | file path |
| ------|------|-------|----|
| root | root | 0600 | /etc/ssh/sshd_config |
| root | root | 0640 | /etc/ssh/sshd_config |
| root | root | 0644 | /etc/ssh/sshd_config | 

## patternn
```
xisudo -f [file path]
# lalu tambahkan/hapus baris directive tertentu
```
## object
| Directive/Target  | ket | file path |
| ------|------|-------|
| Defaults use_pty | ada | /etc/sudoers, /etc/sudoers.d/* |
| Defaults logfile="/var/log/sudo.log" | ada (tambh)  | /etc/sudoers, /etc/sudoers.d/* |
| (tag) NOPASSWD | tidak ada (hpus)  | /etc/sudoers, /etc/sudoers.d/* |
| (directive) !authenticate | tidak ada (hapus) | /etc/sudoers, /etc/sudoers.d/* |
| Defaults timestamp_timeout=<N> | N sesuai kebijakan (mis. ≤15) | /etc/sudoers, /etc/sudoers.d/* |




# 6. Logging and Auditing
