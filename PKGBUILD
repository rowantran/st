# Maintainer: Rowan-James Tran <rowanjames.tran@gmail.com>

pkgname=st
pkgver=0.8.2
pkgrel=6
pkgdesc="Simple terminal emulator from Suckless"
arch=('x86_64')
url="https://st.suckless.org"
license=('MIT')
depends=('libxft')
makedepends=('ncurses')

_patches=("st-alpha-$pkgver.diff"
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
         '1a6d4884ed0e4fe8df7df5e455a35d60'
         '96b75f11218ac1c510c86bc45333ccff'
         '939ad5870f6c2d50e2110f09dc44a2de'
         '8f3e642be09bbdfd8449c5eb0815fd56'
         '47fa64e3ea047fb9184caa01a3e2e86e')
