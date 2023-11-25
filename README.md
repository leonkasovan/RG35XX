# RG35XX
Knowledge for RG35XX Anbernic Device

# Firmware
Anbernic Stock: Dual OS https://win.anbernic.com/download/270.html  
Garlic OS: 1.4.9 https://www.patreon.com/posts/76561333  
Koriki OS: 1.0 https://github.com/rg35xx-cfw/Koriki/releases  

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
