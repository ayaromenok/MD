tegraTx1Nano
========================

[Carriead board: 4x4CSI cams](https://github.com/antmicro/jetson-nano-baseboard)


## System
`tegra210-porg-p3448`

### jtop

- `sudo apt install python-pip`
- `git clone https://github.com/rbonghi/jetson_stats.git``
- `cd jetson_stats`
-  `sudo -H pip install jetson-stats`

### G-Streamer

[nvpdf](https://developer.download.nvidia.com/embedded/L4T/r31_Release_v1.0/Docs/Accelerated_GStreamer_User_Guide.pdf)

[ridgerun pipelines](https://developer.ridgerun.com/wiki/index.php?title=Gstreamer_pipelines_for_Jetson_TX1)

### Kernel
[compile for arm](https://github.com/umiddelb/armhf/wiki/How-To-compile-a-custom-Linux-kernel-for-your-ARM-device)


## Tests

### I/O

#### IOZone3

`sudo apt install iozone3`
 

[Nano PI T/M4 test/Armbian](https://forum.armbian.com/topic/8097-nanopi-m4-performance-and-consumption-review/)

##### SD
SanDisk microSDXC 64GB Ultra C10 (SDSQUNS-064G-GN3MA)

`iozone -I -a -s 100M -r 4k -r 16k -r 512k -r 1024k -r 16384k -i 0 -i 1 -i 2 ﻿-e /dev/mmcblk0`
```
                                                              random    random     bkwd    record    stride                                    
              kB  reclen    write  rewrite    read    reread    read     write     read   rewrite      read   fwrite frewrite    fread  freread
          102400       4     2689     3151     9640     9720     8995     2452                                                          
          102400      16     4962    10825    28109    26939    25623     5129                                                          
          102400     512    13449    22286    72213    66743    65744    27217                                                          
          102400    1024    21610    31766    67329    69440    70787    32035                                                          
          102400   16384    32137    29891    83337    83145    83785    32421 
```
##### USB3
SanDisk Ultra Fit 32GB USB 3.1 (SDCZ430-032G-G46)

`iozone -I -a -s 100M -r 4k -r 16k -r 512k -r 1024k -r 16384k -i 0 -i 1 -i 2 ﻿-e /dev/sda1`
```
                                                             random    random     bkwd    record    stride                                    
              kB  reclen    write  rewrite    read    reread    read     write     read   rewrite      read   fwrite frewrite    fread  freread
          102400       4     3185     3359     9569     9858     8873     2692                                                          
          102400      16     3246     9791    27695    26346    22949     5687                                                          
          102400     512    13589    19637    74022    68300    64778    24242                                                          
          102400    1024    31169    26515    65636    69584    71667    29728                                                          
          102400   16384    27738    32379    82674    83473    86129    33039 
```

#### HDparm

`sudo apt-get install -y hdparm`

##### SD
SanDisk microSDXC 64GB Ultra C10 (SDSQUNS-064G-GN3MA)

```
sudo hdparm -t /dev/mmcblk0
Timing buffered disk reads: 250 MB in  3.02 seconds =  82.90 MB/sec
```

##### USB3
SanDisk Ultra Fit 32GB USB 3.1 (SDCZ430-032G-G46)

```
sudo hdparm -t /dev/sda1 
 Timing buffered disk reads: 250 MB in  3.02 seconds =  82.80 MB/sec
```