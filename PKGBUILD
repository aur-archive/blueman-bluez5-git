# Maintainer: Martin Wimpress <code@flexion.org>

_ver=1.2.3
_pkgname=blueman
pkgname=${_pkgname}-bluez5-git
pkgver=1.2.3.20140718.9781499
pkgrel=1
pkgdesc="A GTK+ Bluetooth Manager (BlueZ 5)"
arch=('i686' 'x86_64')
license=('GPL')
url="https://github.com/blueman-project/blueman"
depends=('bluez' 'dbus-glib' 'gconf' 'gtk3' 'notification-daemon'
         'libnotify' 'obex-data-server' 'polkit' 'python2-dbus'
         'python2-gobject' 'python2-pybluez' 'startup-notification')
optdepends=('dnsmasq: DHCP server for Network Access Point'
            'pulseaudio: for some audio support')
makedepends=('cython2' 'git' 'intltool' 'libtool')
source=("${pkgname}"::"git+https://github.com/blueman-project/${_pkgname}.git")
sha1sums=('SKIP')
install=${_pkgname}.install

pkgver() {
    cd "${srcdir}/${pkgname}"
    echo ${_ver}.$(date +%Y%m%d).$(git rev-parse --short master)
}

prepare() {
    cd "${srcdir}/${pkgname}"
    # Replace the python interpreter with python2
    for PY in apps/blueman-*
    do
        sed -i 's/python/python2/' "${PY}"
    done
    NOCONFIGURE=1 ./autogen.sh
}

build() {
    cd "${srcdir}/${pkgname}"
    export PYTHON=/usr/bin/python2
    export CYTHONEXEC=/usr/bin/cython2
    ./configure \
        --prefix=/usr \
        --sysconfdir=/etc \
        --libexecdir=/usr/lib/${_pkgname} \
        --with-gtk=3.0 \
        --disable-hal \
        --disable-sendto \
        --disable-static
    make
}

package() {
    cd "${srcdir}/${pkgname}"
    make DESTDIR="${pkgdir}" install
}
