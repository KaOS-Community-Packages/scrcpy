pkgname=scrcpy
pkgver=1.19
pkgrel=1
pkgdesc='Display and control your Android device'
arch=('x86_64')
url='https://github.com/Genymobile/scrcpy'
license=('Apache')
depends=('ffmpeg' 'sdl2' 'android-tools')
makedepends=('meson')
source=("https://github.com/Genymobile/scrcpy/archive/v${pkgver}.tar.gz"
        "scrcpy-server-v${pkgver}.jar::https://github.com/Genymobile/scrcpy/releases/download/v${pkgver}/scrcpy-server-v${pkgver}")
md5sums=('3f362edb5ac7d66db5ad979cf71fa698'
         '79237c00052d7a35c4fc4d172eaf5ae0')

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

