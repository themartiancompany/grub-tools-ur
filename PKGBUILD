# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>

# shellcheck disable=SC2034
_git=false
_offline=false
_proj="hip"
_pkg="grub"
pkgname="arch-${_pkg}"
pkgver=0.1.1.1.1.1.1
_commit="3356937a2dccfedca34e9e48a62586a4e2c995ea"
pkgrel=1
_pkgdesc=(
  'Produces a standalone GRUB binary'
  'compatible with Arch Linux.'
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
  "${_pkg}"
  bash
)
provides=(
  "mk${_pkg}=${pkgver}"
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
source=()
sha256sums=()
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${pkgname}-${_tag}"
[[ "${_offline}" == "true" ]] && \
  _url="file://${HOME}/${pkgname}"
[[ "${_git}" == true ]] && \
  makedepends+=(
    "git"
  ) && \
  source+=(
    "${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
  ) && \
  sha256sums+=(
    SKIP
  )
[[ "${_git}" == false ]] && \
  if [[ "${_tag_name}" == 'pkgver' ]]; then
    _tar="${_tarname}.tar.gz::${_url}/archive/refs/tags/${_tag}.tar.gz"
    _sum="d4f4179c6e4ce1702c5fe6af132669e8ec4d0378428f69518f2926b969663a91"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _tar="${_tarname}.zip::${_url}/archive/${_commit}.zip"
    _sum="41d0f776de3814d390fd6f8fd75fd1c217c7ff4b3c79953a855356c8652bd554"
  fi && \
    source+=(
      "${_tar}"
    ) && \
    sha256sums+=(
      "${_sum}"
    )
[[ "${_git}" == true ]] && \
  makedepends+=(
    'git'
  ) && \
  source+=(
    "${pkgname}::git+${_url}"
  ) && \
  sha256sums+=(
    'SKIP'
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
