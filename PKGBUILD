# Maintainer: ubicorn <ubicorn@protonmail.com>
pkgname=ubic-core
pkgver=0.4.2
pkgrel=1
pkgdesc="official UBIC node"
arch=('x86_64')
url="https://github.com/UBIC-repo/core"
license=('MIT')
makedepends=('git' 'cmake')
depends=('leveldb' 'pcsclite' 'boost' 'boost-libs' 'openssl')
source=("ubic-core-$pkgver.tar.gz::https://github.com/UBIC-repo/core/archive/V$pkgver.tar.gz")
sha256sums=('7c49382386a487125e7665ab13743ad6443a30d84aee6d8f22a8936f34d4ccb3')

build() {
	cd "$srcdir/core-$pkgver"
	cmake CMakeLists.txt
	make
}

package() {
	cd "$srcdir/core-$pkgver"

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
		cp -r "Static/web" "$pkgdir/var/ubic/"
		cp -r -m777 -d "Static/genesis" "$pkgdir/var/ubic/genesis"
	fi

	install -m755 -d ${pkgdir}/usr/lib/systemd/system
	install -m644 $startdir/ubic.service -t ${pkgdir}/usr/lib/systemd/system
}
