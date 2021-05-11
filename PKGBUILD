# My own build of eccodes
# The AUR version is a model for this build file
## Maintainer: "Jan Kohnert <bughunter@jan-kohnert.de"
## Contributor: Graziano Giuliani <graziano.giuliani@poste.it>
# But with my own preferences. full options see:
# https://confluence.ecmwf.int/display/ECC/ecCodes+installation

pkgname=eccodes
pkgver=2.21.0
_attnum=45757960
pkgrel=2
pkgdesc="ECMWF decoding library for GRIB, BUFR and GTS"
arch=('i686' 'x86_64')
url="https://software.ecmwf.int/wiki/display/ECC/ecCodes+Home"
license=('Apache')
depends=('libaec' 'openjpeg2' 'netcdf')
makedepends=('gcc-fortran' 'cmake')
conflicts=('grib_api' 'libbufr-ecmwf')
source=(http://software.ecmwf.int/wiki/download/attachments/${_attnum}/${pkgname}-${pkgver}-Source.tar.gz)
sha512sums=('f2ba8361b99800646a92f5f5beb7ec2facf2ee3b8a3f7985d9681a23b2faae778004c8c688ebe4b3a8492e99c76422c66ecc8943d12d3342d5bc1d38362ccf06')
 
build() {
  cd "$srcdir"/${pkgname}-${pkgver}-Source
  mkdir -p build
  cd build
  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=RelWithDebInfo \
    -DCMAKE_INSTALL_DATAROOTDIR=/usr/share/$pkgname/definitions \
    -DCMAKE_INSTALL_DATADIR=/usr/share -DENABLE_AEC=ON \
    -DENABLE_PNG=1 -DENABLE_ECCODES_THREADS=1 \
    -DENABLE_JPG=1 -DENABLE_JPG_LIBOPENJPEG=1 \
    -DOPENJPEG_INCLUDE_DIR=`pkg-config --variable=includedir libopenjpeg` \
    -DENABLE_JPG_LIBJASPER=OFF ..
  make || return 1
}

package() {
  cd "$srcdir"/${pkgname}-${pkgver}-Source/build
  make DESTDIR="$pkgdir" install || return 1
}
