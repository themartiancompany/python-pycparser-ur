# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Justin Dray <justin@dray.be>
# Contributor: Alexander Rødseth <rodseth@gmail.com>
# Contributor: lang2 <wenzhi.liang@gmail.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=pycparser
pkgname="${_py}-${_pkg}"
pkgver=2.22
pkgrel=2
_pkgdesc=(
  'C parser and AST generator'
  'written in Python'
)
pkgdesc="${_pkgdesc[*]}"
_http="https://github.com"
_ns="eliben"
url="${_http}/${_ns}/${_pkg}"
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}setuptools"
)
arch=(
  'any'
)
license=(
  'BSD'
)
_tarname="${_pkg}-release_v${pkgver}"
source=(
  "${_tarname}.tar.gz::${url}/archive/release_v${pkgver}.tar.gz"
)
sha512sums=(
  '1c5be2b83c0a892cafa55a2595942d7048994772dc0fc71d2943004b4198d939c0bf2a164d763d94fe11d532e49371c59c1cf4037c32dab8d3cf0c553a8de64a'
)

build() {
  cd \
    "${_tarname}"
  "${_py}" \
    "setup.py" \
    build
  cd \
    "${_pkg}"
  "${_py}" \
    "_build_tables.py"
}

check() {
  cd \
    "${_tarname}"
  "${_py}" \
    -m \
      unittest \
    discover
}

package() {
  cd \
    "${_tarname}"
  "${_py}" \
    "setup.py" \
      install \
        --root="${pkgdir}" \
	--optimize=1
  install \
    -Dm644 \
    "LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
