rk3399_nanopiM4
========================
## Table of Context <a name="toc"></a>
- [Hardware](#hard)
	- [Cores](#cores)
- [Software](#soft)
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


## Software <a name="soft"></a>

General [wiki](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_M4) including

power supply: `USB-type-C, 5V/3A`

user: `pi/pi`
root: `root/pa`

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


### OpenCV <a name ="opencv"></a>

- OpenCV can't be build with python - `gcc` just hangup on py.cpp. need to temporary remove physicaly `/usr/bin/python`
- OpenCL/superres crashed due to workgroup_size, which can be 64,128,256 and depends from complexity of the kernel

let's use only A72 cores to build:

```
mkdir build/opencv
cd build/opencv
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -D BUILD_TESTS=ON -D BUILD_EXAMPLES=OFF ../../opencv
make -j 2
```


[back to top](#toc)