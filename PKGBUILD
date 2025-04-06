# Maintainer: You!
pkgname=handbrake-av1-qsv
pkgver=1.9.2
pkgrel=1
pkgdesc="Multithreaded video transcoder with AV1 QSV CLI support"
arch=('x86_64')
url="https://handbrake.fr/"
license=('GPL')

# Runtime deps for HandBrake itself, plus QSV (intel-media-sdk, intel-media-driver, libmfx).
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
  'intel-media-sdk'     # QSV runtime
  'intel-media-driver'  # iHD driver for Intel GPU
  'libmfx'              # MFX dispatcher
)

# Build-time deps for building HandBrake with QSV on Arch
makedepends=(
  'git'
  'cmake'
  'nasm'
  'python'
  'yasm'
  'intltool'
  'meson'
  'cctools'     # provides lipo
  'autoconf'
  'automake'
  'libtool'
  'ninja'
  'pkg-config'
)

provides=('handbrake')
conflicts=('handbrake')

# We clone the official HandBrake repo at tag 1.9.2
source=(
  "git+https://github.com/HandBrake/HandBrake.git#tag=${pkgver}"
  "av1_qsv_cli.patch"
)
sha256sums=('SKIP'
            'SKIP')

prepare() {
  cd HandBrake
  # Apply your custom patch enabling AV1 QSV CLI, e.g. adding qsv_av1_10bit, etc.
  patch -p1 < ../av1_qsv_cli.patch
}

build() {
  cd HandBrake
  # HandBrake's 'configure' script will detect meson, cctools (lipo), ninja, etc.
  ./configure --launch-jobs="$(nproc)" --launch
  make -C build
}

package() {
  cd HandBrake/build
  make DESTDIR="${pkgdir}" install
}
