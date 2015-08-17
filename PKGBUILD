# Maintainer: Daniel Wallace <danielwallace at gtmanfred dot com>
pkgname=virgo-git
pkgver=0.1.8.11.g8aa0688
pkgrel=1
pkgdesc="project for building an on-host agents"
arch=('i686' 'x86_64')
url="https://github.com/racker/virgo"
license=('GPL')
depends=()
makedepends=('python2' 'git')
source=("$pkgname::git://github.com/racker/virgo.git"
	"rackspace-monitoring-agent.service")
md5sums=('SKIP'
         'c9a510396f3010a32c547c2aff773333')
install=$pkgname.install

pkgver(){
  cd $srcdir/$pkgname
  git describe --tags --long | sed 's/^v//;s/-/./g'
}

prepare(){
  [[ ! -d $srcdir/python-path ]] && mkdir $srcdir/python-path
  ln -sf /usr/bin/python2 $srcdir/python-path/python
  export PATH="$srcdir/python-path:$PATH"
  cd $srcdir/$pkgname
  git submodule init
  git submodule update
}

build() {
  cd $srcdir/$pkgname
  ./configure --prefix=/usr PYTHON=python2
  make
}

package() {
  cd $srcdir/$pkgname
  make DESTDIR="$pkgdir/" install
  install -Dm644 $srcdir/rackspace-monitoring-agent.service $pkgdir/usr/lib/systemd/system/rackspace-monitoring-agent.service
}

# vim:set ts=2 sw=2 et:
