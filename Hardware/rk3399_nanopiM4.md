rk3399_nanopiM4
========================
## Table of Context <a name="toc"></a>
- [Hardware](#hard)
	- [Cores](#cores)
	- [GPU](#gpu)
	- [make SD card](#makeSDcard)
- [Software](#soft)
 	- [default software](#defaultSoft)
	- [swap](#swap)
	- [Armbian](#armbian)
	- [OpenCV](#opencv)

## Hardware <a name="hard"></a>

MIPI-CSI - only [own 13.2MP cam](https://www.friendlyarm.com/index.php?route=product/product&path=78&product_id=228) - since connector is 30x0.5mm - [see in detail](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_M4#Layout)

[back to top](#toc)

### Cores <a name="cores"></a>
 
- 0-3 - A53
- 4-5 - A72

run on particular core:

- `taskset 0x30 ./runtest` (0x30 = 4+5 )
- `taskset -c 4,5 ./runtest`

`sudo cpufreq-set -c 5 -g performance`

[back to top](#toc)

### GPU<a name="gpu"></a>
 
frequency: `/sys/class/misc/mali0/device/devfreq/ff9a0000.gpu/cur_freq` - 800MHz
can be 200, 300, 400, 600, 800 MHz


`sudo systemctl disable ondemand` - for ubuntu 18.04
`/sys/devices/system/cpu/cpufreq/policy0` - A53x4
`/sys/devices/system/cpu/cpufreq/policy4`- A72x2

set predefined freq fro bosth CPU/CPU: 1200MHz/600MHz
can ba added to `/etc/rc.local`

```
echo "CPU-A53"
echo "performance" > /sys/devices/system/cpu/cpufreq/policy0/scaling_governor
echo 1200000 > /sys/devices/system/cpu/cpufreq/policy0/scaling_max_freq
echo "CPU-A72"
echo "performance" > /sys/devices/system/cpu/cpufreq/policy4/scaling_governor
echo 1200000 > /sys/devices/system/cpu/cpufreq/policy4/scaling_max_freq
echo "GPU-Mali"
echo "performance" > /sys/class/misc/mali0/device/devfreq/ff9a0000.gpu/governor
echo 600000000 > /sys/class/misc/mali0/device/devfreq/ff9a0000.gpu/max_freq
```


Mali graphic debugger
Required X11 - can't recognize core

```
scp libinterceptor.so pi@192.168.8.121:/home/pi
scp mgddaemon  pi@192.168.8.121:/home/pi
```

[back to top](#toc)

### Make SD card <a name="makeSDcard"></a>

[Ubuntu18 docker](https://github.com/friendlyarm/friendlyelec-ubuntu18-docker)

[https://github.com/friendlyarm/sd-fuse_rk3399](https://github.com/friendlyarm/sd-fuse_rk3399)

[back to top](#toc)

## Software <a name="soft"></a>

### Default friendlyarm software <a name="defaultSoft"> </a>

General [wiki](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_M4) including

Software download - [gdrive](https://drive.google.com/drive/folders/1gaLKSlIHvqhJ5cASTFGSjJ9XvtgosZFQ)

Software install
`sudo dd bs=4M if=rk3399-sd-lubuntu-desktop-xenial-4.4-armhf-20181112.img of=/dev/mmcblk0 status=progress oflag=sync`


power supply: `USB-type-C, 5V/3A`

user: `pi/pi`
root: `root/pa`

How to install:

- [Mate](https://www.friendlyarm.com/Forum/viewtopic.php?f=62&t=2036) to ubuntu 18.04 - but it's **broke Arm Mali drivers**!
- [htop](https://github.com/avafinger/htop-2.1.1_enhanced-version/raw/master/htop/htop_2.1.1-3_arm64.deb) with big\little cores(require root to show Frequency correctly). already included in Armbian.

[back to top](#toc)

### Swap
```
sudo swapon --show
sudo fallocate -l 1G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo cp /etc/fstab /etc/fstab.bak
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

```
[back to top](#toc)

### Autostart

`~/.config/autostart/x11vnc.desktop`

```
[Desktop Entry]
Type=Application
Name=x11vnc autostart
Comment=Start x11vnc
Exec=sh -c 'x11vnc -forever'
OnlyShowIn=LXDE
```

[back to top](#toc)


### Armbian <a name="armbian"></a>

first login required HDMI connection!

default login: `root`
default pass: `1234`
setup: `sudo armbian-config`

No accelerated drivers provided - need to install:

 - OpenCL `https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.2.1`
 - Open GL ES2 not working for now
 - for GL/GLES2/CLinfo `sudo apt install clinfo mesa-utils mesa-utils-extra` 
 - Qt5.9.5 `sudo apt install build-essential qt5-default qt5-doc qtbase5-examples qt5-doc-html qtbase5-doc-html` 

kernel sources can be installed from armbian-config 

[back to top](#toc)

### avafinger Linux

Minimal linux [https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal] with KODI.

[back to top](#toc)

### kernel <a name=""kernel"></a>

[details - sd-fuse_rk3399](https://github.com/friendlyarm/sd-fuse_rk3399)
 
```
sudo apt install bc liblz4-tool
git clone https://github.com/friendlyarm/kernel-rockchip --depth 1 -b nanopi4-linux-v4.4.y kernel-rockchip
cd kernel-rockchip
```
in case of buil on board need to remove cross compile prefix in nanopi4linux_defconfig

```
make ARCH=arm64 nanopi4_linux_defconfig
make ARCH=arm64 nanopi4-images
```


### OpenCV <a name ="opencv"></a>

- OpenCV can't be build with python - `gcc` just hangup on py.cpp. need to temporary remove physicaly `/usr/bin/python`
- OpenCL/superres crashed due to workgroup_size, which can be 64,128,256 and depends from complexity of the kernel

 - to build with OpenCL: `sudo apt install opencl-c-headers cmake`
 - to build on Armbian: `sudo apt install libgtk2.0-dev pkg-config`

let's use only A72 cores to build:

```
mkdir build
cd build
mkdir opencv
cd opencv
cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
	-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
	-D BUILD_TESTS=ON \
	-D BUILD_EXAMPLES=ON \
	-D INSTALL_C_EXAMPLES=ON \
	-D WITH_OPENCL=ON \
	../../opencv
make -j 2
```


[back to top](#toc)
