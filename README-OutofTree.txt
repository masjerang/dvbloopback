
Clone repository:

git clone https://github.com/bas-t/dvbloopback

cd dvbloopback

apt-get install linux-headers-`uname -r`
cp /usr/src/linux-headers-`uname -r`/include/media/dvbdev.h dvbloopback/
patch -p3 < 4.5-linux.patch
patch -p1 < Makefile-OutofTree.patch
make -C /lib/modules/`uname -r`/build M=$PWD/dvbloopback/ modules



