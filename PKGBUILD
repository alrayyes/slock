# Maintainer: Ryan Kes <alrayyes@gmail.com>

pkgname=slock
pkgver=1.4
pkgrel=3
pkgdesc="A simple screen locker for X"
arch=('x86_64')
url="http://tools.suckless.org/slock"
license=('MIT')
depends=('libxext' 'libxrandr')
source=("http://dl.suckless.org/tools/$pkgname-$pkgver.tar.gz")
#source=("slock-$pkgver.tar.bz2::http://hg.suckless.org/slock/archive/$_pkgver.tar.gz")
md5sums=('f91dd5ba50ce7bd1842caeca067086a3'
         '76c1d90cfb0a1da62a00caec951f48f7'
         '2afeace988ef4eaf0a8a078aded7c4a0')
sha256sums=('b53849dbc60109a987d7a49b8da197305c29307fd74c12dc18af0d3044392e6a'
            '209c5e9954f38f6dae8cc32f7c79bc0351eee5210f943912d1ff0c7a305a355c'
            '0d5508c24ab2e870f1d807044c08c7c4f835e696267ecca7521b08f59bc803d1')

_patches=("slock-dpms-20170923-fa11589.diff")

source=("http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz"
        "config.h"
        "${_patches[@]}")


prepare() {
  cd "$srcdir/slock-$pkgver"
  sed -i 's|static const char \*group = "nogroup";|static const char *group = "nobody";|' config.def.h
  sed -ri 's/((CPP|C|LD)FLAGS) =/\1 +=/g' config.mk

  for patch in "${_patches[@]}"; do
    echo "Applying patch $(basename $patch)..."
    patch -Np1 -i "$srcdir/$(basename $patch)"
  done

  cp $srcdir/config.h config.h
}

build() {
  cd "$srcdir/slock-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "$srcdir/slock-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

