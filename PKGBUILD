# Maintainer:  Petr Mrázek <peterix@gmail.com>
pkgname=multimc-bin
pkgver=1.6
pkgrel=3
pkgdesc="Free, open source launcher and instance manager for Minecraft."
arch=('i686' 'x86_64')
url="http://multimc.org/"
license=('Apache')
depends=('zlib' 'opengl-driver' 'qt5-base' 'qt5-x11extras' 'qt5-svg' 'xorg-xrandr' 'zenity' 'wget')
conflicts=('multimc' 'multimc5' 'multimc5-git')
provides=('multimc' 'multimc5' 'multimc5-git')
source=("$pkgname-$pkgver.deb::https://files.multimc.org/downloads/multimc_$pkgver-1.deb"
        "https://raw.githubusercontent.com/MultiMC/Launcher/f45f83173662ea8d28a6d69a5312679df76d762b/launcher/package/ubuntu/multimc/usr/share/man/man1/multimc.1"
        'desktop-icon.patch')
sha1sums=('b943427e5f32f6a41d77a373029731c67571901d'
          'b4f1dfc021fbf6be22b066734364a1f87ed37214'
          '3553ee496ae3327bc6878b455226f7df973ccf37')
noextract=("$pkgname-$pkgver.deb")

prepare() {
    mkdir -p "$pkgname-$pkgver"
    bsdtar -xf $pkgname-$pkgver.deb -C "$pkgname-$pkgver"
    cd "$srcdir/$pkgname-$pkgver"
    bsdtar -xf data.tar.xz -C "$srcdir/$pkgname-$pkgver"

    # Patch the .desktop file to point to the icon in /usr/share/icons
    patch -p1 -i "${srcdir}/desktop-icon.patch"
}

package() {
    mkdir -p "$pkgdir/opt/multimc"
    mkdir -p "$pkgdir/usr/share/metainfo"
    mkdir -p "$pkgdir/usr/share/applications"
    mkdir -p "$pkgdir/usr/bin"
    mkdir -p "$pkgdir/usr/share/man/man1"
    mkdir -p "$pkgdir/usr/share/pixmaps"

    install -m644 -D "$srcdir/$pkgname-$pkgver/usr/share/applications/multimc.desktop" "$pkgdir/usr/share/applications/multimc.desktop"
    install -m644 -D "$srcdir/$pkgname-$pkgver/usr/share/metainfo/multimc.metainfo.xml" "$pkgdir/usr/share/metainfo/multimc.metainfo.xml"
    install -m644 -D "$srcdir/$pkgname-$pkgver/opt/multimc/icon.svg" "$pkgdir/usr/share/pixmaps/multimc.svg"
    install -m755 -D "$srcdir/$pkgname-$pkgver/opt/multimc/run.sh" "$pkgdir/opt/multimc/run.sh"
    install -m755 -D "$srcdir/multimc.1" "$pkgdir/usr/share/man/man1/multimc.1"
    ln -s "/opt/multimc/run.sh" "$pkgdir/usr/bin/multimc"
}
