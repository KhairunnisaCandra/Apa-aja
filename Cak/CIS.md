# CIS

## 1. Initial setup
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
| 1     |   /var     | nodev,nosuid |
| 2     |   /home    |  nodev,nosuid
| 3     |   /tmp     | nodev,nosuid,noexec |
| 4     |   /dev/shm | nodev,nosuid,noexec |
| 5     | /var/tmp   | nodev,nosuid,noexec |
| 6     | /var/log   | nodev,nosuid,noexec |
| 7     | /var/log/audit | nodev,nosuid,noexec |

## pattern package management
> regulaly update arch linux
```
pacman -Syu
```
