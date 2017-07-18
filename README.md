This is a modified version of the driver from here:

http://www.tp-link.com/us/download/TL-WN722N.html#Driver

http://static.tp-link.com/TL-WN722N(US)_V2_161112_Linux.zip

# Warning - Experimental
I'm not an experienced driver or kernel programmer.  Use at your own risk.

It's not picking up any wireless N networks, but seems to be working with 2.4ghz networks.

Instructions, tested on Fedora 26 with kernel = branch name.

I'm using a TP-Link TL-WN722N version 2.1.

```
dnf install kernel-devel
```

You're going to need compilers and whatnot.  This stuff is already installed on default fedora workstation image.


cd into your kernel source.

```
cd /usr/src/kernels/$(uname -r)
export KSRC=$PWD
```

```
export USER_EXTRA_CFLAGS="-Wno-incompatible-pointer-types"
make
sudo make install
sudo modprobe 8188eu
```

With any luck, you should now have a working wireless device.  As soon as I loaded
the module on my system, Ubuntu picked up the wireless networks.
