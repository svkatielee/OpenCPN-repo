This is a repository for Debian or Ubuntu style packages for installing OpenCPN Chart plotting software on
arm SBCs running Armbian such as the Orange Pi PC or equivalent Allwinner H3 ARM SoC based Development boards.

The selected OS is **armbian**, Linux for ARM development boards, from (http://www.armbian.com).

**!! UPDATE !!!**  Feb 20, 2018

I added update package compiled in armbian 5.38 Ubuntu 16.04 :
 * opencpn_4.8.2-1_min_armhf.deb
   * min = no DOCs, no tcdata, maps=CRUDE
 * opencpn_4.8.2_armhf.def
   * = no DOCs, default tcdata, maps=LOW res
 * tcdata/*
   * tide data from WXTide with stations throughout Asia

    
Compliing instructions are at:
    https://kb7kmo.blogspot.tw/2018/02/compile-opencpn-482-for-armbian.html



!! UPDATE !!! Jun, 2016
Added new updated package:
Revisions:  = opencpn_4.4.0-1_armhf.deb
 * Armbian_5.14_Orangepipc_Debian_jessie_3.4.112_desktop.raw
 * OpenCPN 4.4.0 (VERSION_DATE "2016-06-13")
 * Orange PI PC v1.2 (purchased Feb, 2016)

Revisions:
 * Armbian_5.05_Orangepih3_Debian_jessie_3.4.110_desktop
 * OpenCPN 4.2.0.1 (VERSION_DATE "2016-02-03")
 * Orange PI PC  (purchased Feb, 2016)

For compiling OpenCPN see the [OpenCPN Developers Manual]  (https://opencpn.org/wiki/dokuwiki/doku.php?id=opencpn:developer_manual:developer_guide:compiling_linux:building_on_armhf_linux_-_armbian_-_orange_pi)
 or [Compile OpenCPN 4.8.2 for Armbian](https://kb7kmo.blogspot.tw/2018/02/compile-opencpn-482-for-armbian.html) 

These instructions start with a blank micro SD card.
Performance of these cards varies a lot just copping the image on to it.
 * Samsung 32GB EVO - 19MB/s
 * Samsung 8GB PRO  - 4MB/s
 * Transend 8GB 400x HC-i 42.2MB/s
 
* Copy the OS image to the SD card:
```
sudo time dd bs=4M of=/dev/sdc if=Armbian_5.38_Orangepipcplus_Ubuntu_xenial_default_3.4.113_desktop.im
```

* Connect to the Internet, currently LAN works fine, some WiFi dongles.

* Power up
Login as user: `root` password: `1234`
It asks you to reset root\'s password and confirm.
Then asks to create a normal user, set passwd and set GCOES 
Then offers to choose a different display resolution.
( my 1025x768 display needs: h3disp -m 32) 

* Update the installed software:
```
sudo apt-get update
sudo apt-get upgrade
```

* Install the prerequisites for OpenCPN:
```
** for 4,.8.2 on ubuntu 16.04 **
apt install libwxgtk3.0-0v5 wx3.0-i18n libglu1-mesa  libtinyxml2.6.2v5 libportaudio2 \
     libwxbase3.0-0v5 libcurl4-openssl-dev
```

* And finally download OpenCPN package and install with:
```
sudo dpkg -i opencpn_4.8.2-1_armhf.deb
```
* You can also copy the tcdata/* files to a space on yout system and point to them in opencpn 
...
Tools->Options->Charts->Tides & Currents->Add Dataset
...
