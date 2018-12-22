rk3399_nanopiM4
========================
## Table of Context <a name="toc"></a>
- [Hardware](#hard)
	- [Cores](#cores)
- [Software](#soft)
 	- [default software](#defaultSoft)
	- [swap](#swap)
	- [Armbian](#armbian)
	- [OpenCV](#opencv)

## Hardware <a name="hard"></a>

MIPI-CSI - only [own 13.2MP cam](https://www.friendlyarm.com/index.php?route=product/product&path=78&product_id=228) - since connector is 30x0.5mm - [see in detail](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_M4#Layout)

[back to top](#toc)

### Cores:<a name="cores"></a>
 
- 0-3 - A53
- 4-5 - A72

run on particular core:

- `taskset 0x30 ./runtest` (0x30 = 4+5 )
- `taskset -c 4,5 ./runtest`

`sudo cpufreq-det -c 5 -g performance`

[back to top](#toc)

### GPU
frequency: `/sys/class/misc/mali0/device/devfreq/ff9a0000.gpu/cur_freq` - 800MHz
can be 200, 300, 400, 600, 800 MHz

[back to top](#toc)



## Software <a name="soft"></a>

### Default friendlyarm software <a name="defaultSoft"> </a>

General [wiki](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_M4) including

Software download - [gdrive](https://drive.google.com/drive/folders/1gaLKSlIHvqhJ5cASTFGSjJ9XvtgosZFQ)

Software install
`sudo dd bs=4M if=rk3399-sd-lubuntu-desktop-xenial-4.4-armhf-20181112.img of=/dev/mmcblk0p1 status=progress oflag=sync`


power supply: `USB-type-C, 5V/3A`

user: `pi/pi`
root: `root/pa`

How to install:

- [Mate](https://www.friendlyarm.com/Forum/viewtopic.php?f=62&t=2036) to ubuntu 18.04 - but it's **broke Arm Mali drivers**!
- [htop](https://github.com/avafinger/htop-2.1.1_enhanced-version/tree/master/htop) with big\little cores(require root to show Frequency correctly)

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


### Armbian <a name="armbian"></a>

default login: `root`
default pass: `1234`

No accelerated drivers provided - need to install:

 - OpenCL `https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.2.1`
 - Open GL ES2 not working for now
 - for GL/GLES2/CLinfo `sudo apt install clinfo mesa-utils mesa-utils-extra` 
 - Qt5.9.5 `sudo apt install build-essential qt5-default qt5-doc qtbase5-examples qt5-doc-html qtbase5-doc-html` 
[back to top](#toc)


### OpenCV <a name ="opencv"></a>

- OpenCV can't be build with python - `gcc` just hangup on py.cpp. need to temporary remove physicaly `/usr/bin/python`
- OpenCL/superres crashed due to workgroup_size, which can be 64,128,256 and depends from complexity of the kernel

`sudo apt install opencl-c-headers cmake`

let's use only A72 cores to build:

```
mkdir build
cd build
mkdir opencv
cd opencv
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -D BUILD_TESTS=ON -D BUILD_EXAMPLES=ON -D INSTALL_C_EXAMPLES=ON -D WITH_OPENCL=ON ../../opencv
make -j 2
```


[back to top](#toc)