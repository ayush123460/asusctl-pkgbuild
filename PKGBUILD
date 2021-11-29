pkgname=asusctl
pkgver=4.0.6
pkgrel=1
pkgdesc="Asus utility for Linux to control many aspects of various ASUS laptops."
arch=('x86_64')
url="https://gitlab.com/asus-linux/asusctl"
license=('MPL2')
depends=('dbus' 'libusb' 'systemd' 'power-profiles-daemon')
optdepends=('linux-rog')
makedepends=('rust')
conflicts=('asusctl-git' 'tlp' 'rog-core' 'asus-nb-ctrl')
source=("https://gitlab.com/asus-linux/asusctl/-/archive/${pkgver}/asusctl-${pkgver}.tar.gz")
md5sums=('428afc41bde977cf8d3f69f88fc475a7')
install="asusctl.install"

build() {
  cd "${pkgname}-${pkgver}"
  make build
}

package() {
  cd "${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
}
