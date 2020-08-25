
Clone repository:

git clone https://github.com/bas-t/dvbloopback

cd dvbloopback

apt-get install linux-headers-`uname -r`
cp /usr/src/linux-headers-`uname -r`/include/media/dvbdev.h dvbloopback/
patch -p3 < 4.5-linux.patch
patch -p1 < Makefile-OutofTree.patch
make -C /lib/modules/`uname -r`/build M=$PWD/dvbloopback/ modules


apt-get source linux-source-5.4.0
cd linux-5.4.0
cp -v /usr/src/linux-headers-$(uname -r)/Module.symvers .
make oldconfig
make prepare
make scripts
mv -v /lib/modules/$(uname -r)/kernel/drivers/media/dvb-core/dvb-core.ko /lib/modules/$(uname -r)/kernel/drivers/media/dvb-core/dvb-core.ko.backup

patch -p0 < 3.13-dvb-core.patch
cd drivers/media/dvb-core/
make -C /lib/modules/$(uname -r)/build M=$(pwd) modules
make -C /lib/modules/$(uname -r)/build M=$(pwd) modules_install


