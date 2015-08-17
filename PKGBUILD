# Contributor: Serge Gielkens <gielkens_dot_serge_at_mumeli_dot_org>

# Developer tools and API information are not packaged

pkgname=ngplant
pkgver=0.9.10
pkgrel=0
pkgdesc="A plant modeling software package"
url="http://ngplant.sourceforge.net/"
depends=('wxgtk>=2.4' 'lua' 'glew' 'freeglut')
makedepends=('python2' 'scons')
source=(http://downloads.sourceforge.net/sourceforge/ngplant/${pkgname}-${pkgver}.tar.gz \
	scons.patch \
	${pkgname}.desktop) 
arch=('i686' 'x86_64')
license=('GPL' 'BSD')
md5sums=('4e406f4e17076f1b838aaadc5efba4ec' \
	'a26febd2204a1d41694d4597b20b772c' \
	'03a3792684cab8624c6267aa9b18383b')
install=$pkgname.install

build() {
  cd ${srcdir}/${pkgname}-${pkgver}

# Patch and build
  patch -Np0 -i ../scons.patch || return 1
  scons || return 1
}

package() {
  cd ${srcdir}/${pkgname}-${pkgver}

# Install programs
  install -d ${pkgdir}/usr/bin/
  install -m755 -t ${pkgdir}/usr/bin/ \
  	${srcdir}/${pkgname}-${pkgver}/ngplant/ngplant \
  	${srcdir}/${pkgname}-${pkgver}/ngpshot/ngpshot \
  	${srcdir}/${pkgname}-${pkgver}/ngpview/ngpview

# Install menu
  install -d ${pkgdir}/usr/share/pixmaps
  install -m644 ngplant/images/ngplant.xpm ${pkgdir}/usr/share/pixmaps/${pkgname}.xpm
  install -d ${pkgdir}/usr/share/applications
  install -m644 ../../${pkgname}.desktop ${pkgdir}/usr/share/applications/${pkgname}.desktop


# Install plugins
  install -d ${pkgdir}/usr/share/${pkgname}/plugins/
  install -m644 -t ${pkgdir}/usr/share/${pkgname}/plugins/ \
  	${srcdir}/${pkgname}-${pkgver}/plugins/*

# Install examples
  install -d ${pkgdir}/usr/share/${pkgname}/examples/textures/
  install -m644 -t ${pkgdir}/usr/share/${pkgname}/examples/ \
  	${srcdir}/${pkgname}-${pkgver}/samples/*.* 
  install -m644 -t ${pkgdir}/usr/share/${pkgname}/examples/textures/ \
  	${srcdir}/${pkgname}-${pkgver}/samples/textures/*.*
}

