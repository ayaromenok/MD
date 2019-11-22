Tinker Board
========================
### TOC<a name ="toc"></a>
- [install](#install)
	- [asus os/debian stretch](#asusos)
	- [armbian](#)
- [software](#software)
- [hardware](#hardware)
	- [camera](#camera)
	- [cpu/gpu temperature](#cpugputemp)

### Install <a name ="install"></a>

#### Asus OS/Debian Strech <a name ="asusos"></a>

`sudo dd if=20181023-tinker-board-linaro-stretch-alip-v2.0.8.img of=/dev/mmcblk0 bs=4MiB status=progress oflag=sync`

user: `linaro`
pass: `linaro`

config: `tinker-config` - similar to raspi-config. need to select camera(`v1.3` or `v2.1`) here

camera config: `~/camera/xml`

**OpenCL fix** - rename /etc/OpenCL/vend**E**rs to vend**O**rs

kernel:

- [kernel sources](https://github.com/TinkerBoard/debian_kernel)
- [kernel config](https://github.com/TinkerBoard/debian_kernel/blob/release/arch/arm/configs/miniarm-rk3288_defconfig)


[back to top](#toc)

#### Ambian<a name="armbian"></a>

- Armbian\Desktop **default**  use std 4.4 kernel
- Armbian\Desktop  **next**  use 4.19.x kernel

`sudo dd if=Armbian_5.77_Tinkerboard_Ubuntu_bionic_next_4.19.33_desktop.img of=/dev/mmcblk0 bs=4MiB status=progress oflag=sync
`

user: `root``
pass: `1234`

config: `armbian-config`

[back to top](#toc)

### Software <a name ="software"></a>

[perfect wiki](https://tinkerboarding.co.uk/wiki/index.php/Software)

[back to top](#toc)

### Hardware <a name ="hardware"></a>

#### Camera <a name ="camera"></a>
Asus Thinker board wiki provide complete info for:

- old [isp10](https://tinkerboarding.co.uk/wiki/index.php/CSI-camera-2.0.7) - with 2.0.7 firmware or below
- new [isp1](https://tinkerboarding.co.uk/wiki/index.php/CSI-camera-2.0.8) - with 2.0.8 firmware or above

[back to top](#toc)

#### CPU/GPU Tempeature <a name ="cpugputemp"></a>

```
#!/bin/bash
celsius1=$(cat /sys/class/thermal/thermal_zone0/temp | sed 's/.\{3\}$/.&/')
celsius2=$(cat /sys/class/thermal/thermal_zone1/temp | sed 's/.\{3\}$/.&/')
echo "   CPU/GPU temperature"
echo "   ${celsius1} °C"
echo "   ${celsius2} °C"
```

[back to top](#toc)