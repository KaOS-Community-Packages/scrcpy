pkgname=scrcpy
pkgver=1.20
pkgrel=1
pkgdesc='Display and control your Android device'
arch=('x86_64')
url='https://github.com/Genymobile/scrcpy'
license=('Apache')
depends=('ffmpeg' 'sdl2' 'android-tools')
makedepends=('meson')
source=("https://github.com/Genymobile/scrcpy/archive/v${pkgver}.tar.gz"
        "scrcpy-server-v${pkgver}.jar::https://github.com/Genymobile/scrcpy/releases/download/v${pkgver}/scrcpy-server-v${pkgver}")
md5sums=('71913fab3c220f067d35b23a10b7f400'
         '04dbf582a9a0a31c00a22023f4088abf')

src_name="scrcpy-${pkgver}"
src_server="scrcpy-server-v${pkgver}.jar"

build() {
    cd "${src_name}"

    rm -rf build
    meson build --buildtype release --strip -Db_lto=true \
        -Dprebuilt_server="../${src_server}"
    cd build
    ninja
}

package() {
    install -Dm 755 "${src_name}/build/app/scrcpy" "${pkgdir}/usr/bin/scrcpy"
    install -Dm 644 "${src_server}" "${pkgdir}/usr/local/share/scrcpy/scrcpy-server"
    mkdir -p "${pkgdir}/usr/bin"
}

