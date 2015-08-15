# $Id: PKGBUILD 68747 2012-04-01 10:46:48Z rvanharen $
# Maintainer: Ronald van Haren <ronald.archlinux.org>
# Contributor: Ronald van Haren <ronald.archlinux.org>

pkgname=evas-generic-loaders-svn
pkgver=71222
pkgrel=1
pkgdesc="Generic loaders for evas"
arch=('i686' 'x86_64')
groups=('e17-extra-svn')
url="http://www.enlightenment.org"
license=('BSD')
depends=('evas-svn' 'eina-svn' 'poppler' 'cairo' 'libspectre' 'libraw' 'librsvg')
makedepends=('svn')
conflicts=('evas-generic-loaders')
provides=('evas-generic-loaders')
replaces=('emprint-cvs')
options=('!libtool')
source=()
md5sums=()

_svntrunk="http://svn.enlightenment.org/svn/e/trunk/evas_generic_loaders"
_svnmod="evas-generic-loaders"

build() {
   cd $srcdir

  msg "Connecting to $_svntrunk SVN server...."
  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  cp -r $_svnmod $_svnmod-build
  cd $_svnmod-build
  
  ./autogen.sh --prefix=/usr
  make
}

package() {
  cd $srcdir/$_svnmod-build

  make DESTDIR=$pkgdir install

# install license files
  install -Dm644 $srcdir/$_svnmod-build/COPYING \
        $pkgdir/usr/share/licenses/$pkgname/COPYING

  rm -r $srcdir/$_svnmod-build

}
