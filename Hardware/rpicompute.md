rpicompute
========================

### TOC<a name ="toc"></a>
- [install](#install)
	- [Flash RPi module](#flashmodule)
	- [Dual Camera](#dualcam)
		- [Video4Linux](#Videlo4Linux)
- [Software](#software)
	- [Qt](#qt)
	- [OpenCV](#opencv)
	- [POCL](#pocl)
	- [Other OS](#otheros)
		- [Motion OS](#motionos)
		- [Ubuntu Mate](#ubuntumate)
		- [Android](#android)
- [CNC server](#cnc)


### Install <a name ="install"></a>

#### Flash module <a name ="flashmodule"></a>
on I/O module:
 
- Pull the jumpers of USB SLAVE 1/2/3/4 SELECTION (you need to pull two jumpers
here), set the BOOT ENABLE USB SLAVE jumpers to EN position.
- Plug the USB SLAVE port of IO Board Plus into your host PC USB. (don’t need to
connect power adapter to the IO Board Plus )
- run rpiboot(sudo /share/rpi/rpiboot/rpiboot) to mount CM to PC

See [Compute_Module_IO_Board_PLUS_User_Manual_EN.pdf](http://copperhilltech.com/content/Compute_Module_IO_Board_PLUS_User_Manual_EN.pdf) for details;

Use `raspbian-stretch-lite` image to fit to 4GB of rpi compute


Flash CM's EMMC as described in [official guide](https://www.raspberrypi.org/documentation/hardware/computemodule/cm-emmc-flashing.md) :

- `sudo ./rpiboot`
- `sudo dd if=2019-04-08-raspbian-stretch-lite.img of=/dev/mmcblk0 bs=4MiB status=progress oflag=sync` for sc-card or `of=/dev/sdc` for ComputeModule.
- Raspbiand Desktop since 2019-04-08 also fit ot 4GB ComputeModule; Debian 10 based Raspbian can be installed too

To make a `*.img` from sdcard need to decrease partition size to aprox 125% of used space(unmount partiton, than `sudo gparted /dev/mmcblk0`) and than make opposite `dd` with `bs=1MiB count=2048` for 2GB image.

 
Config:

- default user: `pi`
- default passwd: `raspberry` - don't forget to change with `passwd`
- wifi - `sudo raspi-config`
- set localization option to en.us-utf8 by `sudo raspi-config`
- set correct timezone`dpkg-reconfigure tzdata`

wifi as perconfig:

- create `wpa_supplicant.conf` at `/boot`;
- add

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="YOUR_NETWORK_NAME"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}
```
- add `ssh` empty file to `/boot` to enable SSH server by default

installing GUI brake broadcom drivers;
[installing GUI](https://www.raspberrypi.org/forums/viewtopic.php?p=890408#p890408), including Mate

```
sudo apt-get install lightdm
sudo apt-get install mate-desktop-environment-core
```

Autologin for Console:

- `raspi-config`
- >> `Boot options`
- select autologin for `console` or `GUI`

Autologin for GUI:

- at `/etc/lightdm/lightdm.conf`
- `autologin-user=USERNAME
autologin-user-timeout=0`

- `dpkg-reconfigure lightdm` 



SSH:
`ssh -Y pi@raspberrypi`

VNC:

[guide](https://www.raspberrypi.org/documentation/remote-access/vnc)

`sudo apt-get install realvnc-vnc-server realvnc-vnc-viewer`

`sudo raspi-config > Interface Option > VNC:yes`

[back to top](#toc)

#### dual Cam <a name ="dualcam"></a>
- `sudo raspi-config` and enable the camera;
- `wget https://raw.githubusercontent.com/6by9/documentation/refs/heads/master/hardware/computemodule/dt-blob-dualcam.dts`
- `dtc -I dts -O dtb -o dt-blob-dualcam.dtb dt-blob-dualcam.dts`
- `sudo cp dt-blob-dualcam.dtb /boot/dt-blob.bin`
- `sudo reboot` to load blobs;
-  correct output is: 
`vcgencmd get_camera` : 
`supported=2 detected=2`

get images: `raspistill -cs 0 -o image0.jpg` for 1st camera and  `raspistill -cs 1 -o image1.jpg` for second

OmniVision OV5647 - 2592 × 1944, FOV  160
`raspistill -3d sbs -w 1280 -h 480 -o 1.jpg`

##### TimeLapse

[TimeLapse with raspicam](https://www.raspberrypi.org/documentation/usage/camera/raspicam/timelapse.mm)

Note: raspicam can't make a long (100+) timelapse due to stability issue, so it's a good idea to use `crontab -e` together with short timelapses

[stereo pi IO](http://www.stereopi.com/)

[perfect doc for cameras](https://picamera.readthedocs.io/en/latest/fov.html)

[1k RPI cam](https://www.raspberrypi.org/forums/viewtopic.php?t=212518)

| #mode | resolution | status|
|---|---|---|
|1|1920x1080|ok, part sensor|
|2|2592x1944|ok|
[full sensor info](https://picamera.readthedocs.io/en/release-1.13/fov.html#sensor-modes)

##### NoIR Cams

IRCamera mode(for real cams):
`sudo nano /boot/config.txt`
`disable_camera_led=1 or 0`

[Examples for NoIR Cam's 1.3 and 2.x](https://raspi.tv/2016/new-and-old-raspberry-pi-camera-comparison-shots-1-3-2-1-noir)

##### Remote accecs

[UV4L - remote camera acceess](https://www.linux-projects.org/uv4l/installation/)

[back to top](#toc)

##### Video4Linux <a name ="Video4Linux"></a>


At 2018.06 build Video4Linux driver is already included, but not loaded by default, so `bcm2835-v4l2` need to be added to `/etc/modules`. `v4l2-ctl --list-formats` output a list of supported formats. Additional info can be found at [rpi forum](https://www.raspberrypi.org/forums/viewtopic.php?t=62364)

[back to top](#toc)

#### OpenCL for VC4<a name ="opencl"></a>

[attempt to implement OpenCL 1.2 for pri](https://github.com/doe300/VC4CL), [part 2](https://github.com/doe300/VC4C)

[back to top](#toc)


#### I2C

[Overclocking I2C for OLED display](https://www.raspberrypi-spy.co.uk/2018/02/change-raspberry-pi-i2c-bus-speed/)

[back to top](#toc)

#### Oled SSD1306 0.96 Display

[Great C++ lib](https://github.com/hallard/ArduiPi_OLED)

to compile need to remove `-li2c` on latest Raspbian(since spring 2018)

[doc for lib](http://hallard.me/adafruit-oled-display-driver-for-pi/)

can be used as a frambuffer at [least since 2019.05.14](https://github.com/raspberrypi/firmware/issues/1098)

add to /boot/config.txt 

        dtoverlay=ssd1306,inverted,sequential
        dtparam=i2c_arm=on,i2c_baudrate=1000000

[more info](https://sites.google.com/site/mincepi/pi2oled)

[use fb1 instead of fb0](https://github.com/notro/fbtft/wiki/Framebuffer-use)

`con2fbmap 1 1`

`sudo dpkg-reconfigure console-setup` - to change font


[back to top](#toc)


### Software<a name ="software"></a>

#### Swap file size
open `sudo nano /etc/dphys-swapfile`, than increase to 512MB `CONF_SWAPSIZE=512`

than restart

- `sudo /etc/init.d/dphys-swapfile stop`
- `sudo /etc/init.d/dphys-swapfile start`

#### add sources

`sudo nano /etc/apt/sources.list` and uncomment `deb-src`

#### ssh without password

[ssh login without passwordcgparted](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md)

-  on pi: `ssh-keygen -t rsa -b 4096 -C "ayaromenok@gmail.com"`
-  on PC: `ssh-copy-id pi@rpiIP`


#### Partitions/ComputeModule only
Since rpi Compute have only 4GB of EMMC memory, it's necessary to move some data to SD/USBFlash drive, like:

`/dev/sda1 /mnt/32GB ext4 defaults 0 1`

```
 - /home/pi 
 - /usr/local
 - /usr/share
 - /usr/include
 - swap file
 - /var/cache/apt
```

 - looks like impossible to move `/usr/lib` even it should be possible according Unix standard ;) 

[back to top](#toc)
 
#### Qt <a name ="qt"></a>
 
[Qt 5.12](http://www.tal.org/tutorials/building-qt-512-raspberry-pi)

**Memory split** should be set to **64/128 MB** to avoid EGLFS driver crash:
```
EGL Error : Could not create the egl surface: error = 0x3003
```

- [Cross compile Qt](https://wiki.qt.io/RaspberryPi2EGLFS)
 
For every version of Raspberry Pi, you have to change `-device`:

- Raspberry Pi 1 (+ Zero and Zero W): `-device linux-rasp-pi-g++`
- Raspberry Pi 2: `-device linux-rasp-pi2-g++`
- Raspberry Pi 3: `-device linux-rasp-pi3-g++` - close-source broadcom stack
- Raspberry Pi 3 with VC4 driver: `-device linux-rasp-pi3-vc4-g++`` - open-source experimental stack

Dependencies:

- `sudo apt-get build-dep qt4-x11`
- `sudo apt-get build-dep libqt5gui5`
- `sudo apt-get install libudev-dev libinput-dev libts-dev libxcb-xinerama0-dev libxcb-xinerama0`
- for multimedia\gstreamer - `sudo apt-get install gstreamer1.0-alsa libasound2-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gstreamer1.0-plugins-good gstreamer1.0-plugins-bad libraspberrypi-dev libpulse-dev alsa-base gstreamer1.0-omx libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev`

Broadcom libs instead of Mesa:

- `ln -s /opt/vc/lib/libbrcmEGL.so /usr/lib/arm-linux-gnueabihf/libEGL.so`

- `ln -s /opt/vc/lib/libbrcmGLESv2.so /usr/lib/arm-linux-gnueabihf/libGLESv2.so.2.0.0`


For cross-compilation:

`./configure -release -opengl es2 -device linux-rasp-pi3-g++ -device-option CROSS_COMPILE=~/sdk/rpi/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/arm-linux-gnueabihf- -sysroot ~/sdk/rpi/sysroot -opensource -confirm-license -make libs -prefix /usr/local/qt5pi -extprefix ~/sdk/rpi/qt5pi -hostprefix ~/sdk/rpi/qt5 -v`


For RPI compilation
`./configure --release -opengl es2 -opensource -confirm-license -make libs -no-use-gold-linker`

```
mkdir build
cd build
mkdir qt
cd qt
../../qt/configure --release -opengl es2 \
        -opensource -confirm-license \
        -prefix /usr/local \
        -skip qtlocation \
        -skip qtwebengine \
        -skip qtwebchannel \
        -skip qtwebglplugin \
        -skip qtwebsockets \
        -skip qtwebview \
        -skip qtcanvas3d \
        -skip qtdatavis3d \
	       -skip qtvirtualkeyboard
```

 - [Configure QtCreator](https://www.ics.com/blog/configuring-qt-creator-raspberry-pi)

[back to top](#toc)


#### OpenCV  <a name ="opencv"></a>

`sudo apt-get install build-essential cmake pkg-config libjpeg-dev libpng-dev libtiff-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev`

Gstreamer and most of the dev libs already installed with Qt from above

`cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -D ENABLE_NEON=ON -D ENABLE_VFPV3=ON -D BUILD_TESTS=OFF -D BUILD_EXAMPLES=OFF -D WITHQT=ON ..`

Note `WITH_OPENGL=ON` will try to use Desktop GL

#### POCL <a name ="pocl"></a>

`sudo apt install libhwloc-dev ocl-icd-opencl-dev libglew-dev zlib1g-dev libedit-dev`

`sudo apt install clang-4.0 libclang-4.0-dev`

```
cmake -DLLC_HOST_CPU=cortex-a53 -DWITH_LLVM_CONFIG=/usr/bin/llvm-config-4.0 -DENABLE_ICD=0 -DEXTRA_KERNEL_CL_FLAGS=-mfpu=neon -DEXTRA_KERNEL_CXX_FLAGS=-mfpu=neon ../../pocl
```

installed OpenCL driver:
```
./poclcc -l
LIST OF DEVICES:
0:
  Vendor:   ARM
    Name:   pthread-cortex-a53
 Version:   OpenCL 1.2 pocl HSTR: pthread-armv6-unknown-linux-gnueabihf-cortex-a53
```
[back to top](#toc)

#### Other OS <a name="otheros"></a>

##### MotionEYE OS <a name="motioneyeos"></a>

[Motion EYE OS](https://github.com/ccrisan/motioneyeos)  - use RPi3 as a Security Camera. both CSI and USB cams supported

[back to top](#toc)

##### Ubuntu Mate  <a name="ubuntumate"></a>

[18.04 - 32 or 64 bit](https://ubuntu-mate.org/download/) 
 - can't be installed directly to RPi3A due to low memory issue, but can be run when already installed on RPi3B.
 - 64bit don't have any h\w acceleration :()
 - don't recognize HDMI display for now

[back to top](#toc)


##### Android  <a name="android"></a>

[Android 10/LineageOS 17.1](https://konstakang.com/devices/rpi3) 
  - not working - Hardware video decoding & encoding (software decoding & encoding works)
  - [gapps](https://opengapps.org/)

[back to top](#toc)

### CNC <a name ="cnc"></a>

[laser4web](https://github.com/LaserWeb/LaserWeb4/wiki/1.4-Installation-on-RaspberryPi)

`sudo systemctl status lw.comm-server`

`start|stop|restart`

[back to top](#toc)


