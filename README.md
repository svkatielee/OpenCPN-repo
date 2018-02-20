This is a repository for debian packages for installing OpenCPN Chart plotting software on
the Orange Pi PC or equivalent Allwinner H3 ARM SoC based Development boards.

The selected OS is **armbian**, Linux for ARM development boards, from (http://www.armbian.com).

**!! UPDATE !!!**  Feb 20, 2018
added update package:
    opencpn_4.8.2-1_min_armhf.deb
    min = no DOCs, no tcdata, maps=CRUDE
    
Compliing instructions are at:
    https://kb7kmo.blogspot.tw/2018/02/compile-opencpn-482-for-armbian.html



!! UPDATE !!!bJun, 2016
Added new updated package:
Revisions:  = opencpn_4.4.0-1_armhf.deb
 * Armbian_5.14_Orangepipc_Debian_jessie_3.4.112_desktop.raw
 * OpenCPN 4.4.0 (VERSION_DATE "2016-06-13")
 * Orange PI PC v1.2 (purchased Feb, 2016)

Revisions:
 * Armbian_5.05_Orangepih3_Debian_jessie_3.4.110_desktop
 * OpenCPN 4.2.0.1 (VERSION_DATE "2016-02-03")
 * Orange PI PC  (purchased Feb, 2016)

For compiling OpenCPN see: [OpenCPN on Orange Pi Allwinner H3 ARM](http://kb7kmo.blogspot.com/2016/04/opencpn-on-orange-pi-allwinner-h3-arm.html)

These instructions start with a blank micro SD card.
Performance of these cards varies a lot just copping the image on to it.
 * Samsung 32GB EVO - 19MB/s
 * Samsung 8GB PRO  - 4MB/s
 * Transend 8GB 400x HC-i 42.2MB/s
 
* Copy the OS image to the SD card:
```
sudo time dd bs=4M of=/dev/mmcblk0 if=Armbian_5.05_Orangepih3_Debian_jessie_3.4.110_desktop.raw
```
* mount the card and edit the `/boot/boot.cmd` to change the hyphen to and underscore in `cgroup_enable`.
unmount SDcard and put it in the Orange Pi PC.

* Connect to the Internet, currently LAN works fine, some WiFi dongles, but not mine.

* Power up and Wait for it to boot twice, up to 3 minutes.
Login as user: `root` password: `1234`
It asks you to reset root\'s password and confirm.
Then asks to create a normal user.
Optionally choose a different display resolution.

* Update the installed software. The following resulted in 81.7MB downlod as of Apr 18, 2016:
```
sudo apt-get update
sudo apt-get upgrade
```

* Install the prerequisites for OpenCPN:
```
sudo apt-get install libportaudio2 libtinyxml2.6.2 libwxbase3.0-0 libwxgtk3.0-0 wx3.0-i18n libwxbase3.0-0 libwxgtk3.0-0 wx3.0-i18n libtinyxml2.6.2 libportaudio2 wx3.0-i18n
```

* And finally download OpenCPN package and install with:
```
sudo dpkg -i opencpn_4.4.0-1_armhf.deb
```

