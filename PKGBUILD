# Maintainer: Johannes Arnold <johannes.arnold@stud.uni-hannover.de>
pkgname=shairport-sync-git
pkgver=3.3.7rc3.r1.g90636da
pkgrel=1
pkgdesc='Emulates an AirPort Express for the purpose of streaming music from iTunes and compatible iPods and iPhones'
arch=('x86_64')
url='https://github.com/mikebrady/shairport-sync'
license=('custom')
backup=('etc/shairport-sync.conf')
depends=('avahi' 'libsoxr' 'alsa-lib' 'libconfig' 'libpulse' 'jack' 'mosquitto')
makedepends=('git' 'xmltoman')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=(
  'git+https://github.com/mikebrady/shairport-sync.git'
  'shairport-sync.sysusers'
  'remove_useradd.patch'
)
sha1sums=(
  SKIP
  'b806f9cd3eeaf8585a51d79c7b5681e3d3e4748a'
  '2cdd711a21a74748137d2e3894fb0fcb189c41e2'
)

pkgver() {
	cd "$srcdir/${pkgname%-git}"
	git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
	cd "$srcdir/${pkgname%-git}"
	patch -p1 < ../remove_useradd.patch
}

build() {
	cd "$srcdir/${pkgname%-git}"

	autoreconf -i -f

	./configure \
	  --prefix=/usr \
	  --sysconfdir=/etc \
	  --with-alsa \
	  --with-pa \
	  --with-stdout \
	  --with-pipe \
	  --with-jack \
	  --with-avahi \
	  --with-dns_sd \
	  --with-soxr \
	  --with-convolution \
	  --with-metadata \
	  --with-dbus-interface \
	  --with-mpris-interface \
	  --with-mqtt-client \
	  --with-ssl=openssl \
	  --with-pkg-config \
	  --with-systemd \
	  --with-configfiles

	make
}

package() {
	cd "$srcdir/${pkgname%-git}"
	make DESTDIR="$pkgdir" install
  install -D -m644 "$srcdir"/shairport-sync.sysusers "$pkgdir"/usr/lib/sysusers.d/shairport-sync.conf
  install -D -m664 LICENSES "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
  rm "$pkgdir"/etc/shairport-sync.conf.sample
}
