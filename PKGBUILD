# Maintainer: Johannes Löthberg <johannes@kyriasis.com>
# Contributor: Sergej Pupykin <arch+pub@sergej.pp.ru>
# Contributor: Gilbert Kennen <gilbert firewatcher org>
# Contributor: Alex JP <programming.hubmaking@slmail.me>

pkgbase=elixir
pkgname=elixir-latest
conflicts=('elixir')
provides=('elixir')
pkgver=1.15.4
pkgrel=1

pkgdesc="a functional meta-programming aware language built on top of the Erlang VM"
url="https://elixir-lang.org"
license=('Apache' 'custom:EPL')

arch=('any')

depends=('erlang-nox')
checkdepends=('git')

source=("$pkgbase-$pkgver.tar.gz::https://github.com/elixir-lang/elixir/archive/v$pkgver.tar.gz")
sha256sums=('302bf8065ab792a88f6c3a0c01a6bb58737be3e4fc2564c8afd418bf9792501c')

#prepare() {
#  cd elixir-"$pkgver"
#  # https://github.com/elixir-lang/elixir/issues/12677
#  patch -Np1 < "../73b65eca5af294a8afbed5bc73c178da18f0055c.patch"
#}

build() {
cd elixir-"$pkgver"
make
}

#check() {
#  cd elixir-"$pkgver"
#  ERL_EPMD_PORT=5369 make test
#
#  # The elixir test suite starts up epmd and then doesn't kill it again afterwards.
#  epmd -port 5369 -kill
#}

package() {
cd elixir-"$pkgver"
mkdir -p "$pkgdir"/usr/share/licenses/"$pkgbase"
install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/"$pkgbase"
make DESTDIR="$pkgdir" PREFIX=/usr install
}
