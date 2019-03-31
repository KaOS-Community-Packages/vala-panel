
_pkgname=vala-panel
pkgname=${_pkgname}-git
_cmakename=cmake-vala
pkgver=0.4.87.r38.g5f4f6bd
pkgrel=1
pkgdesc="Gtk3 panel for compositing window managers"
url="https://gitlab.com/vala-panel-project/vala-panel"
arch=('x86_64')
license=('LGPL3')
depends=('gtk3' 'libwnck3')
makedepends=('cmake' 'vala')

source=("git+https://gitlab.com/vala-panel-project/${_pkgname}.git"
        "git+https://gitlab.com/vala-panel-project/${_cmakename}.git")
sha256sums=('SKIP'
            'SKIP')

pkgver() {
  cd "${srcdir}/${_pkgname}"
  ( set -o pipefail
    git describe --long --tags 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

prepare() {
  cd "${srcdir}/${_cmakename}"
  cp -r . "${srcdir}/${_pkgname}/cmake"
}

build() {
  cd "${srcdir}/${_pkgname}"
  cmake ./ -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=lib -DENABLE_WNCK=ON
  make
}

package() {
  cd "${srcdir}/${_pkgname}"
  make DESTDIR="${pkgdir}" install
}


