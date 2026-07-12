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
| fs.suid_dumpable | ... | ... |
| kernel.dmesg_restrict | ... | ... |
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

## configure client service
```
pacman -Rs ftp ldap telnet tftp
```
# 3. Network
