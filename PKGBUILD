# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Justin Dray <justin@dray.be>
# Contributor: Alexander Rødseth <rodseth@gmail.com>
# Contributor: lang2 <wenzhi.liang@gmail.com>

pkgbase=python-pycparser
pkgname=(python-pycparser python2-pycparser)
pkgver=2.13
pkgrel=1
pkgdesc='C parser and AST generator written in Python'
url='https://github.com/eliben/pycparser'
makedepends=('python-ply' 'python2-ply' 'git')
arch=('any')
license=('BSD')
source=("https://github.com/eliben/pycparser/archive/release_v$pkgver.zip")
sha256sums=('93d5a52d802dfe9f8724fdeb4446b689eabf2e6a817e390c34cc5b2cd6cddf6e')

prepare() {
  cp -a pycparser-release_v${pkgver}{,-py2}
}

build() {
  cd pycparser-release_v${pkgver}
  python setup.py build

  cd pycparser
  python _build_tables.py

  cd "$srcdir/pycparser-release_v${pkgver}-py2"
  python2 setup.py build

  cd pycparser
  python2 _build_tables.py
}

package_python-pycparser() {
  depends=('python-ply')

  cd pycparser-release_v${pkgver}

  python setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_python2-pycparser() {
  depends=('python2-ply')

  cd pycparser-release_v${pkgver}-py2

  python2 setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
