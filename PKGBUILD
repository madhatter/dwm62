# Maintainer: Arvid Warnecke <arvid.warnecke@gmail.com>

pkgname=dwm-git
_pkgname=dwm
pkgver=6.1.33.gb69c870
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft')
makedepends=('git')
install=dwm.install
provides=('dwm')
conflicts=('dwm')
epoch=1
source=(dwm.desktop
        "$_pkgname::git+http://git.suckless.org/dwm")
_patches=(dwm-alpha-20180613-b69c870.diff
          dwm-pertag.diff
          dwm-bottomstack.diff)
md5sums=('939f403a71b6e85261d09fc3412269ee'
         'SKIP'
         '4e5893e04c443530168223639c97bc47'
         '9f8c3a6ed9745856f05921837660df08'
         '77a365003af3b6a500cf05c573c88b04')
source=(${source[@]} ${_patches[@]})

pkgver(){
  cd $_pkgname
  git describe --tags |sed 's/-/./g'
}

prepare() {
  cd $_pkgname

  for p in "${_patches[@]}"; do
        echo "=> $p"
    patch < ../$p || return 1
  done

  if [[ -f "$SRCDEST/config.h" ]]; then
    cp -f "$SRCDEST/config.h" config.h
  fi
}

build() {
  cd $_pkgname
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $_pkgname
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D ../dwm.desktop "$pkgdir/usr/share/xsessions/dwm.desktop"
}

# vim:set ts=2 sw=2 et:
