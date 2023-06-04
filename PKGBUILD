# Maintainer: dragonn <>
# Contributor: Arglebargle <arglebargle@arglebargle.dev>
# Contributor: Static_Rocket

# shellcheck disable=SC2034,SC2154,SC2164

pkgver=4.6.2.r0.g7ae0f89
_gitref=7ae0f896cf197a240b871a0228966bc36e239a3c
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
makedepends=('git' 'rust' 'llvm' 'clang' 'at-spi2-core' 'cairo' 'gtk3')
provides=()
conflicts=('asusctl-git' 'asus-nb-ctrl-git' 'asus-nb-ctrl' 'rog-core' 'tlp')
source=('git+https://gitlab.com/asus-linux/asusctl.git')
md5sums=('SKIP')

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

_package-asusctl() {
	# add runtime dependencies, these aren't needed during build
	depends+=('power-profiles-daemon>=0.9.0+14+g112df04')
	optdepends+=('rog-control-center')
	install="asusctl.install"

	cd "$srcdir/asusctl"
	make DESTDIR="$pkgdir" install
	rm -rf $pkgdir/usr/bin/rog-control-center
	rm -rf $pkgdir/usr/share/rog-gui
	rm -rf $pkgdir/usr/share/icons
	rm -rf $pkgdir/usr/share/applications
}

_package-rog-control-center() {
	depends+=('asusctl' 'libappindicator-gtk3' 'at-spi2-core' 'cairo' 'gtk3')

	cd "$srcdir/asusctl"
	make DESTDIR="$pkgdir" install
	rm -rf $pkgdir/usr/bin/asusctl
	rm -rf $pkgdir/usr/bin/asusd
	rm -rf $pkgdir/usr/bin/asusd-user
	rm -rf $pkgdir/usr/lib
	rm -rf $pkgdir/usr/share/dbus-1
	rm -rf $pkgdir/usr/share/asusd
	rm -rf $pkgdir/etc/asusd
}

pkgname=("asusctl" "rog-control-center")
for _p in "${pkgname[@]}"; do
  eval "package_$_p() {
    $(declare -f "_package-${_p#$pkgbase}")
    _package-${_p#$pkgbase}
  }"
done
