# RG35XX
Knowledge for RG35XX Anbernic Device

# Firmware
Anbernic Stock: Dual OS https://win.anbernic.com/download/270.html  
Garlic OS: 1.4.9 https://www.patreon.com/posts/76561333  
Koriki OS: 1.0 https://github.com/rg35xx-cfw/Koriki/releases  
Recalbox OS: 9.1 https://github.com/leonkasovan/RG35XX/wiki  

# Binary
https://github.com/andrew-d/static-binaries/tree/master/binaries/linux/arm  
```
/usr/bin/readelf
/usr/bin/file
/usr/local/share/misc/magic.mgc
```

# Setting for development
```shell
#!/bin/sh
export PATH="/opt/miyoo/arm-miyoo-linux-uclibcgnueabi/sysroot/usr/bin:/opt/miyoo/bin:$PATH"
export CC="/opt/miyoo/bin/arm-miyoo-linux-uclibcgnueabi-gcc"
export CXX="/opt/miyoo/bin/arm-miyoo-linux-uclibcgnueabi-g++"
export CROSS_COMPILE="/opt/miyoo/bin/arm-miyoo-linux-uclibcgnueabi-"
export AR="/opt/miyoo/bin/arm-miyoo-linux-uclibcgnueabi-ar"
export AS="/opt/miyoo/bin/arm-miyoo-linux-uclibcgnueabi-as"
export HOST="arm-miyoo-linux-uclibcgnueabi"
export LD="/opt/miyoo/bin/arm-miyoo-linux-uclibcgnueabi-ld"
export PREFIX="/opt/miyoo/"
export PLATFORM="rg35xx"
cd workspace
```

# Update Core
https://boosty.to/xquader  

```shell
/cfw/mnt/mmc/busybox chroot /cfw /bin/sh
chmod 0755 /usr/bin/pstree
export PATH=/bin:/usr/bin:$PATH
```

Tanya ke Johanes:
1. cara install pstree

```shell
/ # ldd /usr/bin/pstree
checking sub-depends for 'not found'
checking sub-depends for 'not found'
        libtinfo.so.6 => not found (0x00000000)
        libc.so.6 => not found (0x00000000)
        /lib/ld-linux-armhf.so.3 => /lib/ld-linux-armhf.so.3 (0x00000000)
/ # ldd /usr/bin/lua
        liblua.so.5.1.5 => /usr/lib//liblua.so.5.1.5 (0xb6f12000)
        libc.so.0 => /lib//libc.so.0 (0xb6e74000)
        ld-uClibc.so.1 => /lib/ld-uClibc.so.0 (0xb6f41000)
```

# Build SDL 1.2 in Koriki Dev
```shell
git clone https://github.com/libsdl-org/SDL-1.2.git
cd SDL-1.2
./autogen.sh
./configure --host=x86_64-pc-linux-gnu --prefix=/opt/rg35xx/arm-buildroot-linux-gnueabihf/sysroot/usr
chmod a+w sdl.pc
nano sdl.pc (LINE 3 => prefix=/usr)
make
make install

git clone -b SDL-1.2 https://github.com/libsdl-org/SDL_ttf.git
cd SDL_ttf
./autogen.sh
./configure --host=x86_64-pc-linux-gnu --prefix=/opt/rg35xx/arm-buildroot-linux-gnueabihf/sysroot/usr
chmod a+w SDL_ttf.pc
nano SDL_ttf.pc (LINE 3 => prefix=/usr)
make
make install

git clone -b SDL-1.2 https://github.com/libsdl-org/SDL_image.git
cd SDL_image
./autogen.sh
./configure --host=x86_64-pc-linux-gnu --prefix=/opt/rg35xx/arm-buildroot-linux-gnueabihf/sysroot/usr
chmod a+w SDL_image.pc
nano SDL_image.pc (LINE 3 => prefix=/usr)
make
make install

```

# HACK
```
enable write for StockOS mount -o remount,rw /dev/block/actc /system
/system/appres/bin/switch_os.sh
```

# Fix ADB in Stock OS
Download:
https://www.dropbox.com/scl/fi/336v1carp3aqm0bu92j80/rootfs.tar.gz?rlkey=5hnr6a7qdzcuttopvc0a4yvif&dl=0
```
adb push rootfs.tar.gz /mnt/mmc
adb shell
```
inside adb shell:

```
cd /mnt/data/
busybox tar -xf /mnt/mmc/rootfs.tar.gz
```

Start chroot

```
mount -o bind /dev /mnt/data/root/dev
mount -o bind /proc /mnt/data/root/proc
busybox chroot /mnt/data/root /bin/bash
export PATH=/bin:/usr/bin
```


## Building rootfs

create this file:
```
[General]
cleanup=true
noauth=false
unpack=true
bootstrap=Debian
aptsources=Debian

[Debian]
packages=kmod dbus
packages=nano dosfstools psmisc binutils
source=http://deb.debian.org/debian
keyring=debian-archive-keyring
suite=stable
components=main contrib non-free
```

Add or remove packages that you want (see `packages=`)

```
apt-get install multistrap
multistrap -a armhf -d $PWD/root -f multistrap.conf
tar -zcf rootfs.tar.gz root 
```


