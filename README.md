This is a repository for debian packages for installing OpenCPN Chart plotting software on
the Orange Pi PC or equivalent Allwinner H# arm CPU based Linux Development boards.
<br />
The selected OS is Armbian, Linux for ARM development boards, from armbian.com.

<br />
Revisions:<br />

  <li>Armbian_5.05_Orangepih3_Debian_jessie_3.4.110_desktop
  <li>OpenCPN 4.2.0.1 (VERSION_DATE "2016-02-03")
  <li>Orange PI PC  (purchased Feb, 2016)
<br />
Compiled without and with debug support.
  <li>opencpn_4.2.0-1_armhf.deb
  <li>opencpn_debug_4.2.0-1_armhf.deb

<br />For compiling OpenCPN see:  http://kb7kmo.blogspot.com/2016/04/opencpn-on-orange-pi-allwinner-h3-arm.html

<br />

These instructions start with a blank micro SD card.
Performance of these cards varries alot just copping the image on to it.
  <li>Samsung 32GB EVO - 19MB/s
  <li>Samsung 8GB PRO  - 4MB/s
  <li>Transend 8GB 400x HC-i 42.2MB/s
 
<br />Copy the OS image to the SD card:
<br /><code>
sudo time dd bs=4M of=/dev/mmcblk0 if=Armbian_5.05_Orangepih3_Debian_jessie_3.4.110_desktop.raw
</code>

mount the card and edit the /boot/boot.cmd to change the hyphen to and underscore in cgroup_enable.
unmount SDcard and boot in OPiPC.

<br />
Wait for it to boot twice, up to 3 minutes.
<br />
Login as user: root password: 1234
<br />
It asks you to reset roots password and confirm.
<br />Then asks to create a normal user.
<br />
Optionally choose a different display resolution.

<br />
Connect to the Internet, currently LAN works fine, some WiFi dongles, but not mine.
<br />The following resulted in 81.7MB downlod as of Apr 18, 2016:
<br /><code>
sudo apt-get update<br>
sudo apt-get upgrade
</code>

If you plan to use ssh, as root add this line to the end of /etc/ssh/sshd.conf
<br /><code>
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,blowfish-cbc,aes128-cbc,3des-cbc,cast128-cbc,arcfour,aes192-cbc,aes256-cbc
</code>
<br />Now restart sshd:
<br /><code>
sudo service sshd restart ; sudo service sshd status
</code>
<br />
Currently, USB memory devices are not automounted so:
<br /><code>
sudo apt-get install gvfs policykit-1 policykit-1-gnome eject<br>
sudo mkdir -p /etc/polkit-1/localauthority/50-local.d/
</code>
<br />and create these two files there:

<br />
plugdev.pkla
<pre>
<code>
[Allow Automount]
Identity=unix-group:plugdev
Action=org.freedesktop.udisks2.filesystem-mount;org.freedesktop.udisks2.filesystem-mount-system;org.freedeskt
op.udisks2.filesystem-mount-other-seat;org.freedesktop.udisks2.filesystem-unmount-others;org.freedesktop.udis
ks2.eject-media;org.freedesktop.udisks2.eject-media-system;org.freedesktop.udisks2.power-off-drive*
ResultAny=yes
ResultInactive=yes
ResultActive=yes
</code>
</pre>
<br />


power.pkla
<pre>
<code>
[Allow Desktopstuff]
Identity=unix-group:sudo
Action=org.freedesktop.login1.reboot;org.freedesktop.login1.reboot-multiple-session;org.freedesktop.login1.po
wer-off;org.freedesktop.login1.power-off-multiple-sessions;org.freedesktop.login1.suspend;org.freedesktop.log
in1.suspend-multiple-sessions;org.freedesktop.login1.hibernate;org.freedesktop.login1.hibernate-multiple-sess
ions
ResultAny=yes
ResultInactive=yes
ResultActive=yes
</code>
</pre>

Install the prerequisites for OpenCPN:
<br /><code>
sudo apt-get install libportaudio2 libtinyxml2.6.2 libwxbase3.0-0 libwxgtk3.0-0 wx3.0-i18n libwxbase3.0-0 libwxgtk3.0-0 wx3.0-i18n libtinyxml2.6.2 libportaudio2
</code>

<br />And finally download OpenCPN package and install with:
<br /><code>
sudo dpkg -i opencpn_4.2.0-1_armhf.deb 
</code>
