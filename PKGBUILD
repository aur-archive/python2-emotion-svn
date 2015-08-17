# Maintainer: Doug Newgard <scimmia22 at outlook dot com>

pkgname=python2-emotion-svn
pkgver=76210
pkgrel=4
pkgdesc="Python2 bindings for Emotion"
arch=('i686' 'x86_64')
url="http://www.enlightenment.org"
license=('LGPL2.1')
depends=('python2-evas-svn')
makedepends=('subversion' 'cython2')
conflicts=('python2-emotion')
provides=('python2-emotion')
options=('!libtool' '!emptydirs')

_svntrunk="http://svn.enlightenment.org/svn/e/trunk/BINDINGS/python/python-emotion/"
_svnmod="python-emotion"

build() {
  cd "$srcdir"

  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  svn export "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  PYTHON=/usr/bin/python2 \
  ./autogen.sh --prefix=/usr

  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir" install

  rm -r "$srcdir/$_svnmod-build"
}
