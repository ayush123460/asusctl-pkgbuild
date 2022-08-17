# Maintainer: dragonn <>
# Contributor: Arglebargle <arglebargle@arglebargle.dev>
# Contributor: Static_Rocket

# shellcheck disable=SC2034,SC2154,SC2164

pkgname=asusctl
pkgver=4.3.4.r6.ga0f7cf3
_gitref=a0f7cf3acd89318ceeb73de7dfacab131f0d97e3
pkgrel=1
pkgdesc="Asus laptop control utilities"
arch=('x86_64')
url="https://gitlab.com/asus-linux/asusctl"
license=('MPL2')
depends=('libusb' 'udev')
optdepends=(
	'ASUS-WMI-FAN-CONTROL: custom fan curve support'
	'linux-rog: deprecated name for custom fan curve capability'
	'supergfxctl: graphics swithing for iGPU + Nvidia dGPU laptops'
	)
makedepends=('git' 'rust')
provides=()
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
	depends+=('power-profiles-daemon>=0.9.0+14+g112df04')
	cd "$srcdir/$pkgname"
	make DESTDIR="$pkgdir" install
}

