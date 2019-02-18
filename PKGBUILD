# Maintainer: Rowan-James Tran <rowanjames.tran@gmail.com>

pkgname=st
pkgver=0.8.2
pkgrel=1
pkgdesc="Simple terminal emulator from Suckless"
arch=('x86_64')
url="https://st.suckless.org"
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
source=(http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz
        config.h)

prepare() {
	cd $srcdir/$pkgname-$pkgver
    cp $srcdir/config.h config.h
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
