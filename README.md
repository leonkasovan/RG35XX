# RG35XX
Knowledge for RG35XX Anbernic Device

# Firmware
Anbernic Stock: Dual OS https://win.anbernic.com/download/270.html  
Garlic OS: 1.4.9 https://www.patreon.com/posts/76561333  
Koriki OS: 1.0 https://github.com/rg35xx-cfw/Koriki/releases  

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
make
make install
```
