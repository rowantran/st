# Maintainer: Rowan-James Tran <rowanjames.tran@gmail.com>

pkgname=st
pkgver=0.8.2
pkgrel=1
pkgdesc="Simple terminal emulator from Suckless"
arch=('x86_64')
url="https://st.suckless.org"
license=('MIT')
depends=('libxft')
makedepends=('ncurses')

_patches=("st-alpha-1-$pkgver.diff"
          "st-alpha-2-$pkgver.diff")
source=(http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz
        config.h
        "${_patches[@]}")

prepare() {
	cd $srcdir/$pkgname-$pkgver

    # Remove terminfo from Makefile
    sed -i '/tic /d' Makefile

    cp $srcdir/config.h config.h

    for patch in "${_patches[@]}"; do
        echo "Applying patch $(basename $patch)..."
        patch -Np1 -i "$srcdir/$(basename $patch)"
    done
}

build() {
    cd $srcdir/$pkgname-$pkgver
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd $srcdir/$pkgname-$pkgver
	make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}

md5sums=('a3d97ee92215071e6399691edc0f04b0'
         '7ea9dd38a5a290538c9ea6e2f5121b4a'
         'c219705aa98be69d1707597aece765ac'
         '80f73f631ff89720664945cc2b21da4c')
