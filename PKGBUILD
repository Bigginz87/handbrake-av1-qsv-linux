# Maintainer: You!
pkgname=handbrake-av1-qsv
pkgver=1.9.2
pkgrel=1
pkgdesc="Multithreaded video transcoder with AV1 QSV CLI support"
arch=('x86_64')
url="https://handbrake.fr/"
license=('GPL')
depends=('gtk4' 'libass' 'libbluray' 'libtheora' 'libvorbis' 'opus' 'speex' 'x264' 'x265' 'jansson' 'libxml2' 'numactl' 'libvpx' 'bzip2' 'zlib' 'libjpeg-turbo' 'libva' 'libvpl')
makedepends=('git' 'cmake' 'nasm' 'python' 'yasm' 'intltool')
provides=('handbrake')
conflicts=('handbrake')
source=("git+https://github.com/HandBrake/HandBrake.git#tag=${pkgver}"
        "av1_qsv_cli.patch")
sha256sums=('SKIP'
            'SKIP')

prepare() {
  cd HandBrake
  patch -p1 < ../av1_qsv_cli.patch
}

build() {
  cd HandBrake
  ./configure --launch-jobs=$(nproc) --launch
  make -C build
}

package() {
  cd HandBrake/build
  make DESTDIR="${pkgdir}" install
}
