rk3399_nanopiM4
========================
## Table of Context <a name="toc"></a>
- [Raspberry PI compute](#rpicompute)
- [Tegra K1](#tegraK1)
- [RK3399/NanoPi M4](#rk339_npm4)
	- [OpenCV](#opencv)

## Board <a name="board"></a>

MIPI-CSI - only [own 13.2MP cam](https://www.friendlyarm.com/index.php?route=product/product&path=78&product_id=228) - since connector is 30x0.5mm - [see in detail](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_M4#Layout)

### Cores:
 
- 0-3 - A53
- 4-5 - A72

run on particular core:

- `taskset 0x30 ./runtest` (0x30 = 4+5 )
- `taskset -c 4,5 ./runtest`

`sudo cpufreq-det -c 5 -g performance`

[back to top](#toc)


## Software <a name="soft"></a>

General [wiki](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_M4) including

power supply: `USB-type-C, 5V/3A`

user: `pi/pi`
root: `root/pa`

### OpenCV <a name ="opencv"></a>

- OpenCV can't be build with python - `gcc` just hangup on py.cpp. need to temporary remove physicaly `/usr/bin/python`
- OpenCL/superres crashed due to workgroup_size, which can be 64,128,256 and depends from complexity of the kernel

[back to top](#toc)