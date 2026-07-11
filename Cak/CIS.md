# CIS

## 1. Initial setup

### pattern (configure file system kernel module)
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


## pattern (file system partition)
```
[device] [mount_target] [mount_option] 0 0
```
## object

## pattern package management
> regulaly update arch linux
```
pacman -Syu
```
