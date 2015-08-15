# Maintainer: Freyermuth Julien <julien.chipster@archlinux.fr>
pkgname=dkms-mt7601u-latest
pkgver=v3.0.0.4
# pkgrel=4
pkgrel=5
pkgdesc="Driver for Ralink MT7601U chipset wireless adaptors"
arch=('any')
url="http://www.ralinktech.com"
license=('GPL')
depends=('dkms' 'linux-headers')
conflicts=()
install=${pkgname}.install
options=(!strip)
source=("http://www.mediatek.com/AmazonS3/Downloads/linux/DPO_MT7601U_LinuxSTA_3.0.0.4_20130913.tar.bz2"
        #"https://mt7601-openwrt.googlecode.com/hg/patches/001-DPO_MT7601U_LinuxSTA_3.0.0.4_20130913-Linux-3.17.0-v2.patch"
        "https://mt7601-openwrt.googlecode.com/hg/patches/002-rt2870-mt7601Usta-kuid_t-kgid_t.patch"
        #"https://mt7601-openwrt.googlecode.com/hg/patches/003-add-openwrt-platform.patch"
        #"https://mt7601-openwrt.googlecode.com/hg/patches/004-debug.patch"
        #"https://mt7601-openwrt.googlecode.com/hg/patches/006-big-endian.patch"
        #"https://mt7601-openwrt.googlecode.com/hg/patches/007-big-endian-fix.patch"
        #"https://mt7601-openwrt.googlecode.com/hg/patches/008-more-big-endiand-fixes.patch"
        "dkms.conf")

md5sums=('5f440dccc8bc952745a191994fc34699'
         'a12442972c9518aca6b063426d060de6'
         '95caf4e6ba262c9683867e207fe846d7')

#md5sums=('5f440dccc8bc952745a191994fc34699'
#         'bcc3e8c2a845f3b7c7e099406dddd8c2'
#         'a12442972c9518aca6b063426d060de6'
#         '9f941beec19826fd3eefb3039b5f2d30'
#         '75604a3e29332753b0dadde30e3c3260'
#         '638ce64712e8478d9c38333de10ae020'
#         'a1aecadafcea28b46613e8b203a82f4d'
#         '007700d40ebcf54ef7e15ce4fcd09898'
#         '95caf4e6ba262c9683867e207fe846d7')

prepare() {
    rm -rf ${srcdir}/$pkgname-$pkgver
    # Change src dir name
    mv ${srcdir}/DPO_MT7601U_LinuxSTA_3.0.0.4_20130913 ${srcdir}/$pkgname-$pkgver

    cd "${srcdir}/${pkgname}-${pkgver}/"
#    patch -Np1 -i ${srcdir}/001-DPO_MT7601U_LinuxSTA_3.0.0.4_20130913-Linux-3.17.0-v2.patch
    patch -Np1 -i ${srcdir}/002-rt2870-mt7601Usta-kuid_t-kgid_t.patch
#    patch -Np1 -i ${srcdir}/003-add-openwrt-platform.patch
#    patch -Np1 -i ${srcdir}/004-debug.patch
#    patch -Np1 -i ${srcdir}/006-big-endian.patch
#    patch -Np1 -i ${srcdir}/007-big-endian-fix.patch
#    patch -Np1 -i ${srcdir}/008-more-big-endiand-fixes.patch
}

build() {
    DATE=$(date +%d-%m-%Y);
    TIME=$(date +%z);

    #gcc 4.9 adds -Werror=date-time, which Linux has enabled in its build.
    cd "${srcdir}/${pkgname}-${pkgver}/"
    sed -i "s|__DATE__|\"$DATE\"|g" sta/sta_cfg.c
    sed -i "s|__TIME__|\"$TIME\"|g" sta/sta_cfg.c
}

package() {

    installDir="$pkgdir/usr/src/$pkgname-$pkgver"

    install -dm755 "$installDir"
    install -m644 "$srcdir/dkms.conf" "$installDir"
    install -dm755 "$pkgdir/etc/modprobe.d"

    cd "${srcdir}/${pkgname}-${pkgver}/"

    for d in `find . -type d`
    do
        install -dm755 "$installDir/$d"
    done

    for f in `find . -type f -o -type l`
    do
        install -m644 "${srcdir}/${pkgname}-${pkgver}/$f" "$installDir/$f"
    done
}
