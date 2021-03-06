# Maintainer:
# Contributor: Alexander Rødseth <rodseth@gmail.com>
# Contributor: Arch Haskell Team <arch-haskell@haskell.org>

pkgname=haskell-ghc-paths
pkgver=0.1.0.8
pkgrel=6
pkgdesc="Knowledge of GHC's installation directories"
url="http://hackage.haskell.org/package/ghc-paths"
license=('custom:BSD3')
arch=('x86_64' 'i686')
makedepends=()
depends=(ghc=7.4.1)
options=('strip')
source=("http://hackage.haskell.org/packages/archive/ghc-paths/$pkgver/ghc-paths-$pkgver.tar.gz")
install=haskell-ghc-paths.install
md5sums=('d2b23dc563888e380588501d2ce1d82b')

build() {
  cd "$srcdir/ghc-paths-$pkgver"

  runhaskell Setup configure -O -p --enable-split-objs --enable-shared \
     --prefix=/usr --docdir="/usr/share/doc/$pkgname" \
     --libsubdir=\$compiler/site-local/\$pkgid
  runhaskell Setup build
  runhaskell Setup haddock
  runhaskell Setup register --gen-script
  runhaskell Setup unregister --gen-script
  sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}

package() {
  cd "$srcdir/ghc-paths-$pkgver"

  install -Dm 744 register.sh \
    "$pkgdir/usr/share/haskell/$pkgname/register.sh"
  install -m 744 unregister.sh \
    "$pkgdir/usr/share/haskell/$pkgname/unregister.sh"
  install -dm 755 "$pkgdir/usr/share/doc/ghc/html/libraries"
  ln -s "/usr/share/doc/$pkgname/html" \
    "$pkgdir/usr/share/doc/ghc/html/libraries/ghc-paths"
  runhaskell Setup copy --destdir="$pkgdir"
  install -D -m644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  rm -f "$pkgdir/usr/share/doc/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
