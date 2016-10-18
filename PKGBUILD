# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Justin Dray <justin@dray.be>
# Contributor: Alexander Rødseth <rodseth@gmail.com>
# Contributor: lang2 <wenzhi.liang@gmail.com>

pkgbase=python-pycparser
pkgname=(python-pycparser python2-pycparser)
pkgver=2.15
_commit=9e9855b3254a8e234ac8f793154d600905b90a55
pkgrel=1
pkgdesc='C parser and AST generator written in Python'
url='https://github.com/eliben/pycparser'
makedepends=('python-ply' 'python2-ply' 'python-setuptools' 'python2-setuptools' 'git')
arch=('any')
license=('BSD')
source=("git+https://github.com/eliben/pycparser.git#commit=$_commit")
sha256sums=('SKIP')

prepare() {
  cp -a pycparser{,-py2}
}

build() {
  cd "$srcdir"/pycparser
  python setup.py build
  cd pycparser
  python _build_tables.py

  cd "$srcdir"/pycparser-py2
  python2 setup.py build
  cd pycparser
  python2 _build_tables.py
}

check() {
  cd "$srcdir"/pycparser
  python tests/all_tests.py

  cd "$srcdir"/pycparser-py2
  python2 tests/all_tests.py
}

package_python-pycparser() {
  depends=('python-ply')

  cd pycparser

  python setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-pycparser() {
  depends=('python2-ply')

  cd pycparser-py2

  python2 setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
