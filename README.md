# rpi-rtl8188eu

Linux driver for tplink-wn725n nano wireless adapter.

## compile and install

1. get linux source code from github
	- `git clone --depth 1 git://github.com/raspberrypi/linux.git rpi-linux`
2. get fireware from github
	- `git clone --depth 1 git://github.com/raspberrypi/firmware.git rpi-firmware`
3. cd rpi-linux
	- `make mrproper`
	- `zcat /proc/config.gz > .config`
	- `make modules_prepare`
	- `cp /path/to/rpi-firmware/extra/Module.symvers .`
	- `cd /path/to/rtl-8188eu`
	- ``CONFIG_RTL8188EU=m make -C /path/to/rpi-linux M=`pwd` ``
4. copy 8188eu.ko to ``/lib/modules/`uname -r`/kernel/driver/net/wireless``
5. depmod -a
6. modprobe 8188eu
7. ifconfig and you can see the wlan interface :-)





cd
git clone https://github.com/liwei/rpi-rtl8188eu.git
git clone --depth 1 git://github.com/raspberrypi/linux.git rpi-linux
git clone --depth 1 git://github.com/raspberrypi/firmware.git rpi-firmware
cd rpi-linux
make mrproper
zcat /proc/config.gz > .config
make modules_prepare
cp ../rpi-firmware/extra/Module.symvers .
cd ../rpi-rtl8188eu
CONFIG_RTL8188EU=m make -C ../rpi-linux M=`pwd`
sudo rmmod 8188eu
sudo install -p -m 644 8188eu.ko /lib/modules/`uname -r`/kernel/drivers/net/wireless
sudo depmod -a
sudo modprobe 8188eu
