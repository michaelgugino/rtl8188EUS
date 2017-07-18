Update:  Are you just looking for a working driver?  Give https://github.com/lwfinger/rtl8188eu a try.  LW Finger is a kernel maintainer, the software should be much better than mine.

Please refer to the branches for different versions of this software.

master:  Ubuntu 16.04 with 4.4.0

This is a modified version of the driver from here:

http://www.tp-link.com/us/download/TL-WN722N.html#Driver

http://static.tp-link.com/TL-WN722N(US)_V2_161112_Linux.zip

# Warning - Experimental
I'm not an experienced driver or kernel programmer.  Use at your own risk.

It's not picking up any wireless N networks, but seems to be working with 2.4ghz networks.

Instructions, tested on Ubuntu 16.04 with 4.4.0-59-generic #80-Ubuntu SMP

I'm using a TP-Link TL-WN722N version 2.1.

```
apt-get install linux-headers-$(uname -r)
apt-get install binutils
apt-get source linux-image-$(uname -r) # this will download source to PWD
apt-get build-essential
```

There may be one or two packages I missed, but that should cover most of it.


cd into your kernel source.

```
cp /usr/src/linux-headers-$(uname -r)/Module.symvers .
cp /boot/config-$(uname -r) .config
# Export the path where you downloaded the source.
export KSRC=$PWD
```

The following commands may be necessary, I haven't tested on a clean system
(they don't appear necessary as I've run make clean in the kernel tree.)
```
make prepare
make scripts
```


cd back to this project.

```
make
sudo make install
sudo modprobe -f 8188eu
sudo modprobe 8188eu
```

With any luck, you should now have a working wireless device.  As soon as I loaded
the module on my system, Ubuntu picked up the wireless networks.
