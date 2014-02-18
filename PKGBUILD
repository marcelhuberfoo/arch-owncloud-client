# Maintainer: Kuba Serafinowski <zizzfizzix(at)gmail(dot)com>
# https://github.com/zizzfizzix/pkgbuilds

##############################################################
#### The section below can be adjusted to suit your needs ####
##############################################################

# What type of build do you want?
# See http://techbase.kde.org/Development/CMake/Addons_for_KDE#Buildtypes to check what is supported.
# Default is RelWithDebInfo to help with debugging.

_buildtype='Release'

##############################################################

_name=mirall
pkgname=owncloud-client
pkgver=1.5.1
pkgrel=1
pkgdesc='ownCloud client based on mirall'
arch=('i686' 'x86_64' 'armv7h')
url='http://owncloud.org/'
license=('GPL2')
depends=('qtkeychain' 'qtwebkit' 'neon')
makedepends=('cmake' 'pkgconfig')
provides=('mirall' 'owncloud-client')
conflicts=('mirall-git')
install=owncloud-client.install
backup=('etc/ownCloud/sync-exclude.lst')
source=("http://download.owncloud.com/desktop/stable/${_name}-${pkgver}.tar.bz2")
md5sums=('bedc635c26b7f84f4a6118b930cf6607')

if [[ ! ${_buildtype} == 'Release' ]] && [[ ! ${_buildtype} == 'release' ]]; then
  options=(!strip)
fi

prepare() {
  if [[ -e ${srcdir}/${_name}-${pkgver}-build ]]; then rm -rf ${srcdir}/${_name}-${pkgver}-build; fi
  mkdir ${srcdir}/${_name}-${pkgver}-build
}

build() {
  cd ${srcdir}/${_name}-${pkgver}-build

  cmake -DQT_QMAKE_EXECUTABLE=qmake-qt4 \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=/usr/lib \
    -DCMAKE_BUILD_TYPE=${_buildtype} \
    -DCMAKE_INSTALL_SYSCONFDIR=/etc/${pkgname} \
    ../${_name}-${pkgver}
  make
}

package() {
  cd ${srcdir}/${_name}-${pkgver}-build
  make DESTDIR=${pkgdir} install
}

# vim: set ts=2 sw=2 et:
