# Maintainer: Josko Nikolic <dinamo DOT forever AT gmail DOT com>
pkgname=lqt-git
pkgver=20130706
pkgrel=1
pkgdesc="Automated Lua 5.1 binding generated from the Qt4 headers"
arch=('i686' 'x86_64')
url="https://github.com/mkottman/lqt"
license=('MIT')
depends=('qt4' 'lua51')
makedepends=('git' 'cmake')
conflicts=('lqt')
provides=('lqt')
source=(remove_signalslot_debug.patch)
md5sums=('df155e7b7989eecae37d40a575203a40')

_gitroot="https://github.com/mkottman/lqt.git"
_gitname="lqt-master"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server..."
  if [ -d "$_gitname" ] ; then
    cd "$_gitname" && git pull origin
    cd "$srcdir"
    msg "The local files are updated."
  else
    git clone --depth=1 "$_gitroot" "$_gitname"
  fi
  msg "GIT checkout done or server timeout"
  msg "Starting make..."
  
  rm -rf ${srcdir}/${_gitname}-build
  cp -r ${srcdir}/${_gitname} ${srcdir}/${_gitname}-build
  patch -p1 -i $srcdir/remove_signalslot_debug.patch
  cd ${_gitname}-build
  cmake . -DLUA_INCLUDE_DIR="/usr/include/lua5.1"
  make
}

package() {
  install -d "$pkgdir/usr/lib/lua/5.1"
  install -Dm755 $srcdir/${_gitname}-build/lib/{qtcore.so,qtgui.so,qtnetwork.so,qtopengl.so,qtscript.so,qtsql.so,qtsvg.so,qtuitools.so,qtwebkit.so,qtxml.so,qtxmlpatterns.so} "$pkgdir/usr/lib/lua/5.1"
}
