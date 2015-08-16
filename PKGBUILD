

pkgname=mingw-w64-taglib-static
pkgver=1.9.1
pkgrel=2
pkgdesc="A Library for reading and editing the meta-data of several popular audio formats (mingw-w64, static)"
arch=(any)
url="http://taglib.github.com"
license=("GPL")
makedepends=('mingw-w64-cmake')
depends=('mingw-w64-crt' 'mingw-w64-zlib')
conflicts=('mingw-w64-taglib')
provides=('mingw-w64-taglib')
options=('!strip' '!buildflags' 'staticlibs')
source=http://taglib.github.io/releases/taglib-1.9.1.tar.gz
md5sums=('0d35df96822bbd564c5504cb3c2e4d86')
_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  cd "$srcdir/taglib-$pkgver"
  unset LDFLAGS
  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
    ${_arch}-cmake \
      -DBUILD_SHARED_LIBS:BOOL=OFF \
      -DENABLE_STATIC:BOOL=ON \
      -DWITH_ASF:BOOL=ON \
      -DWITH_MP4:BOOL=ON \
      ..
    make
    popd
  done
}

package() {

  for _arch in ${_architectures}; do
    cd "$srcdir/taglib-$pkgver/build-${_arch}"
    make DESTDIR="$pkgdir" install
    ${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a
  done
}

