# Maintainer: Christoph Haag <haagch at studi.informatik.uni-stuttgart.de>

pkgname=lib32-libglu
pkgver=20120902
pkgrel=1
pkgdesc="GL utility library for mesa builds from git after 2012-08-31"
arch=('x86_64')
url="http://mesa.freedesktop.org/"
license=('LGPL')
depends=('lib32-libgl' 'lib32-gcc-libs')
makedepends=('lib32-mesa')
options=(!libtool)

_gitroot="git://cgit.freedesktop.org/mesa/glu/"
_gitname="glu"

build() {
  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  msg "Connecting to the Freedesktop.org GIT server...."
  if [[ -d "${srcdir}/${_gitname}" ]] ; then
    cd "${_gitname}" &&  git pull origin
    msg "The local files are updated..."
  else
    git clone "${_gitroot}" --depth=1
  fi

  msg "GIT checkout done."
  msg "Starting make for: ${pkgname}"

  msg "Cleaning the previous build directory..."
  rm -rf "${srcdir}/${_gitname}-build"
  cp -r "${srcdir}/${_gitname}" "${srcdir}/${_gitname}-build"

  cd "${srcdir}/${_gitname}-build"

  msg "Starting configure..."

  ./autogen.sh --prefix=/usr --libdir=/usr/lib32
  make
}

package() {
  cd "${srcdir}/${_gitname}-build"
  make DESTDIR="${pkgdir}" install
  rm -rf ${pkgdir}/usr/include/ || true
}
