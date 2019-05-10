RkISP
========================

### TOC
- [General info](#info)
- [rkisp10 "old"](#rkisp10)
- [rkisp1 "new"](#rkisp1)
- [devices info](#devinfo)
	- [check isp1 status](#check_status)
- [gstreamer plugin info](#gsreamerInfo)
- [usage with gstreamer](#gstreamerUsage)
- [Linux disto for NanoPi boards status](#nanopi)
	- [friendly elec/nanopi m4](#friendlyelec);
	- [armbian/nanopi m4](#armbian);
	- [asus os/tinkerboard](#asusos);
- [Cameras](#cameras) 
	- [ov5647](#ov5647) - RPi Cam v1.3
	- [ov4689](#ov4689) - NanoPi  Cam400 wide 16:9 cam
	- [imx219](#imx219) - RPi Cam v 2.1
	- [ov13850](#ov13850) NanoPI Cam13
	- [Camera IQ files](#iqfiles)
- [Tools](#tools)
	- [yavta](#yavta)
- [ToDo](#todo)


### General Info <a name ="info"></a>

Latest RockChip SoC shared the same Image Signal Processor([ISP](http://opensource.rock-chips.com/wiki_Rockchip-isp1)):

- RK3288 (used in ASUS ThinkerBoard) - 32 bit ARM Cortex-A17;
- Rk3399 (NanoPi T/M4, FireFly, OrangePi, etc );

- Dual MIPI-CSI 4lane(MIPI1 shared CSI\DSI, MIPI2 only for CSI)
- from 80 to 1500 Mbps per line  

It's a **two** version of kernel driver:

- `rkisp10` - original kernel driver(2017-2018), based on Video4Linux subsystem. Support one device in time;
- `rkisp1` - new kernel driver(2018+), used kernel media subsystem(`/dev/media`) to control `ISP` ; Support multiply device in time;

Don't as me why `rkisp1` is higher than `rkisp10` - it's a Chinese way to use Indian or binary numbers ;)

And it's a only **one** `GStreamer`  plugin name to support a both kernel drivers - `rkisp`. Depending from the version, it may support only a `rkisp10` or `rkisp1`.

Different cameras can supporterted by `ISP`, but this depends from board developer:

- 2 line CSI, 15x1mm MIPI interface - Raspi Cam V1/V2 for ASUS Thinker Board;
- 4 line CSI, 30x0.5mm MIPI inteface - [NanoPi](http://wiki.friendlyarm.com/wiki/index.php/NanoPC-T4#Layout)/[FireFly](http://wiki.t-firefly.com/en/Firefly-RK3399/driver_camera.html)/OrangePI - but cameras not compatible between boards due to different layout

[back to top](#toc)


### rkisp10 ("old")<a name="rkisp10"></a>

- [gstreamer isp10](https://github.com/rockchip-linux/gstreamer-camera) - modules>rkisp
- [gstreamer - rkximage](https://github.com/rockchip-linux/gstreamer-rockchip-extra) - to display via script under `X11/gst-launch-1.0`, not needed for OpenCV;

[back to top](#toc)


### rkisp1 ("new") <a name="rkisp1"></a>
- [rkisp1 wiki ](http://opensource.rock-chips.com/wiki_Rockchip-isp1);
- [gstreamer isp1](https://github.com/rockchip-linux/camera_engine_rkisp);
- [gstreamer - rkximage](https://github.com/rockchip-linux/gstreamer-rockchip-extra) - to display via script under `X11/gst-launch-1.0`, not needed for OpenCV;
- `rkisp1` present in Asus tinkerboard 2.0.8+ firmware and as a patches in Armbian kernel for tinkerboardl;

[back to top](#toc)


### Device info <a name="devinfo"></a>

Typically camera device at rkisp looks like different `/dev/video*` devices. position of pathes is different


| Path | TinkerBoard | NanoPi M4|
|---|---|---|
| Main scaler path, YUV only | /dev/video1 | /dev/video2 |
| Self scaler path, YUV or RGB888 | /dev/video0 | /dev/video0|
| statistic  | /dev/video2| ?|
| config for AWV, etc | /dev/video3|? |

Cam2 use /dev/video4-/dev/video7

need to test config dsi files

/kernel-rockchip/arch/arm64/boot/dts/rockchip/
M4: rk3399-nanopi4-rev01.dts

branch stable-4.4-rk3399-linux-20190402 looks like include `isp1` and `dual camera`
https://github.com/FireflyTeam/kernel/blob/stable-4.4-rk3399-linux-20190402/arch/arm64/boot/dts/rockchip/rk3399-firefly-port.dtsi
https://github.com/FireflyTeam/kernel/blob/stable-4.4-rk3399-linux-20190402/arch/arm64/boot/dts/rockchip/rk3399-firefly-linux.dts 

patches:https://github.com/FireflyTeam/kernel/commit/d6e54874c782f12da8391401ceb6491ab62a18f1#diff-66557344644c9e2f3abe605c75d3ff28
https://github.com/FireflyTeam/kernel/commit/a0ea05d352c46f7b21ab8227b1e43306d017e333

[tinkerbaord rkisp1](https://github.com/TinkerBoard/debian_kernel/blob/develop/arch/arm/boot/dts/rk3288-rkisp1.dtsi)

`sudo i2cdetect -y -r 2` : both cameras @36

`/sdk/src/gstreamer/camera_engine_rkisp/rkisp/ia-engine/cam_ia_api/cam_ia10_engine.cpp:303` - `AWB` disabled

sources:

- [wiki](http://opensource.rock-chips.com/wiki_Rockchip-isp1)
- [rk3399 pdf](http://opensource.rock-chips.com/images/6/60/Rockchip_RK3399_Datasheet_V1.6-20170301.pdf)

#### Check isp1 status <a name="check_status"></a>

`sudo media-ctl --print-topology`
`v4l2-compliance`


[back to top](#toc)

### GStreamer plugin info <a name="gstreamerInfo"></a>

[back to top](#toc)

### GStreamer usage <a name="gstreamerUsage"></a>

Asus Thinker board wiki provide complete info for:

- old [isp10](https://tinkerboarding.co.uk/wiki/index.php/CSI-camera-2.0.7) - with 2.0.7 firmware or below
- new [isp1](https://tinkerboarding.co.uk/wiki/index.php/CSI-camera-2.0.8) - with 2.0.8 firmware or above

[back to top](#toc)


### Linux disto for nanoPi boards status <a name="nanopi"></a>

#### Friendly Elec core/Desktop: <a name="frienlyelec"></a>

- `rkisp10` - work out-of-box with 20181219 distro
- `rkisp1` - don't work

#### Armbian/Rk3399:<a name="armbian"></a>

- `rkisp10` - work after kernel\gstreamer compilation, but without camera white balance and other parameters
- `rkisp1` - don't work on rk3399. Work on ASUS thinker board/[firefly custom kernel](http://bbs.t-firefly.com/forum.php?mod=viewthread&tid=2490&extra=).

#### Asus OS:<a name="asusos"></a>
- `rkisp10` - work in 2.0.7 OS version or early;
- `rkisp1` - work in 2.0.8 OS version or later

[back to top](#toc)

### Cameras<a name="#cameras"></a>

#### ov5647: RPi Cam v1.3<a name="#ov5647"></a>

[datasheet](https://cdn.sparkfun.com/datasheets/Dev/RaspberryPi/ov5647_full.pdf)

lens size: 1/4
output 8/10bit RAW

| resolution | fps | rpi fps | rpi mode |
|---|---|---|---|
| 2592x1944 | 15 | 15 | 2 |
| 1920x1080 | 30 | 30 | 1, crop |
| 1280x960| 45 | 42 | 4 |
| 1280x720 | 60 | 49 | 5 |
| 640x480 | 90 |  90| 7 |
| 320x240 | 120 |  - | - |


[back to top](#toc)

#### ov4689: NanoPi  Cam400 wide 16:9 cam<a name="ov4689"></a>

[back to top](#toc)

#### imx219: RPi Cam v 2.1<a name="imx219"></a>

[back to top](#toc)

#### ov13850: NanoPI Cam13<a name="#ov13850"></a>

[back to top](#toc)

#### Camera IQ files <a name="#iqfiles"></a>

[link to all IQ's](https://github.com/rockchip-linux/camera_engine_rkisp/tree/master/iqfiles)

| sensor  | camera | add info |
|---|---|---|
| IMX327  |  | 1925x1097 |
| OV4689  | nanopi cam400 /30x0.5| 16:9  |
| OV13850 | NanoPi cam13 / 30x0.5 | 4:3  |

and many more


[back to top](#toc)

### Tools<a name="#tools"></a>

#### Yet Another V4L2 Test Application<a name="#yavta"></a>

[yavta](git://git.ideasonboard.org/yavta.git)

`./yavta --list-controls /dev/video0``


[back to top](#toc)


### ToDo<a name="#todo"></a>

firefly Rk3399 woks with **isp1** /dualcamera, and kernel looks similar, so 

[back to top](#toc)