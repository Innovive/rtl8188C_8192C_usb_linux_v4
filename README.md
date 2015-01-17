# Realtek 8192CU drivers for Linux

Configured to be cross compiled to PXA2XX platform with debug statements greatly reduced.

Tested with the Edimax EW-7811Un [Amazon link](http://www.amazon.com/gp/product/B003MTTJOY/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1) or TP-LINK TL-WN823N [Amazon link](http://www.amazon.com/gp/product/B0088TKTY2/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1).  The driver should load automatically when the USB wifi device is inserted.

## Compile

Export appropriate variables:

```
export ARCH=arm
export KVER=2.6.32.27
export KSRC=/mnt/src/device-os/kernel/cm-x300/build/linux-2.6.32.27
```

Run `make`.

The result is the kernel module file is 8192cu.ko, which is what will be installed on the device.

## Installing

```
MODULE_FILE=8192cu.ko
MODULE_DIR=/lib/modules/$(uname -r)/kernel/drivers/net/wireless
cp -v $MODULE_FILE $MODULE_DIR
depmod -a
```

To test that the module loads properly:

```
modprobe -v 8192cu
```

To verify the module is loaded:

```
lsmod | grep 8192cu
```

If the module is listed, you are good to go.  To unload the module (it will load automatically when necessary):

```
rmmod -v 8192cu
```

#### Misc.

To create md5 checksum file:

```
md5sum 8192cu.ko > 8192cu.ko.md5
```

To verify md5 checksum:

```
md5sum --check 8192cu.ko.md5
```


