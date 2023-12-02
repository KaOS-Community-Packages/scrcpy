pkgname=scrcpy
_pkgname=scrcpy-server
pkgver=2.3.1
pkgrel=1
pkgdesc='Display and control your Android device on your PC using USB cable or wirelessly via WiFi.'
arch=('x86_64')
url='https://github.com/Genymobile/scrcpy'
license=('Apache')
depends=('ffmpeg' 'sdl2' 'android-tools')
makedepends=('meson' 'ninja')
optdepends=('android-udev-rules')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/Genymobile/scrcpy/archive/refs/tags/v${pkgver}.tar.gz"
        "${_pkgname}-${pkgver}.jar::https://github.com/Genymobile/scrcpy/releases/download/v${pkgver}/scrcpy-server-v${pkgver}")
md5sums=('4d8348bd16293c1ebafff6084fd4a4c8'
         'a196721c8e0abbdf40a24122a02b4942')

build() {
    cd "${pkgname}-${pkgver}"

    rm -rf build
    meson build --buildtype release --strip -Db_lto=true \
        -Dprebuilt_server="../${_pkgname}-${pkgver}.jar"
    cd build
    ninja
}

package() {
    install -dm 755 "${pkgdir}/usr/bin"
    install -dm 755 "${pkgdir}/usr/local/share/scrcpy"
    install -Dm 755 "${pkgname}-${pkgver}/build/app/scrcpy" "${pkgdir}/usr/bin/scrcpy"
    install -Dm 644 "${_pkgname}-${pkgver}.jar" "${pkgdir}/usr/local/share/scrcpy/scrcpy-server"
}
