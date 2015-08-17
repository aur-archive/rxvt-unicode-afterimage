# Maintainer: Erus_Ilùvatar <erus.iluvatar@gmail.com>

_pkgname=rxvt-unicode
pkgname=rxvt-unicode-afterimage
pkgver=9.15
pkgrel=1
pkgdesc="An unicode enabled rxvt-clone terminal emulator (urxvt), libafterimage enabled"
url="http://software.schmorp.de/pkg/rxvt-unicode.html"
arch=(i686 x86_64)
depends=('gcc-libs' 'libxft' 'libxpm' 'librsvg' 'libafterimage')
makedepends=('ncurses' 'perl>=5.10.0' 'pkgconfig')
optdepends=('perl: lots of utilities' 'gtk2-perl: to use the urxvt-tabbed')
conflicts=('rxvt-unicode-256color' 'rxvt-unicode')
license=("GPL")
source=(http://dist.schmorp.de/rxvt-unicode/${_pkgname}-${pkgver}.tar.bz2 \
        ${_pkgname}.desktop ${_pkgname}.png)

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
./configure --prefix=/usr \
--with-terminfo=/usr/share/terminfo \
--enable-font-styles \
--enable-xim \
--enable-warnings \
--enable-keepscrolling \
--enable-selectionscrolling \
--enable-smart-resize \
--enable-transparency \
--enable-utmp \
--enable-wtmp \
--enable-256-color \
--enable-lastlog \
--disable-pixbuf \
--enable-afterimage
#    --with-term=rxvt-256color \ // Use aur/rxvt-unicode-terminfo, because yeah, that's the clean way.
  make
  install -d "${pkgdir}/usr/share/terminfo"
  export TERMINFO="${pkgdir}/usr/share/terminfo"
  make DESTDIR="${pkgdir}" install || return 1
 # install the tabbing wrapper ( requires gtk2-perl! )
  sed -i 's/\"rxvt\"/"urxvt"/' doc/rxvt-tabbed || return 1
  install -Dm 755 doc/rxvt-tabbed "${pkgdir}/usr/bin/urxvt-tabbed" || return 1
 # install freedesktop menu and icon ( icon from cvs checkout )
  install -Dm644 ../${_pkgname}.desktop \
    "${pkgdir}/usr/share/applications/${_pkgname}.desktop"
  install -Dm644 ../${_pkgname}.png \
    "${pkgdir}/usr/share/pixmaps/${_pkgname}.png"
}
md5sums=('15595aa326167ac5eb68c28d95432faf'
         '5bfefa1b41c2b81ca18f2ef847330543'
         '84328cada91751df07324d95f8be4d1b')
sha512sums=('1095fb88502377fa669746bbe9a5597f0c748e2c01a468ce382e91236ed0e6f720f3ca7631f7105aa390afac09588b92cebd70589096b6a20f174c4297463b71'
            '2188d8802c4f3f9af71ebc83a4358af965f31f1fcaf423f6760e5879d895dcad2f27acad5fe6a0fadcff2765d0a44daeabef83edcefe244ecf1e2c511b4c0183'
            '82e69cca681877d1e4dd24315d037abf0b69e27f9161538613bce29001c4e579fb5c8a4804acecd406b46cdc72d33bb11ef43891e2e02cd9c1d12cfce3e8c1ba')
