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


### General Info <a name ="info"></a>

Latest RockChip SoC shared the same Image Signal Processor(`ISP`):

- RK3288 (used in ASUS ThinkerBoard) - 32 bit ARM Cortex-A17;
- Rk3399 (NanoPi T/M4, FireFly, OrangePi, etc );

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

[back to top](#toc)


### rkisp1 ("new") <a name="rkisp1"></a>

[back to top](#toc)


### Device info <a name="devinfo"></a>

[back to top](#toc)

### GStreamer plugin info <a name="gstreamerinfo"></a>

[back to top](#toc)

### GStreamer usage <a name="gstreamer usage"></a>

[back to top](#toc)


### Linux disto for nanoPi boards status <a name="nanopi"></a>

#### Friendly Elec core/Desktop: 

`rkisp10` - work out-of-box with 20181219 distro
`rkisp1` - don't work

#### Armbian:

`rkisp10` - work after kernel\gstreamer compilation, but without camera white balance and other parameters
`rkisp1` - don't work. but may be work on ASUS thinker board.

[back to top](#toc)