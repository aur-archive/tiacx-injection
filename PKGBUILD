# Maintainer: Thomas Schneider <maxmusterm@gmail.com>

pkgname=tiacx-injection
pkgver=20080210
pkgrel=3
pkgdesc="OpenSource module for Texas Instruments ACX100/ACX111 wireless chips. For stock arch 2.6 kernel with injection support for aircrack-ng"
arch=(i686 x86_64)
url="http://acx100.sourceforge.net/"
license=('MPL')
depends=('wireless_tools' 'kernel26>=2.6.27' 'kernel26<2.6.28' 'tiacx-firmware')
install=acx.install
conflicts=('tiacx')
source=(http://downloads.sourceforge.net/sourceforge/acx100/acx-$pkgver.tar.bz2
        kernel-2.6.27.patch
	http://patches.aircrack-ng.org/acx-20070101.patch)
md5sums=('7d5ce3215708e4e9f95cf567a9ee3a12'
         '9895f72f8d0c84956b0f6c3b16df0fe8'
	 '786344c994b8e36c91b2d81490c770b1')

_kernver=2.6.27-ARCH

build() {
    cd $startdir/src/acx-$pkgver
    patch -Np1 -i ../acx-20070101.patch || return 1
    patch -Np1 -i ../kernel-2.6.27.patch || return 1
    make -C /lib/modules/${_kernver}/build M=`pwd` || return 1
    install -D acx.ko $startdir/pkg/lib/modules/${_kernver}/kernel/drivers/net/wireless/tiacx/acx.ko
    sed -i -e "s/KERNEL_VERSION='.*'/KERNEL_VERSION='${_kernver}'/" $startdir/*.install
}
