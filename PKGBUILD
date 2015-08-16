# Maintainer: Benjamin Chretien <chretien+aur at lirmm dot fr>
# Contributor: Daniel Fiser <danfis@danfis.cz>
# Contributor: Cédric M. Campos <cedricmc@{icmat,uva}.es>

pkgname=ipopt
pkgver=3.12.3
pkgrel=1
pkgdesc="Ipopt (Interior Point OPTimizer) is a software package for large-scale  nonlinear optimization."
arch=(i686 x86_64)
url="https://projects.coin-or.org/Ipopt"
license=('GPL')
depends=(blas lapack)
makedepends=(gcc-fortran)
provides=()
conflicts=()
replaces=()
backup=()
install=
source=(http://www.coin-or.org/download/source/Ipopt/Ipopt-$pkgver.tgz)
noextract=()
md5sums=('c560cbfa9cbf62acf8b485823c255a1b')

build() {
    export PKG_CONFIG_PATH="$PKG_CONFIG_PATH:$srcdir/Ipopt-$pkgver/ThirdParty/Metis/:$srcdir/Ipopt-$pkgver/ThirdParty/Mumps/:$srcdir/Ipopt-$pkgver/ThirdParty/HSL/:$srcdir/Ipopt-$pkgver/Ipopt"

#   cd "$srcdir/Ipopt-$pkgver/ThirdParty/Blas"   && ./get.Blas
#   cd "$srcdir/Ipopt-$pkgver/ThirdParty/Lapack" && ./get.Lapack
    cd "$srcdir/Ipopt-$pkgver/ThirdParty/ASL"    && ./get.ASL
    cd "$srcdir/Ipopt-$pkgver/ThirdParty/Metis"  && ./get.Metis
    cd "$srcdir/Ipopt-$pkgver/ThirdParty/Mumps"  && ./get.Mumps
    cd "$srcdir/Ipopt-$pkgver"

    # Quick and dirty fix for linker errors
    export LDFLAGS="$LDFLAGS,-ldl,-lpthread"
    ./configure --prefix=/usr

    make
}

package() {
    cd "$srcdir/Ipopt-$pkgver"
    make DESTDIR="$pkgdir" install

    sed -i "s:$srcdir/Ipopt-$pkgver:\$srcdir:g" "$pkgdir"/usr/share/coin/doc/Ipopt/*.txt

    mkdir -p "$pkgdir/etc/ld.so.conf.d" && cd "$pkgdir/etc/ld.so.conf.d"
    echo "/usr/lib/coin" > ipopt.conf
    echo "/usr/lib/coin/ThirdParty" >> ipopt.conf
}
