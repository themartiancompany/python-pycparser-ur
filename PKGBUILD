# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Justin Dray <justin@dray.be>
# Contributor: Alexander Rødseth <rodseth@gmail.com>
# Contributor: lang2 <wenzhi.liang@gmail.com>

pkgbase=python-pycparser
pkgname=(python-pycparser python2-pycparser)
pkgver=2.12
pkgrel=1
pkgdesc='C parser and AST generator written in Python'
url='https://github.com/eliben/pycparser'
makedepends=('python-ply' 'python2-ply' 'git')
arch=('any')
license=('BSD')
source=("https://github.com/eliben/pycparser/archive/release_v$pkgver.zip")
sha256sums=('ac915295a2e0313c23d823aa3042ca7b20a88cdf5650a6581dc761627f9bb7f9')

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
