# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Contributor:  Chris Severance aur.severach aATt spamgourmet dott com

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
_pkg="pathspec"
pkgname="${_py}-${_pkg}"
pkgver=0.12.1
pkgrel=1
pkgdesc='Utility library for gitignore style pattern matching of file paths'
arch=('any')
_http="https://github.com"
_ns="cpburnz"
url="${_http}/${_ns}/${pkgname}"
license=(
  'MPL2'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  'git'
  "${_py}-build"
  "${_py}-flit-core"
  "${_py}-installer"
  "${_py}-wheel"
)
source=(
  "git+${url}.git#tag=v${pkgver}"
)
b2sums=(
  'SKIP'
)

build() {
  cd \
    "${pkgname}"
  "${_py}" \
    -m build \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  cd $pkgname
  "${_py}" \
    -m unittest
}

package() {
  cd \
    "${pkgname}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  # Symlink license file
  local \
    site_packages=$( \
      python \
        -c \
	"import site; print(site.getsitepackages()[0])")
  install \
    -d \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${site_packages}/${_pkg}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
# vim: ft=sh syn=sh et
