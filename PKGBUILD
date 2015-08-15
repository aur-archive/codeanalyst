# Maintainer: Felipe Bugno <capent@yahoo.com>

pkgbase=CodeAnalyst
pkgname=codeanalyst
pkgver=3_3_18_0361
pkgrel=4
pkgdesc="AMD Code Analyst performance profiler"
url="http://www.amd.com/"
arch=('i686' 'x86_64')
license=('GPL')
depends=('gcc' 'sudo' 'qt>=4.1')
makedepends=('gcc' 'linux-headers' 'binutils' 'elfutils' 'popt>=1.16')
conflicts=('oprofile')
replaces=()
backup=()
options=('!strip')
install=codeanalyst.install
source=("http://download2-developer.amd.com/amd/CodeAnalyst/CodeAnalyst3_3_18_0361Public.tar.gz"
	'gcc47.patch'
	'skipSetup.patch'
	'codeanalyst.install'
	'codeanalyst.svg')

sha1sums=('ddb397eb106af1c0777517ee7233ffc7fc5c9f05'
         'eb7dc01733a66ee4c55e083ddccfd61d7ba9f552'
         '9773bd7f06a8f7b3f08a5dd48808b31fea46258c'
         '4a7eb91c895d347e3f3a397818e0b1f50178f177'
         '99f93507b3c52ff6c31d0aa27d729cb608fb3625')

build() {
  cd $startdir/src/$pkgbase-$pkgver-Public
  chmod u+w src/ca/cg/Makefile.am
  chmod u+w src/ca/gui/MonitorDockView.cpp
  chmod u+w src/ca/libs/libca/dwarfengine.cpp
  chmod u+w src/ca/libs/libopdata/opdata_handler.cpp
  chmod u+w src/ca_agent/libCAagent/slock.cpp
  chmod u+w src/ca/Makefile.am
  chmod u+w src/ca_agent/jvmpi/Makefile.am
  chmod u+w src/Makefile.am
  patch -Np1 -i "${srcdir}/gcc47.patch" || return 1
  patch -Np1 -i "${srcdir}/skipSetup.patch" || return 1
  
  ./autogen.sh
  ./configure --prefix=/usr
  make || return 1
  make DESTDIR=$startdir/pkg install || return 1
  strip $startdir/pkg/usr/bin/calog_report
  strip $startdir/pkg/usr/bin/calog_report
  strip $startdir/pkg/usr/bin/cgreport
  strip $startdir/pkg/usr/bin/CodeAnalyst
  strip $startdir/pkg/usr/bin/opannotate
  strip $startdir/pkg/usr/bin/oparchive
  strip $startdir/pkg/usr/bin/opgprof
  strip $startdir/pkg/usr/bin/ophelp
  strip $startdir/pkg/usr/bin/opimport
  strip $startdir/pkg/usr/bin/opjitconv
  strip $startdir/pkg/usr/bin/opreport
  strip $startdir/pkg/usr/bin/oprofiled
  strip $startdir/pkg/usr/sbin/*
  
  mkdir -p ${pkgdir}/usr/share/icons/hicolor/scalable/apps/
  cp ${startdir}/codeanalyst.svg ${pkgdir}/usr/share/icons/hicolor/scalable/apps/
}
