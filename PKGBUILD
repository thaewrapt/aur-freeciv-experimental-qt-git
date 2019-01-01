# $Id$
# Maintainer: Alexey Ugnichev <alexey.ugnichev@gmail.com>

pkgname=freeciv-qt-git
pkgver=3.0.91.085354a262
pkgrel=1
pkgdesc="A multiuser clone of the famous Microprose game of Civilization, Qt client only (git version)"
url="http://www.freeciv.org/"
license=('GPL')
arch=('x86_64')
depends=(
  'qt5-base'
  'gtk3'
  'lua'
  'sqlite'
  'curl'
  'libtool'
  'icu'
  'hicolor-icon-theme'
  'sdl2_mixer'
  'libpulse'
  'gettext'
)
makedepends=('python' 'git' 'autoconf' 'automake' 'make' 'gcc')
backup=('etc/freeciv/database.lua')
conflicts=('freeciv')
provides=('freeciv')
source=("${pkgname}::git+https://github.com/freeciv/freeciv.git")
sha256sums=('SKIP')

pkgver() {
  cd "${srcdir}/${pkgname}"

  VERSION_REVTYPE=git ./fc_version | sed 's/-dev+/./'
}

build() {
  cd "${srcdir}/${pkgname}"

  ./autogen.sh \
    --prefix=/usr \
    --sysconfdir=/etc \
    --enable-sys-lua \
    --enable-client=qt \
    --enable-gitrev \
    --enable-aimodules=experimental \
    --enable-fcmp=qt,cli \
    --with-readline \
    --with-zoom \
    --with-gnu-ld \
    --with-liblzma \
    --enable-shared

  make
}

package() {
  cd "${srcdir}/${pkgname}"

  make DESTDIR=${pkgdir} install
}

