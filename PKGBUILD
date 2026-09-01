# Maintainer: Dudemanguy <dudemanguy@artixlinux.org>
pkgname=s6-frontend
pkgver=0.1.0.0.r2.gd08efcb
pkgrel=1
pkgdesc='A higher-level interface to the s6 ecosystem.'
arch=('x86_64')
url='https://github.com/username13121/s6-frontend'
license=('ISC')
depends=('s6' 's6-rc' 's6-linux-init')
makedepends=('git')
backup=('etc/s6-frontend.conf'
        'etc/s6-frontend-user.conf')
install=s6-frontend.install
_commit=d08efcbe035d221447c4c8a5a87036e39dca3205
source=("${pkgname}::git+https://github.com/username13121/${pkgname}.git#commit=${_commit}"
        's6-frontend.conf'
        's6-frontend-user.conf')
sha256sums=('SKIP'
            '4805d0c844cfe43685f4f0c5e1d3c24b150339779e335266619e366bfa62a2d1'
            '3823f1b49fdc84ced4e26f013967bdad80c18e5c68d7fbc153498db65ad02477')

build() {
  cd ${pkgname}
  ./configure --prefix=/usr \
              --sysconfdir=/etc \
              --libexecdir=/usr/lib \
              --conffile=/etc/s6-frontend.conf \
              --user-conffile=/etc/s6-frontend-user.conf \
              --with-user-store-list=/etc/s6/user/sv/:/etc/s6/user/adminsv \
              --with-user-source-subdir=/s6/sv \
              --with-user-repo-subdir=/s6/repo \
              --with-user-bootdb-subdir=/s6/rc/compiled \
              --disable-allstatic \
              --disable-static \
              --enable-pkgconfig \
              --enable-shared \
              --enable-util-linux \
              --with-pkgconfig
  make
}

check() {
  cd ${pkgname}
  make check
}

package() {
  depends+=('libs6.so' 'libs6rc.so' 'libs6_linux_init.so')
  cd ${pkgname}
  make DESTDIR=${pkgdir} install
  install -v -d -m2755 "${pkgdir}"/etc/s6/repo
  install -v -d -m0755 \
    "${pkgdir}"/etc/s6/user/sv \
    "${pkgdir}"/etc/s6/user/adminsv
  install -Dm644 "${srcdir}"/s6-frontend.conf "${pkgdir}/etc/s6-frontend.conf"
  install -Dm644 "${srcdir}"/s6-frontend-user.conf "${pkgdir}/etc/s6-frontend-user.conf"
  install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
