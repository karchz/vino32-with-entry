# Maintainer: kaz <kaz@geeks-dev.com>

_pkgname=vino
pkgname=${_pkgname}38-with-entry
pkgver=3.8.0
pkgrel=1
pkgdesc="a VNC server for the desktop with config tool (vino legacy version)"
arch=('i686' 'x86_64')
license=('GPL')
depends=('libnotify' 'libxtst' 'libsm' 'libsoup' 'telepathy-glib' 'gtk3' 'libsecret' 'avahi' 'desktop-file-utils')
makedepends=('intltool' 'networkmanager' 'gnome-common')
provides=("vino=${pkgver}")
conflicts=('vino' 'vino38')
url="http://www.gnome.org"
options=(!emptydirs)
source=("http://ftp.gnome.org/pub/gnome/sources/${_pkgname}/${pkgver%.*}/${_pkgname}-$pkgver.tar.xz")
sha256sums=('be665ff7a76076902a84cab69e7c3a6a7ddf2c634cc648aa35189895eefaac28')

build() {
  cd ${_pkgname}-$pkgver
  sed -i -e '/AC_PATH_XTRA/d' configure.ac
  autoreconf -fi
  ./configure --prefix=/usr --sysconfdir=/etc \
      --libexecdir=/usr/lib/vino \
      --localstatedir=/var \
      --disable-http-server --with-secret
  make
}

package() {
  cd ${_pkgname}-$pkgver
  make DESTDIR="$pkgdir" install
  sed -i -e '/OnlyShowIn/d' "$pkgdir/usr/share/applications/vino-preferences.desktop"
  sed -i -e '/OnlyShowIn/d' "$pkgdir/etc/xdg/autostart/vino-server.desktop"
}
