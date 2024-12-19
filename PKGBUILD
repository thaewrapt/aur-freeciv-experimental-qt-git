# $Id$
# Maintainer: Alexey Ugnichev <alexey.ugnichev@gmail.com>

pkgname=freeciv-experimental-qt-git
pkgver=3.2.92.7.fbf34300c6
pkgrel=1
pkgdesc="A multiuser clone of the famous Microprose game of Civilization, experimental AI modules, Qt client only (git version)"
url="http://www.freeciv.org/"
license=('GPL')
arch=('x86_64')
depends=(
	'qt6-base'
	'sqlite'
	'curl'
	'libtool'
	'icu'
	'hicolor-icon-theme'
	'sdl2_mixer'
	'libpulse'
	'gettext'
	'xz'
	'zlib'
	'zstd'
	'lua'
	'bzip2'
)
makedepends=('python' 'git')
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

	mkdir .build
	cd .build

	../autogen.sh \
		--prefix=/usr \
		--sysconfdir=/etc \
		--enable-client=qt \
		--enable-gitrev \
		--enable-aimodules=experimental \
		--enable-fcmp=qt,cli \
		--with-readline \
		--with-gnu-ld \
		--enable-sys-lua \
		--enable-fcdb=sqlite3 \
		--enable-ack-legacy \
		--enable-shared

	make
}

package() {
	cd "${srcdir}/${pkgname}"

	cd .build

	make DESTDIR=${pkgdir} install
}

