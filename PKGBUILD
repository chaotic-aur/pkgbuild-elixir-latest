# Maintainer: Johannes Löthberg <johannes@kyriasis.com>
# Contributor: Sergej Pupykin <arch+pub@sergej.pp.ru>
# Contributor: Gilbert Kennen <gilbert firewatcher org>
# Contributor: Alex JP <programming.hubmaking@slmail.me>

# options - defaults
if [ -z "$_pkgver" ] ; then
  : ${_autoupdate:=true}
else
  : ${_autoupdate:=false}
fi

: ${_pkgver:=1.15.5}

# update version
case "${_autoupdate::1}" in
  't'|'y'|'1')
    _response=$(curl "https://api.github.com/repos/elixir-lang/elixir/releases" -s)

    _get() {
      printf '%s' "$_response" \
        | awk -F '"' '/"'"$1"'":/{print $4}' \
        | head -1 | sed 's/^v//'
    }
    _pkgver_new=$(_get name)

    # update _pkgver
    if [ x"$_pkgver" != x"$_pkgver_new" ] ; then
      _pkgver="$_pkgver_new"
      sed -Ei "s@^(\s*: \\\$\{_pkgver):=[0-9]+.*\}\$@\1:=$_pkgver}@" "$startdir/PKGBUILD"
    fi
    ;;
esac

_pkgname="elixir"
pkgname="$_pkgname-latest"
pkgver=1.15.5
pkgrel=1

pkgdesc="a functional meta-programming aware language built on top of the Erlang VM"
url="https://elixir-lang.org"
license=('Apache' 'custom:EPL')

arch=('any')

depends=('erlang-nox')
checkdepends=('git')

conflicts=("$_pkgname")
provides=("$_pkgname")

_pkgsrc="$_pkgname-$_pkgver"
source=("$_pkgsrc.tar.gz::https://github.com/elixir-lang/elixir/archive/v$_pkgver.tar.gz")
sha256sums=('SKIP')

pkgver() {
  printf '%s' \
    "$_pkgver"
}

#prepare() {
#  cd "$_pkgsrc"
#  # https://github.com/elixir-lang/elixir/issues/12677
#  patch -Np1 < "../73b65eca5af294a8afbed5bc73c178da18f0055c.patch"
#}

build() {
  cd "$_pkgsrc"
  make
}

#check() {
#  cd "$_pkgsrc"
#  ERL_EPMD_PORT=5369 make test
#
#  # The elixir test suite starts up epmd and then doesn't kill it again afterwards.
#  epmd -port 5369 -kill
#}

package() {
  cd "$_pkgsrc"
  install -Dm644 "LICENSE" -t "$pkgdir/usr/share/licenses/$pkgname"
  make DESTDIR="$pkgdir" PREFIX=/usr install
}
