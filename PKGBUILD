pkgname=bullet
_pkgname=bullet3
pkgver=2.83.7
pkgrel=1
pkgdesc="A 3D Collision Detection and Rigid Body Dynamics Library for games and animation"
arch=('x86_64')
url="http://www.bulletphysics.com/Bullet/"
license=('custom:zlib')
makedepends=('cmake' 'doxygen' 'graphviz' 'ttf-dejavu' 'mesa' 'glu')
source=("https://github.com/bulletphysics/${_pkgname}/archive/${pkgver}.tar.gz")
md5sums=('39fd0138fcb59047c12861f3b65c063e')

build() {
  cd ${_pkgname}-${pkgver}

  [[ -d build ]] && rm -rf build
  mkdir build && cd build 

  cmake .. \
       -DCMAKE_INSTALL_PREFIX=/usr \
       -DBUILD_SHARED_LIBS=1 \
       -DINSTALL_LIBS=1 \
       -DINSTALL_EXTRA_LIBS=1 \
       -DCMAKE_BUILD_TYPE=Release

  make

  cd ..
  #sed -i 's/GENERATE_HTMLHELP.*//g' Doxyfile
  doxygen
}

package_bullet() {
  
  cd ${_pkgname}-${pkgver}/build

  make DESTDIR=${pkgdir} install

  install -Dm755 examples/ExampleBrowser/App_ExampleBrowser ${pkgdir}/usr/bin/${_pkgname}_examplebrowser
  install -Dm644 ../LICENSE.txt ${pkgdir}/usr/share/licenses/${pkgbase}/LICENSE
}
