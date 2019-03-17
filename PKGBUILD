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

sha256sums=('b53849dbc60109a987d7a49b8da197305c29307fd74c12dc18af0d3044392e6a'
            '97c09fd6f7e0aff3002a24dabe57798bcfaa1467a043cf7b7119177f005e5848'
            '0d5508c24ab2e870f1d807044c08c7c4f835e696267ecca7521b08f59bc803d1'
            'e4f1401e0f6a2615e3c1a6ab204e84b83917388d77247c311bf7902f1245b373'
            '1c46c67980e367321b3d243f843cd34465a2c7dff242b79e1f07b3a5e434e13b')

_patches=("slock-dpms-20170923-fa11589.diff"
          "local-quickcancel-20160619-65b8d52.diff"
          "local-mediakeys-20170111-2d2a21a.diff"
          #"slock-message-20180626-35633d4.diff"
          #"slock-1.2-background-image.diff"
        )

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

