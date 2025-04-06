# Maintainer: You!
pkgname=handbrake-av1-qsv
pkgver=1.9.2
pkgrel=2
pkgdesc="Multithreaded video transcoder with AV1 QSV CLI support"
arch=('x86_64')
url="https://handbrake.fr/"
license=('GPL')

depends=(
  'gtk4'
  'libass'
  'libbluray'
  'libtheora'
  'libvorbis'
  'opus'
  'speex'
  'x264'
  'x265'
  'jansson'
  'libxml2'
  'numactl'
  'libvpx'
  'bzip2'
  'zlib'
  'libjpeg-turbo'
  'libva'
  'libvpl'
  'intel-media-sdk'
  'intel-media-driver'
  'libmfx'
)

makedepends=(
  'git'
  'cmake'
  'nasm'
  'python'
  'yasm'
  'intltool'
  'meson'
  # 'cctools'  # removed since it's not in official repos
  'autoconf'
  'automake'
  'libtool'
  'ninja'
  'pkg-config'
)

provides=('handbrake')
conflicts=('handbrake')

source=(
  "git+https://github.com/HandBrake/HandBrake.git#tag=${pkgver}"
  "av1_qsv_cli.patch"
)
sha256sums=('SKIP'
            'SKIP')

prepare() {
  cd HandBrake
  patch -p1 < ../av1_qsv_cli.patch

  # Fix x265 submodule's old cmake policy usage:
  sed -i '/cmake_policy(SET CMP00/d' contrib/x265_8bit/CMakeLists.txt
  sed -i 's/cmake_minimum_required(VERSION 2.8.12)/cmake_minimum_required(VERSION 3.5)/' contrib/x265_8bit/CMakeLists.txt

  # If 10bit/12bit modules exist, fix them too:
  sed -i '/cmake_policy(SET CMP00/d' contrib/x265_10bit/CMakeLists.txt 2>/dev/null || true
  sed -i 's/cmake_minimum_required(VERSION 2.8.12)/cmake_minimum_required(VERSION 3.5)/' contrib/x265_10bit/CMakeLists.txt 2>/dev/null || true

  sed -i '/cmake_policy(SET CMP00/d' contrib/x265_12bit/CMakeLists.txt 2>/dev/null || true
  sed -i 's/cmake_minimum_required(VERSION 2.8.12)/cmake_minimum_required(VERSION 3.5)/' contrib/x265_12bit/CMakeLists.txt 2>/dev/null || true
}

build() {
  cd HandBrake
  ./configure --launch-jobs="$(nproc)" --launch
  make -C build
}

package() {
  cd HandBrake/build
  make DESTDIR="$pkgdir" install
}
