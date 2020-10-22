

### Software
 - [Raspbian Buster](https://www.raspberrypi.org/downloads/raspbian) required;
 - [Android 9.0 -LineageOS 16.0](https://konstakang.com/devices/rpi4/LineageOS16.0/)


### Hardware

 - [Model B](https://www.raspberrypi.org/products/raspberry-pi-4-model-b)
 - [Overclocking](https://www.cnx-software.com/2019/07/26/how-to-overclock-raspberry-pi-4/)
 - [Overclocking wiki](https://www.raspberrypi.org/documentation/configuration/config-txt/overclocking.md
	- SystemInfo: `inxi -Fc0` (`sudo apt install inxi`)

#### Overclocking
```
sudo apt update
sudo apt dist-upgrade
sudo rpi-update
```

than add to: `sudo nano /boot/config.txt`

```
over_voltage=6
arm_freq=2147
gpu_freq=750
```

#### PCA9685 Servo
- [C library](https://github.com/Reinbert/pca9685)
- [AdaFruit Python lib](https://learn.adafruit.com/16-channel-pwm-servo-driver/python-circuitpython)

#### Display
	
	- 2.8" 320x240 ILI9341, touch is XPT2046 
	- [main wiki] (http://www.lcdwiki.com/2.8inch_SPI_Module_ILI9341_SKU:MSP2807)
	- [user manual](http://www.lcdwiki.com/res/MSP2807/2.8inch_SPI_Module_MSP2807_User_Manual_EN.pdf)
	- [spec](https://www.aliexpress.com/item/32927698197.html)
	- [usage](https://www.raspberrypi.org/forums/viewtopic.php?t=157618)
	https://behindthesciences.com/electronics/connecting-ili9341-SPI-TouchScreen-lcd-to-a-raspberry-pi-in-python/
	https://github.com/BLavery/lib_tft24T
	https://www.waveshare.com/wiki/2.8inch_RPi_LCD_(A)
	http://www.lcdwiki.com/3.5inch_RPi_Display	
	https://www.raspberrypi.org/forums/viewtopic.php?t=143581
	
	https://elinux.org/RPi_SPI
	https://pinout.xyz/pinout/spi#
	https://www.raspberrypi.org/forums/viewtopic.php?f=44&t=22608&p=1216154#p1216154


[table for another ILI9341 display](https://sudomod.com/forum/viewtopic.php?t=2312), adapted for this one

| Display | RPi |  |
|---|---|---|
| SDOk/MISO | pin21(GPIO 9) |  |
| LED | pin12(GPIO 18) | BL |
| SCK | pin 23(GPIO 11) |  |
| SDI(MOSI) | pin 19(GPIO10) |  |
| DC | pin18(GPIO24) |  |
| Reset | pin 22(GPIO 25) |  |
| CS | pin 24(GPIO 8) |  |
| GND | pin 20(GND) |  |
| VCC  | pin 17(V3.3) |  |
|  |  | touch section below |
| T_IRQ | pin 11 |  |
| T_D0 | pin 21 | TP_SO? |
| T_DIN | pin 19 | TP_SI |
| T_CS | pin 26 |  |
| T_CLK |   |  |

##### Disable blanking
Create archive /etc/X11/xorg.conf with this content:

```
Section "ServerFlags"
Option "blank time" "0"
Option "standby time" "0"
Option "suspend time" "0"
Option "off time" "0"
EndSection
```
 

Save and restart.

