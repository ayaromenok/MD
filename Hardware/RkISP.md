RkISP
========================

### TOC
- [General info](#info)
- [rkisp10 "old"](#rkisp10)
- [rkisp1 "new"](#rkisp1)
- [devices info](#devinfo)
- [gstreamer plugin info](#gsreamerinfo)
- [usage with gstreamer](#gstreamerusage)
- [Linux disto for NanoPi boards status](#nanopi)
- [Camera IQ files](#iqfiles)


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
- [rkisp1 wiki ](http://opensource.rock-chips.com/wiki_Rockchip-isp1)
- [gstreamer isp1](https://github.com/rockchip-linux/camera_engine_rkisp)
- [gstreamer - rkximage](https://github.com/rockchip-linux/gstreamer-rockchip-extra) - to display via script under `X11/gst-launch-1.0`, not needed for OpenCV;
[back to top](#toc)


### Device info <a name="devinfo"></a>

Typically camera device at rkisp looks like different `/dev/video*` devices:

| name |  |  |
|---|---|---|
| /dev/video0 | 4416x3312 | Main scaler path, YUV only |
| /dev/video1 | 1920x1080 | Self scaler path, YUV or RGB888, 666, 565 (need to test!) |
| /dev/video2 |  | statistic  |
| /dev/video3 |  | config for AWV, etc |
| /dev/video4-7 |  | 2nd CSI camera |

sources:

- [wiki](http://opensource.rock-chips.com/wiki_Rockchip-isp1)
- [rk3399 pdf](http://opensource.rock-chips.com/images/6/60/Rockchip_RK3399_Datasheet_V1.6-20170301.pdf)

[back to top](#toc)

### GStreamer plugin info <a name="gstreamerinfo"></a>

[back to top](#toc)

### GStreamer usage <a name="gstreamer usage"></a>

Asus Thinker board wiki provide complete info for:

- old [isp10](https://tinkerboarding.co.uk/wiki/index.php/CSI-camera-2.0.7) - with 2.0.7 firmware or below
- new [isp1](https://tinkerboarding.co.uk/wiki/index.php/CSI-camera-2.0.8) - with 2.0.8 firmware or above

[back to top](#toc)


### Linux disto for nanoPi boards status <a name="nanopi"></a>

#### Friendly Elec core/Desktop: 

- `rkisp10` - work out-of-box with 20181219 distro
- `rkisp1` - don't work

#### Armbian:

- `rkisp10` - work after kernel\gstreamer compilation, but without camera white balance and other parameters
- `rkisp1` - don't work. but may be work on ASUS thinker board.

[back to top](#toc)


### Camera IQ files <a name="#iqfiles"></a>

[link to all IQ's](https://github.com/rockchip-linux/camera_engine_rkisp/tree/master/iqfiles)

| sensor  | camera | add info |
|---|---|---|
| IMX327  |  | 1925x1097 |
| OV4689  | nanopi cam400 /30x0.5| 16:9  |
| OV13850 | NanoPi cam13 / 30x0.5 | 4:3  |
| OV2685 |  |  |
| OV2718 |  |  |
| OV2735 |  |  |
| OV5696 |  |  |
| OV7251 |  |  |
| OV7750 |  |  |
| GC2355 |  |  |
| SC031GS |  |  |



[back to top](#toc)

