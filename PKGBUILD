# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Giancarlo Razzolini
#     <grazzolini@archlinux.org>
#   Frederik Schwan
#     <freswa at archlinux dot org>
#   Bartłomiej Piotrowski
#     <bpiotrowski@archlinux.org>
#   Allan McRae
#     <allan@archlinux.org>
#   Daniel Kozak
#     <kozzi11@gmail.com>

# toolchain build order:
#   linux-api-headers ->
#     glibc ->
#       binutils ->
#         gcc ->
#           glibc ->
#             binutils ->
#               gcc
# NOTE:
#   libtool requires rebuilt
#   with each new gcc version

if [[ ! -v "_os" ]]; then
  _os="$(
    uname \
      -o)"
fi
if [[ ! -v "_arch" ]]; then
  _arch="$(
    uname \
      -m)"
fi
if [[ ! -v "CHOST" ]]; then
  if [[ "${_arch}" == "x86_64" ]]; then
    CHOST="${_arch}-pc-linux-gnu"
  fi
fi

if [[ ! -v "_distro" ]]; then
  _distro="dogeos"
fi
if [[ ! -v "_git_service" ]]; then
  if [[ "${_distro}" == "archlinux" ]]; then
    _git_service="gitlab"
  elif [[ "${_distro}" == "dogeos" ]]; then
    _git_service="gitlab"
    _git_service="github"
  fi
fi
if [[ ! -v "_http_bugs" ]]; then
  if [[ "${_distro}" == "archlinux" ]]; then
    _http_bugs="https://gitlab.${_distro}.org"
  elif [[ "${_distro}" == "dogeos" ]]; then
    _http_bugs="https://${_git_service}.com"
  fi
fi
_proj=gnu
_pkg=gcc
if [[ ! -v "_ns" ]]; then
  if [[ "${_distro}" == "archlinux" ]]; then
    _ns="${_pkg}"
  elif [[ "${_distro}" == "dogeos" ]]; then
    _ns="themartiancompany"
  fi
fi
if [[ ! -v "_ns_bugs" ]]; then
  if [[ "${_distro}" == "archlinux" ]]; then
    _ns_bugs="${_distro}/packaging/packages"
  elif [[ "${_distro}" == "dogeos" ]]; then
    _ns_bugs="${_ns}"
  fi
fi
if [[ ! -v "_pkg_bugs" ]]; then
  if [[ "${_distro}" == "archlinux" ]]; then
    _pkg_bugs="${_pkg}"
  elif [[ "${_distro}" == "dogeos" ]]; then
    _pkg_bugs="${_pkg}-ur"
  fi
fi
if [[ ! -v "_url_bugs" ]]; then
  if [[ "${_distro}" == "archlinux" ]]; then
    _url_bugs="${_http_bugs}/${_ns_bugs}/${_pkg_bugs}/-/issues"
  elif [[ "${_distro}" == "dogeos" ]]; then
    _url_bugs="${_http_bugs}/${_ns_bugs}/${_pkg_bugs}/issues"
  fi
fi
if [[ ! -v "_http" ]]; then
  if [[ "${_distro}" == "archlinux" ]]; then
    _http="https://forge.sourceware.org"
  elif [[ "${_distro}" == "dogeos" ]]; then
    _http="https://${_git_service}.com"
  fi
fi
if [[ ! -v "_docs" ]]; then
  _docs="true"
fi
_pkgver="16.2.1"
pkgver="${_pkgver}+r23+gd564253eb6c8"
_commit="d564253eb6c859e266d3cae18e82fb4db9a88316"
if [[ ! -v "_git" ]]; then
  _git="true"
fi
if [[ ! -v "_tag_name" ]]; then
  _tag_name="commit"
fi
if [[ ! -v "_tag" ]]; then
  if [[ "${_tag_name}" == "commit" ]]; then
    _tag="${_commit}"
  elif [[ "${_tag_name}" == "tag" ]]; then
    _tag="${_pkgver}"
  else
    _msg=(
      "Unknown tag name '${_tag_name}'."
    )
    echo \
      "${_msg[*]}" \
      1>&2
  fi
fi
pkgbase="${_pkg}"
pkgname=(
 "${_pkg}"
 "${_pkg}-ada"
 "${_pkg}-d"
 "${_pkg}-fortran"
 "${_pkg}-gcobol"
 "${_pkg}-go"
 "${_pkg}-libs"
 "${_pkg}-m2"
 "${_pkg}-objc"
 "${_pkg}-rust"
  "lib32-${_pkg}-libs"
  "libasan"
  "libatomic"
  "lib${_pkg}"
  "lib${_pkg}jit"
  "libgcobol"
  "libgfortran"
  "libgm2"
  "libgo"
  "libgomp"
  "libgphobos"
  "libhwasan"
  "libitm"
  "liblsan"
  "libobjc"
  "libquadmath"
  "libstdc++"
  "libtsan"
  "libubsan"
  "lto-dump"
)
pkgrel=3
pkgdesc='The GNU Compiler Collection'
arch=(
  "aarch64"
  "armv7l"
  "armv8l"
  "x86_64"
)
license=(
  "GPL-3.0-or-later WITH GCC-exception-3.1"
  "GFDL-1.3-or-later"
)
url="https://${_pkg}.${_proj}.org"
makedepends=(
  "binutils"
  "${_pkg}-ada"
  "${_pkg}-d"
  "git"
  "lib32-glibc"
  "libisl"
  "libmpc"
  "python"
  "rust"
  "zstd"
)
# Circular dependencies
makedepends+=(
  "${_pkg}-ada"
  "${_pkg}-d"
  "lib32-${_pkg}-libs"
)
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "doxygen"
  )
fi
checkdepends=(
  "deja${_proj}"
  "expect"
  "inetutils"
  "python-pytest"
  "tcl"
)
options=(
  "!emptydirs"
  "!lto"
)
_libdir="usr/lib/${_pkg}/$CHOST/${pkgver%%.*}"
_tarname="${_pkg}-${_tag}"
if [[ "${_git}" == "true" ]]; then
  _url="${_http}/${_ns}/${_pkg}"
  _uri="git+${_url}#${_tag}=${_tag}"
  _src="${_tarname}::${_uri}"
elif [[ "${_git}" == false ]]; then
  if [[ "${_git_service}" == "github" ]]; then
    if [[ "${_tag_name}" == "commit" ]]; then
      _uri="${_url}/archive/${_commit}.${_archive_format}"
      _sum="${_github_sum}"
    fi
  elif [[ "${_git_service}" == "gitlab" ]]; then
    if [[ "${_tag_name}" == "commit" ]]; then
      _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
    fi
  fi
  _src="${_tarfile}::${_uri}"
fi
source=(
  "${_src}"
  "c89"
  "c99"
  "${_pkg}-ada-repro.patch"
  "tune_branch_prediction_cost.patch"
)
sha256sums=(
  'c4def1816bc86f2bb981deb958a572ca63eb0ef784418f0414f1071a4efee44d'
  '7b09ec947f90b98315397af675369a1e3dfc527fa70013062e6e85c4be0275ab'
  '44ea973558842f3f4bd666bdaf6e810fd7b7c7bd36b5cc4c69f93d2cd0124fc7'
  '1773f5137f08ac1f48f0f7297e324d5d868d55201c03068670ee4602babdef2f'
  '838e14d4ef76079107a5373316598025915eaf747a10522ec9f8842125ca9a8e'
)
pkgver() {
  cd \
    "${_tarname}"
  echo \
    "$(cat \
         "${_pkg}/BASE-VER")+$(
      git \
        describe \
          --abbrev=12 \
          --tags |
    sed \
      's/[^-]*-[^-]*-//;s/[^-]*-/r&/;s/-/+/g;s/_/./')"
}

prepare() {
  if [[ ! -d "${_pkg}" ]]; then
    ln \
      -s \
      "${_pkg}-${pkgver/+/-}" \
      "${_pkg}"
  fi
  cd \
    "${_pkg}"
  # DogeOS installs x86_64 libraries in /lib
  sed \
    -i \
    '/m64=/s/lib64/lib/' \
    "${_pkg}/config/i386/t-linux64"
  # Reproducible gcc-ada
  patch \
    -Np0 < \
    "${srcdir}/${_pkg}-ada-repro.patch"
  # tune branch prediction cost
  patch \
    -Np1 < \
    "../tune_branch_prediction_cost.patch"
  mkdir \
    -p \
    "${srcdir}/${_pkg}-build"
  mkdir \
    -p \
    "${srcdir}/lib${_pkg}jit-build"
}

build() {
  local \
    _configure_opts=() \
    _make_bootstrap_opts=()
  _configure_opts+=(
    --prefix="/usr"
    --libdir="/usr/lib"
    --libexecdir="/usr/lib"
    --mandir="/usr/share/man"
    --infodir="/usr/share/info"
    --with-bugurl="${_url_bugs}"
    --with-build-config="bootstrap-lto"
    --with-gcc-major-version-only
    --with-linker-hash-style="gnu"
    --with-system-zlib
    --enable-cet="auto"
    --enable-checking="release"
    --enable-clocale="gnu"
    --enable-default-pie
    --enable-default-ssp
    --enable-gnu-indirect-function
    --enable-gnu-unique-object
    --enable-libstdcxx-backtrace
    --enable-link-serialization=1
    --enable-linker-build-id
    --enable-lto
    --enable-multilib
    --enable-plugin
    --enable-shared
    --enable-threads="posix"
    --disable-fixincludes
    --disable-libssp
    --disable-libstdcxx-pch
    --disable-werror
  )
  cd \
    "${_pkg}-build"
  # Credits @allanmcrae
  # https://github.com/allanmcrae/toolchain/blob/f18604d70c5933c31b51a320978711e4e6791cf1/gcc/PKGBUILD
  # TODO: properly deal with the build issues resulting from this
  CFLAGS="${CFLAGS/-Werror=format-security/}"
  CXXFLAGS="${CXXFLAGS/-Werror=format-security/}"
  "../${_pkg}/configure" \
    --enable-languages="ada,c,c++,d,fortran,go,lto,m2,objc,obj-c++,rust,cobol"
    --enable-bootstrap
    "${_configure_opts[@]:?_configure_opts unset}"
  # See https://bugs.archlinux.org/task/71777
  # for rationale re *FLAGS handling
  _make_bootstrap_opts+=(
    STAGE1_CFLAGS="-O2"
    BOOT_CFLAGS="${CFLAGS}"
    BOOT_LDFLAGS="${LDFLAGS}"
    LDFLAGS_FOR_TARGET="${LDFLAGS}"
  )
  make \
    -O \
    "${_make_bootstrap_opts[@]}" \
    bootstrap
  if [[ "${_docs}" == "true" ]]; then
    make \
      -O \
      -C \
        "${CHOST}/libstdc++-v3/doc" \
      doc-man-doxygen
  fi
  # Build libgccjit separately, to avoid building
  # all compilers with --enable-host-shared
  # which brings a performance penalty.
  cd \
    "${srcdir}/lib${_pkg}jit-build"
  "../${_pkg}/configure" \
    --enable-languages="jit" \
    --disable-bootstrap \
    --enable-host-shared \
    "${_configure_opts[@]:?_configure_opts unset}"
  make \
    -O \
    all-gcc
  cp \
    -a \
    "${_pkg}/lib${_pkg}jit.so"* \
    "../${_pkg}-build/${_pkg}/"
}

check() {
  cd \
    "${_pkg}-build"
  # disable libphobos test to avoid segfaults
  sed \
    -i \
    '/maybe-check-target-libphobos \\/d' \
    "Makefile"
  # do not abort on error as some are "expected"
  make \
    -O \
    -k \
    check || \
  true
  "${srcdir}/${_pkg}/contrib/test_summary"
}

_pick() {
  local \
    p="$1" \
    f \
    d; \
  shift
  for f; do
    d="${srcdir}/${p}/${f#$pkgdir/}"
    mkdir \
      -vp \
      "$(dirname \
           "${d}")"
    mv \
      -v \
      "${f}" \
      "${d}"
    rmdir \
      -vp \
      --ignore-fail-on-non-empty \
      "$(dirname \
           "${f}")"
  done
}

_install_runtime_library_exception() {
  # Install Runtime Library Exception
  install \
    -vDm644 \
    "${srcdir}/${_pkg}/COPYING.RUNTIME" \
    "${pkgdir}/usr/share/licenses/${pkgname}/RUNTIME.LIBRARY.EXCEPTION"
}

package_gcc() {
  local \
    _file_exe \
    _so
  pkgdesc="The GNU Compiler Collection - C and C++ frontends"
  depends=(
    "libasan=${pkgver}-${pkgrel}"
    "libgcc=${pkgver}-${pkgrel}"
    "libhwasan=${pkgver}-${pkgrel}"
    "liblsan=${pkgver}-${pkgrel}"
    "libstdc++=${pkgver}-${pkgrel}"
    "libtsan=${pkgver}-${pkgrel}"
    "libubsan=${pkgver}-${pkgrel}"
    'binutils>=2.28'
    'glibc>=2.27'
    "gmp"
    "libisl.so"
    "libmpc"
    "mpfr"
    "zlib"
    "zstd"
  )
  optdepends=(
    "lib32-${_pkg}-libs: for generating code for 32-bit ABI"
  )
  provides=(
    "${_pkg}-multilib"
  )
  replaces=(
    "${_pkg}-multilib"
  )
  options=(
    "!emptydirs"
    "staticlibs"
  )
  cd \
    "${_pkg}-build"
  make \
    DESTDIR="${pkgdir}" \
    install
  make \
    -C \
      "${_pkg}" \
    DESTDIR="${pkgdir}" \
    jit.install-common \
    jit.install-info
  (
    cd \
      "${pkgdir}"
    # prepare internal *.so symlinks to ensure
    # shared linking for those shared libs
    # where we ALSO ship a matching static
    # lib in the internal _libdir
    for _so \
      in "libatomic.so" \
	 "libstdc++.so" \
	 "libgdruntime.so" \
	 "libgphobos.so"; do
      ln \
        -srv \
	"usr/lib/${_so}" \
	"${_libdir}/${_so}"
      ln \
        -srv \
        "usr/lib32/${_so}" \
        "${_libdir}/32/${_so}"
    done
    _pick \
      "${_pkg}-ada" \
      "usr/bin/gnat"{"","bind","chop","clean","kr","link","ls","make","name","prep"}
    _pick \
      "${_pkg}-ada" \
      "${_libdir}/"{"","32/"}"ada_target_properties"
    _pick \
      "${_pkg}-ada" \
      "${_libdir}/"{"","32/"}"ada"{"include","lib"}"/"
    _pick \
      "${_pkg}-ada" \
      "${_libdir}/gnat1"
    _pick \
      "${_pkg}-ada" \
      "usr/share/info/gnat"{"-style","_rm","_ugn"}".info"
    _pick \
      "${_pkg}-d" \
      "usr/bin/"{"gdc","${CHOST}-gdc"}
    _pick \
      "${_pkg}-d" \
      "${_libdir}/d21"
    _pick \
      "${_pkg}-d" \
      "${_libdir}/include/d/"
    _pick \
      "${_pkg}-d" \
      "${_libdir}/"{"","32/"}"libg"{"druntime","phobos"}".so"
    _pick \
      "${_pkg}-d" \
      "usr/lib"{"","32"}"/libg"{"druntime","phobos"}".a"
    _pick \
      "${_pkg}-d" \
      "usr/lib"{"","32"}"/libgphobos.spec"
    _pick \
      "${_pkg}-d" \
      "usr/share/info/gdc.info"
    _pick \
      "${_pkg}-d" \
      "usr/share/man/man1/gdc.1"
    _pick \
      "${_pkg}-fortran" \
      "usr/bin/"{"gfortran","${CHOST}-gfortran"}
    _pick \
      "${_pkg}-fortran" \
      "${_libdir}/"{"","32/"}"finclude/"
    _pick \
      "${_pkg}-fortran" \
      "${_libdir}/"{"","32/"}"libcaf_"{"shmem","single"}".a"
    _pick \
      "${_pkg}-fortran" \
      "${_libdir}/f951"
    _pick \
      "${_pkg}-fortran" \
      "${_libdir}/include/ISO_Fortran_binding.h"
    _pick \
      "${_pkg}-fortran" \
      "usr/lib"{"","32"}"/libgfortran.spec"
    _pick \
      "${_pkg}-fortran" \
      "usr/share/info/gfortran.info"
    _pick \
      "${_pkg}-fortran" \
      "usr/share/man/man1/gfortran.1"
    _pick \
      "${_pkg}-gcobol" \
      "usr/bin/"{"gcobc","gcobol","${CHOST}-"{"gcobc","gcobol"}}
    _pick \
      "${_pkg}-gcobol" \
      "${_libdir}/cobol/"
    _pick \
      "${_pkg}-gcobol" \
      "${_libdir}/cobol1"
    _pick \
      "${_pkg}-gcobol" \
      "usr/lib/libgcobol.spec"
    _pick \
      "${_pkg}-gcobol" \
      "usr/share/man/man1/gcobol.1"
    _pick \
      "${_pkg}-gcobol" \
      "usr/share/man/man3/gcobol-io.3"
    _pick \
      "${_pkg}-go" \
      "usr/bin/"{"${_pkg}go","go","gofmt","${CHOST}-${_pkg}go"}
    _pick \
      "${_pkg}-go" \
      "${_libdir}/"{"buildid","cgo","go1","test2json","vet"}
    _pick \
      "${_pkg}-go" \
      "usr/lib"{"","32"}"/go/"
    _pick \
      "${_pkg}-go" \
      "usr/lib"{"","32"}"/lib"{"go","gobegin","golibbegin"}".a"
    _pick \
      "${_pkg}-go" \
      "usr/share/info/${_pkg}.info"
    _pick \
      "${_pkg}-go" \
      "usr/share/man/man1/"{"${_pkg}go","go","gofmt"}".1"
    _pick \
      "${_pkg}-m2" \
      "usr/bin/"{"gm2","${CHOST}-gm2"}
    _pick \
      "${_pkg}-m2" \
      "${_libdir}/cc1gm2"
    _pick \
      "${_pkg}-m2" \
      "usr/share/info/m2.info"
    _pick \
      "${_pkg}-m2" \
      "usr/share/man/man1/gm2.1"
    _pick \
      "${_pkg}-objc" \
      "${_libdir}/include/objc/"
    _pick \
      "${_pkg}-objc" \
      "${_libdir}/cc1obj"*
    _pick \
      "${_pkg}-rust" \
      "usr/bin/"{"${_pkg}rs","${CHOST}-${_pkg}rs"}
    _pick \
      "${_pkg}-rust" \
      "${_libdir}/crab1"
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libasan."{"a","so"*}
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libatomic.so"*
    _pick \
      "lib32-${_pkg}-libs" \
      "${_libdir}/32/libatomic.so"
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libgcc_s.so."*
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libgdruntime.so"*
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libgfortran."{"a","so"*}
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libgo.so"*
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libgomp."{"a","so"*}
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libgphobos.so"*
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libitm."{"a","so"*}
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libobjc."{"a","so"*}
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libquadmath."{"a","so"*}
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libstdc++.so"*
    _pick \
      "lib32-${_pkg}-libs" \
      "usr/lib32/libubsan."{"a","so"*}
    _pick \
      "libasan" \
      "usr/lib/libasan."{"a","so"*}
    _pick \
      "libatomic" \
      "usr/lib/libatomic.so"*
    _pick \
      "libatomic" \
      "${_libdir}/libatomic.so"
    _pick \
      "lib${_pkg}" \
      "usr/lib/lib${_pkg}_s.so."*
    _pick \
      "lib${_pkg}jit" \
      "usr/include/lib${_pkg}jit"*
      "usr/lib/lib${_pkg}jit.so"*
    _pick \
      "lib${_pkg}jit" \
      "usr/share/info/lib${_pkg}jit.info"
    _pick \
      "libgcobol" \
      "usr/lib/libgcobol."{"a","so"*}
    _pick \
      "libgfortran" \
      "usr/lib/libgfortran."{"a","so"*}
    _pick \
      "libgm2" \
      "${_libdir}/"{"","32/"}"m2/"
    _pick \
      "libgm2" \
      "usr/lib"{"","32"}"/libm2"{"cor","iso","log","min","pim"}"."{"a","so"*}
    _pick \
      "libgo" \
      "usr/lib/libgo.so"*
    _pick \
      "libgomp" \
      "usr/lib/libgomp."{"a","so"*}
    _pick \
      "libgomp" \
      "usr/share/info/libgomp.info"
    _pick \
      "libgphobos" \
      "usr/lib/libgdruntime.so"*
    _pick \
      "libgphobos" \
      "usr/lib/libgphobos.so"*
    _pick \
      "libhwasan" \
      "usr/lib/libhwasan."{"a","so"*}
    _pick \
      "libitm" \
      "usr/lib/libitm."{"a","so"*}
    _pick \
      "libitm" \
      "usr/share/info/libitm.info"
    _pick \
      "liblsan" \
      "usr/lib/liblsan."{"a","so"*}
    _pick \
      "libobjc" \
      "usr/lib/libobjc."{"a","so"*}
    _pick \
      "libquadmath" \
      "usr/lib/libquadmath."{"a","so"*}
    _pick \
      "libquadmath" \
      "usr/share/info/libquadmath.info"
    _pick \
      "libstdc++" \
      "usr/lib/libstdc++.so"*
    _pick \
      "libstdc++" \
      "usr/share/locale/"{"de","fr"}"/LC_MESSAGES/libstdc++.mo"
    _pick \
      "libtsan" \
      "usr/lib/libtsan."{"a","so"*}
    _pick \
      "libubsan" \
      "usr/lib/libubsan."{"a","so"*}
    _pick \
      "lto-dump" \
      "usr/bin/lto-dump"
    _pick \
      "lto-dump" \
      "usr/share/man/man1/lto-dump.1"
    # move specific files into the internal "_libdir"
    mv \
      -v \
      "usr/lib/libgcc_s"{"","_asneeded"}".so" \
      "${_libdir}/"
    mv \
      -v \
      "usr/lib32/libgcc_s"{"","_asneeded"}".so" \
      "${_libdir}/32/"
    mv \
      -v \
      "usr/lib/libatomic"{"","_asneeded"}".a" \
      "usr/lib/libatomic_asneeded.so" \
      "${_libdir}/"
    mv \
      -v \
      "usr/lib32/libatomic"{"","_asneeded"}".a" \
      "usr/lib32/libatomic_asneeded.so" \
      "${_libdir}/32/"
    mv \
      -v \
      "usr/lib/"*"_preinit.o" \
      "${_libdir}/"
    mv \
      -v \
      "usr/lib32/"*"_preinit.o" \
      "${_libdir}/32/"
    mv \
      -v \
      "usr/lib/"*".spec" \
      "${_libdir}/"
    mv \
      -v \
      "usr/lib32/"*".spec" \
      "${_libdir}/32/"
    mv \
      -v \
      "usr/lib/libstdc++"{"","exp","fs"}".a" \
      "${_libdir}/"
    mv \
      -v \
      "usr/lib32/libstdc++"{"","exp","fs"}".a" \
      "${_libdir}/32/"
    mv \
      -v \
      "usr/lib/libsupc++.a" \
      "${_libdir}/"
    mv \
      -v \
      "usr/lib32/libsupc++.a" \
      "${_libdir}/32/"
  )
  install \
    -vd \
    "${pkgdir}/usr/share/gdb/auto-load/usr/lib"
  mv \
    "../libstdc++/usr/lib/libstdc++.so.6."*"-gdb.py" \
    "${pkgdir}/usr/share/gdb/auto-load/usr/lib/"
  install \
    -vdm755 \
    "${pkgdir}/usr/lib/bfd-plugins/"
  ln \
    -s \
    "/${_libdir}/liblto_plugin.so" \
    "${pkgdir}/usr/lib/bfd-plugins/"
  # many packages expect this symlink
  ln \
    -s \
    "${_pkg}" \
    "${pkgdir}/usr/bin/cc"
  # create cc-rs compatible symlinks
  # https://github.com/rust-lang/cc-rs/blob/1.0.73/src/lib.rs#L2578-L2581
  for _file_exe \
    in {"c++","g++","${_pkg}","gcc-ar","gcc-nm","gcc-ranlib"}; do
    ln \
      -s \
      "/usr/bin/${_file_exe}" \
      "${pkgdir}/usr/bin/${CARCH}-linux-gnu-${_file_exe}"
  done
  # POSIX conformance launcher scripts for c89 and c99
  install \
    -vDm755 \
    "${srcdir}/c89" \
    "${pkgdir}/usr/bin/c89"
  install \
    -vDm755 \
    "${srcdir}/c99" \
    "${pkgdir}/usr/bin/c99"
  # install the libstdc++ man pages
  make \
    -C \
      "${CHOST}/libstdc++-v3/doc" \
    DESTDIR="${pkgdir}" \
    doc-install-man
  # byte-compile python libraries
  python \
    -m \
      "compileall" \
    "${pkgdir}/usr/share/${_pkg}-${pkgver%%.*}/"
  python \
    -O \
    -m \
      "compileall" \
    "${pkgdir}/usr/share/${_pkg}-${pkgver%%.*}/"
  _install_runtime_library_exception
}

package_gcc-ada() {
  pkgdesc='Ada front-end for GCC (GNAT)'
  depends=(
    "${_pkg}=${pkgver}-${pkgrel}"
    "glibc>=2.27"
    "gmp"
    "lib${_pkg}"
    "libisl.so"
    "libmpc"
    "mpfr"
    "zlib"
    "zstd"
  )
  provides=(
    "${pkgname}-multilib"
  )
  replaces=(
    "${pkgname}-multilib"
  )
  options=(
    "!emptydirs"
    "staticlibs"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  ln \
    -s \
    "${_pkg}" \
    "${pkgdir}/usr/bin/gnat${_pkg}"
  # insist on dynamic linking, but keep
  # static libraries because gnatmake complains
  mv \
    "${pkgdir}/${_libdir}/adalib/libgna"{"rl","t"}"-${pkgver%%.*}.so" \
    "${pkgdir}/usr/lib"
  ln \
    -s \
    "libgnarl-${pkgver%%.*}.so" \
    "${pkgdir}/usr/lib/libgnarl.so"
  ln \
    -s \
    "libgnat-${pkgver%%.*}.so" \
    "${pkgdir}/usr/lib/libgnat.so"
  rm \
    -vrf \
    "${pkgdir}/${_libdir}/adalib/libgna"{"rl","t"}".so"
  install \
    -vd \
    "${pkgdir}/usr/lib32/"
  mv \
    "${pkgdir}/$_libdir/32/adalib/libgna"{"rl","t"}"-${pkgver%%.*}.so" \
    "${pkgdir}/usr/lib32"
  ln \
    -s \
    "libgnarl-${pkgver%%.*}.so" \
    "${pkgdir}/usr/lib32/libgnarl.so"
  ln \
    -s \
    "libgnat-${pkgver%%.*}.so" \
    "${pkgdir}/usr/lib32/libgnat.so"
  rm \
    -vrf \
    "${pkgdir}/${_libdir}/32/adalib/libgna"{"rl","t"}".so"
  _install_runtime_library_exception
}

package_gcc-d() {
  pkgdesc="D frontend for GCC"
  depends=(
    "gcc=${pkgver}-${pkgrel}"
    "glibc>=2.27"
    "gmp"
    "libgphobos"
    "libisl.so"
    "libmpc"
    "mpfr"
    "zlib"
    "zstd"
  )
  provides=(
    "gdc"
  )
  replaces=(
    "gdc"
  )
  options=(
    "!emptydirs"
    "staticlibs"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  mkdir \
    -pv \
    "${pkgdir}/${_libdir}/32"
  mv \
    -v \
    "${pkgdir}/usr/lib/libg"{"druntime","phobos"}".a" \
    "${pkgdir}/${_libdir}/"
  mv \
    -v \
    "${pkgdir}/usr/lib32/libg"{"druntime","phobos"}".a" \
    "${pkgdir}/${_libdir}/32"
  mv \
    -v \
    "${pkgdir}/usr/lib/libgphobos.spec" \
    "${pkgdir}/${_libdir}/"
  mv \
    -v \
    "${pkgdir}/usr/lib32/libgphobos.spec" \
    "${pkgdir}/${_libdir}/32"
  _install_runtime_library_exception
}

package_gcc-fortran() {
  pkgdesc='Fortran front-end for GCC'
  depends=(
    "${_pkg}=${pkgver}-${pkgrel}"
    "glibc>=2.27"
    "gmp"
    "libgfortran"
    "libisl.so"
    "libmpc"
    "mpfr"
    "zlib"
    "zstd"
  )
  provides=(
    "${pkgname}-multilib"
  )
  replaces=(
    "${pkgname}-multilib"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  ln \
    -s \
    "gfortran" \
    "${pkgdir}/usr/bin/f95"
  mv \
    -v \
    "${pkgdir}/usr/lib/libgfortran.spec" \
    "${pkgdir}/${_libdir}/"
  mv \
    -v \
    "${pkgdir}/usr/lib32/libgfortran.spec" \
    "${pkgdir}/${_libdir}/32"
  _install_runtime_library_exception
}

package_gcc-gcobol() {
  pkgdesc="Cobol frontend for GCC"
  depends=(
    "${_pkg}=${pkgver}-${pkgrel}"
    'glibc>=2.27'
    "gmp"
    "libgcobol"
    "libisl.so"
    "libmpc"
    "mpfr"
    "zlib"
    "zstd"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  mv \
    -v \
    "${pkgdir}/usr/lib/libgcobol.spec" \
    "${pkgdir}/${_libdir}/"
  _install_runtime_library_exception
}

package_gcc-go() {
  pkgdesc='Go front-end for GCC'
  depends=(
    "${_pkg}=$pkgver-$pkgrel"
    "glibc>=2.27"
    "gmp"
    "libgo"
    "libisl.so"
    "libmpc"
    "mpfr"
    "zlib"
    "zstd"
  )
  provides=(
    "go=1.17"
    "${pkgname}-multilib"
  )
  replaces=(
    "${pkgname}-multilib"
  )
  conflicts=(
    "go"
  )

  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_gcc-libs() {
  pkgdesc='Runtime libraries shipped by GCC'
  depends=(
    "glibc>=2.27"
    "libasan"
    "libatomic"
    "lib${_pkg}"
    "libgfortran"
    "libgomp"
    "libhwasan"
    "liblsan"
    "libobjc"
    "libquadmath"
    "libstdc++"
    "libtsan"
    "libubsan"
  )
  provides=(
    "${pkgname}-multilib"
  )
}

package_gcc-m2() {
  pkgdesc='Modula-2 frontend for GCC'
  depends=(
    "${_pkg}=${pkgver}-${pkgrel}"
    "glibc>=2.27"
    "gmp"
    "libgm2"
    "libisl.so"
    "libmpc"
    "mpfr"
    "zlib"
    "zstd"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_gcc-objc() {
  pkgdesc='Objective-C front-end for GCC'
  depends=(
    "${_pkg}=${pkgver}-${pkgrel}"
    "glibc>=2.27"
    "gmp"
    "libisl.so"
    "libmpc"
    "libobjc"
    "mpfr"
    "zlib"
    "zstd"
  )
  provides=(
    "${pkgname}-multilib"
  )
  replaces=(
    "${pkgname}-multilib"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_gcc-rust() {
  pkgdesc="Rust frontend for GCC"
  depends=(
    "${_pkg}=${pkgver}-${pkgrel}"
    "glibc>=2.27"
    "gmp"
    "libisl.so"
    "libmpc"
    "mpfr"
    "zlib"
    "zstd"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_lib32-gcc-libs() {
  pkgdesc='32-bit runtime libraries shipped by GCC'
  depends=(
    "lib32-glibc>=2.27"
  )
  provides=(
    "libasan.so"
    "libatomic.so"
    "libgdruntime.so"
    "libgfortran.so"
    "libgo.so"
    "libgomp.so"
    "libgphobos.so"
    "libitm.so"
    "libobjc.so"
    "libquadmath.so"
    "libubsan.so"
  )
  options=(
    "!emptydirs"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  rm \
    -v \
    "${pkgdir}/usr/lib32/libstdc++.so.6."*"-gdb.py"
  _install_runtime_library_exception
}

package_libasan() {
  pkgdesc='Address Sanitizer runtime library shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
    "libstdc++"
  )
  provides=(
    "libasan.so"
  )
  mv \
    -v \
    "${_pkg}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libatomic() {
  pkgdesc='GNU Atomic library shipped by GCC'
  depends=(
    "glibc>=2.27"
  )
  provides=(
    "libatomic.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libgcc() {
  pkgdesc='Low-level runtime library shipped by GCC'
  depends=(
    "glibc>=2.27"
  )
  provides=(
    "lib${_pkg}_s.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libgccjit() {
  pkgdesc="Just-In-Time Compilation with GCC backend"
  depends=(
    "${_pkg}=$pkgver-$pkgrel"
    "glibc>=2.27"
    "gmp"
    "libisl.so"
    "libmpc"
    "mpfr"
    "zlib"
    "zstd"
  )
  provides=(
    "lib${_pkg}jit.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libgcobol() {
  pkgdesc='Cobol runtime libraries shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
    "libstdc++"
    "libxml2"
  )
  provides=(
    "libgcobol.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libgfortran() {
  pkgdesc='Runtime libraries shipped by GCC'
  depends=(
    'glibc>=2.27'
    "lib${_pkg}"
  )
  provides=(
    "libgfortran.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libgm2() {
  pkgdesc='Modula-2 runtime libraries shipped by GCC'
  depends=(
    "glibc>=2.27"
  )
  provides=(
    "libm2cor.so"
    "libm2iso.so"
    "libm2log.so"
    "libm2min.so"
    "libm2pim.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libgo() {
  pkgdesc='Go runtime libraries shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
  )
  provides=(
    "libgo.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libgomp() {
  pkgdesc='OpenMP library shipped by GCC'
  depends=(
    "glibc>=2.27"
  )
  provides=(
    "libgomp.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libgphobos() {
  pkgdesc='D runtime libraries shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
  )
  provides=(
    "libgdruntime.so"
    "libgphobos.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libhwasan() {
  pkgdesc='Hardware-assisted Address Sanitizer runtime library shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
    "libstdc++"
  )
  provides=(
    "libhwasan.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libitm() {
  pkgdesc='GNU Transactional Memory library shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
  )
  provides=(
    "libitm.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_liblsan() {
  pkgdesc='Leak Sanitizer runtime library shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
    "libstdc++"
  )
  provides=(
    "liblsan.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libobjc() {
  pkgdesc='Ojective-C runtime libraries shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
  )
  provides=(
    "libobjc.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libquadmath() {
  pkgdesc='GCC __float128 library'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
  )
  provides=(
    "libquadmath.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libstdc++ () {
  pkgdesc='C++ runtime libraries shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
  )
  provides=(
    "libstdc++.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libtsan() {
  pkgdesc='Thread Sanitizer runtime library shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
    "libstdc++"
  )
  provides=(
    "libtsan.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_libubsan() {
  pkgdesc='Undefined Behavior Sanitizer runtime library shipped by GCC'
  depends=(
    "glibc>=2.27"
    "lib${_pkg}"
    "libstdc++"
  )
  provides=(
    "libubsan.so"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}

package_lto-dump() {
  pkgdesc="Dump link time optimization object files"
  depends=(
    "${_pkg}=${pkgver}-${pkgrel}"
    "glibc>=2.27"
    "gmp"
    "libisl.so"
    "libmpc"
    "mpfr"
    "zlib"
    "zstd"
  )
  mv \
    -v \
    "${pkgname}/"* \
    "${pkgdir}"
  _install_runtime_library_exception
}
