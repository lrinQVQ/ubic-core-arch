# Maintainer: ubicorn <ubicorn@protonmail.com>
pkgname=ubic-core-git
pkgver=r609.e2e8235
pkgrel=1
pkgdesc="official UBIC node"
arch=('x86_64')
url="https://github.com/UBIC-repo/core"
license=('MIT')
makedepends=('git' 'cmake')
depends=('leveldb' 'pcsclite' 'boost' 'boost-libs' 'openssl')
source=("${pkgname}::git+https://github.com/UBIC-repo/core.git")
sha256sums=('SKIP')

pkgver() {
    cd "$srcdir/$pkgname"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cd "$srcdir/$pkgname"
	cmake CMakeLists.txt
	make
}

package() {
	cd "$srcdir/$pkgname"

	install -Dm755 "ubicd" -t "$pkgdir/usr/bin/"
	install -Dm755 "ubic" -t "$pkgdir/usr/bin/"

	if [ ! -d "/var/ubic/" ]; then
		install -m777 -d "${pkgdir}/var/ubic/"
		cp -r "Static/web" "$pkgdir/var/ubic/"
		cp -r "Static/genesis/certs" "$pkgdir/var/ubic/"
		cp -r "Static/genesis/x509" "$pkgdir/var/ubic/"
		cp -r "Static/genesis/votes.mdb" "$pkgdir/var/ubic/"
		cp -r "Static/genesis" "$pkgdir/var/ubic/genesis"
		chmod 777 -R "$pkgdir/var/ubic/"
	else
		install -m777 -d "${pkgdir}/var/ubic/"
		cp -r "Static/web" "$pkgdir/var/ubic/"
		cp -r "Static/genesis" "$pkgdir/var/ubic/genesis"
	fi

	install -m755 -d ${pkgdir}/usr/lib/systemd/system
	#install -m644 $startdir/ubic.service -t ${pkgdir}/usr/lib/systemd/system
}
