# Maintainer: dragonn <>
# Contributor: Arglebargle <arglebargle@arglebargle.dev>
# Contributor: Static_Rocket

# shellcheck disable=SC2034,SC2154,SC2164

pkgname=asusctl
pkgver=4.0.6.r7.gbcf516a
_gitref=bcf516afebb5a3c1c0f1aff739230b3e891b562f
pkgrel=1
pkgdesc="Asus laptop control utilities"
arch=('x86_64')
url="https://gitlab.com/asus-linux/asusctl"
license=('MPL2')
depends=('libusb' 'udev')
optdepends=(
	'ASUS-WMI-FAN-CONTROL: custom fan curve support'
	'linux-rog: deprecated name for custom fan curve capability'
	)
makedepends=('git' 'rust')
provides=('asus-nb-ctrl')
conflicts=('asusctl-git' 'asus-nb-ctrl-git' 'asus-nb-ctrl' 'rog-core' 'tlp')
source=('git+https://gitlab.com/asus-linux/asusctl.git')
md5sums=('SKIP')

install="asusctl.install"

pkgver() {
	cd "$srcdir/$pkgname"
	git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
	cd "$srcdir/$pkgname"
	git checkout "$_gitref"
}

build() {
	cd "$srcdir/$pkgname"
	make build
}

package() {
	# add runtime dependencies, these aren't needed during build
	depends+=('supergfxctl' 'power-profiles-daemon>=0.9.0+14+g112df04')
	cd "$srcdir/$pkgname"
	make DESTDIR="$pkgdir" install
}

