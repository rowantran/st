# Maintainer: Rowan-James Tran <rowanjames.tran@gmail.com>

pkgname=st
pkgver=0.8.2
pkgrel=4
pkgdesc="Simple terminal emulator from Suckless"
arch=('x86_64')
url="https://st.suckless.org"
license=('MIT')
depends=('libxft')
makedepends=('ncurses')

_patches=("st-alpha-1-$pkgver.diff"
          "st-alpha-2-$pkgver.diff"
          "st-scrollback-$pkgver.diff"
          "st-scrollback-mouse-$pkgver.diff"
          "st-scrollback-mouse-altscreen-$pkgver.diff")
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
         '768e0225d8862785de5754fe537e7208'
         'c219705aa98be69d1707597aece765ac'
         '80f73f631ff89720664945cc2b21da4c'
         '939ad5870f6c2d50e2110f09dc44a2de'
         'e8d2c7fca59c3c0f322e7f832029e4e3'
         '47fa64e3ea047fb9184caa01a3e2e86e')
