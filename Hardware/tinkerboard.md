Tinker Board
========================
### TOC<a name ="toc"></a>
- [install](#install)
	- [asus os/debian stretch](#asusos)
- [software](#software)
- [hardware](#hardware)
	- [camera](#camera)
	- [cpu/gpu temperature](#cpugputemp)

### Install <a name ="install"></a>

#### Asus OS/Debian Strech <a name ="asusos"></a>

`dd if=20181023-tinker-board-linaro-stretch-alip-v2.0.8.img of=/dev/mmcblk0 bs=4MiB status=progress oflag=sync`

user: `linaro`
pass: `linaro`

config: `tinker-config` - similar to raspi-config. need to select camera(`v1.3` or `v2.1`) here

camera config: `~/camera/xml`

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