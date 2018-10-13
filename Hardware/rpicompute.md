rpicompute
========================

## Install

### Flash module
on I/O module:
 
- Pull the jumpers of USB SLAVE 1/2/3/4 SELECTION (you need to pull two jumpers
here), set the BOOT ENABLE USB SLAVE jumpers to EN position.
- Plug the USB SLAVE port of IO Board Plus into your host PC USB. (don’t need to
connect power adapter to the IO Board Plus )

See [Compute_Module_IO_Board_PLUS_User_Manual_EN.pdf](http://copperhilltech.com/content/Compute_Module_IO_Board_PLUS_User_Manual_EN.pdf) for details;

Use `raspbian-stretch-lite` image to fit to 4GB of rpi compute


Flash CM's EMMC as described in [official guide](https://www.raspberrypi.org/documentation/hardware/computemodule/cm-emmc-flashing.md) :

- `sudo ./rpiboot`
- `sudo dd if=2018-06-27-raspbian-stretch-lite.img of=/dev/sdc bs=4MiB`

Config:

- default user: `pi`
- default passwd: `raspberry` - don't forget to change with `passwd`
- wifi - `sudo raspi-config`
- set localization option to en.us-utf8 by `sudo raspi-config`
- set correct timezone`dpkg-reconfigure tzdata`

[installing GUI](https://www.raspberrypi.org/forums/viewtopic.php?p=890408#p890408), including Mate

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

### dual Cam
- `sudo raspi-config` and enable the camera;
- `wget https://www.raspberrypi.org/documentation/hardware/computemodule/dt-blob-dualcam.dts`
- `dtc -I dts -O dtb -o dt-blob-dualcam.dtb dt-blob-dualcam.dts`;
- `sudo cp dt-blob-dualcam.dtb /boot/dt-blob.bin`;
- `reboot` to load blobs;
-  correct output is: 
`vcgencmd get_camera
supported=2 detected=2`;

get images: `raspivid -cs 0 -o image0.jpg` for 1st camera and  `raspivid -cs 1 -o image1.jpg` for second

#### Video4Linux

At 2018.06 build Video4Linux driver is already included, but not loaded by default, so `bcm2835-v4l2` need to be added to /ect/modules. `v4l2-ctl --list-formats` output a list of supported formats. Additional info can be found at [rpi forum](https://www.raspberrypi.org/forums/viewtopic.php?t=62364)

### Software
#### Swap file size
open `sudo nano /etc/dphys-swapfile`, than increase to 512MB `CONF_SWAPSIZE=512`

than restart

- `sudo /etc/init.d/dphys-swapfile stop`
- `sudo /etc/init.d/dphys-swapfile start`

#### Partitions
Since rpi Compute have only 4GB of EMMC memory, it's necessary to move some data to SD/USBFlash drive, like:

 - /home/pi 
 - /usr/local
 - /usr/share
 - /usr/include
 - swap file
 - /var/cache/apt

 - looks like impossible to move `/usr/lib` even it should be possible according Unix standard ;) 
 
#### Qt
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


 - [Configure QtCreator](https://www.ics.com/blog/configuring-qt-creator-raspberry-pi)

#### OpenCV

`sudo apt-get install build-essential cmake pkg-config libjpeg-dev libpng-dev libtiff-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev`

Gstreamer and most of the dev libs already installed with Qt from above

`cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -D ENABLE_NEON=ON -D ENABLE_VFPV3=ON -D BUILD_TESTS=OFF -D BUILD_EXAMPLES=OFF -D WITHQT=ON ..`

Note`WITH_OPENGL=ON`