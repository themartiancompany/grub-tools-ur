# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>

# shellcheck disable=SC2034
_git=false
_offline=false
_proj="hip"
_pkg="grub"
pkgname="${_pkg}-tools"
pkgver=0.1.1.1.1.1.1.1
_commit='f1c97242edfc2a6b74543f75de4a592904f80342'
pkgrel=1
_pkgdesc=(
  'Produces a standalone GRUB binary.'
  'compatible with Life systems.'
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
license=(
  'AGPL3'
)
_gh="https://github.com"
_arch="https://gitlab.archlinux.org"
_arch_ns="tallero"
_gh_ns="themartiancompany"
_ns="${_gh_ns}"
_http="${_gh}"
url="${_http}/${_ns}/${pkgname}"
_local="file://${HOME}/${pkgname}"
depends=(
  'bash'
  "${_pkg}"
  'libcrash-bash'
)
provides=(
  "arch-${_pkg}=${pkgver}"
  "mk${_pkg}=${pkgver}"
  "mk${_pkg}cfg=${pkgver}"
)
makedepends=(
  "make"
)
groups=(
  "${_proj}"
)
checkdepends=(
  'shellcheck'
)
optdepends=(
  'luks-tools: Format LUKS volume in a GRUB compatible format'  
  'shfmt: to produce indented GRUB configuration files'
)
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${pkgname}-${_tag}"
[[ "${_offline}" == "true" ]] && \
  _url="file://${HOME}/${pkgname}"
if [[ "${_git}" == true ]]; then
  makedepends+=(
    "git"
  )
  _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
  _sum="SKIP"
fi
if [[ "${_git}" == false ]]; then
  if [[ "${_tag_name}" == 'pkgver' ]]; then
    _src="${_tarname}.tar.gz::${_url}/archive/refs/tags/${_tag}.tar.gz"
    _sum="d4f4179c6e4ce1702c5fe6af132669e8ec4d0378428f69518f2926b969663a91"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _src="${_tarname}.zip::${_url}/archive/${_commit}.zip"
    _sum='079dd907a123fe29d3249e21d648f4fe29b9f719d8b3b59642cf493dd81b1bf7'
  fi
fi
source=(
  "${_src}"
)
sha256sums=(
  "${_sum}"
)


check() {
  make \
    -k check \
    -C \
      "${pkgname}-${pkgver}"
}

# shellcheck disable=SC2134
package() {
  make \
    DESTDIR="${pkgdir}" \
    PREFIX="/usr" \
    install \
      -C \
        "${pkgname}-${_tag}"
}

# vim:set sw=2 sts=-1 et:
