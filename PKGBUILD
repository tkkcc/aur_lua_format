# Maintainer: bilabila <bilabila@qq.com>
_src=LuaFormatter
_pkg=lua-format
_pkgver=1.3.3
_lib=args
_libver=6.2.2
_patch=lib.patch
pkgname=$_pkg-ext
pkgver=$_pkgver
pkgrel=1
pkgdesc='LuaFormatter with extended identifiers'
arch=(x86_64)
url=https://github.com/Koihik/LuaFormatter
provides=($_pkg-ext $_pkg $_src)
conflicts=($_pkg-ext $_pkg $_src)
license=(Apache2)
depends=(antlr4-runtime yaml-cpp)
makedepends=(antlr4 cmake)
source=($_pkg-$pkgver::https://github.com/Koihik/$_src/archive/$_pkgver.tar.gz
  $_lib-$_libver::https://github.com/Taywee/$_lib/archive/$_libver.tar.gz
  $_patch
  ext.patch
)
sha512sums=(e9dc1ae7f05aac99af66dd61f71c00f2511db96cc65219a9ac9f777196cd688b093f867a0565627cf47f3c0416b1475cd4ecdd2ffcc88048842a5f93bbe5bbdb
  29b0f53316fe35f65ab92c807180c1e6cc6084dfed9f635aa2e3e848137ee8e5d24ec6831cf19189c6432335f73d1466564e0bc9bc259c98f3f0de264637f971
  ccc16949cceb6bb6a0961694921105e80fba3b478cc34d522d57277d5bbedfafeeb2d9638225fcbe9ae8d87cf01696eb22872e88cce078bdcc600bbef3c5efbd
  8747d10775b34b8e413263439b1284bd524ef0ef867e3646774cb5ed4dddf008f852b7a2b6f8a6a1492739a7f931d57e6346cb8b65e00542b7aa8d0b868a4ebc
)
_src=$_src-$pkgver
prepare() {
  cd $_src
  rm -rf third_party/$_lib
  ln -sr ../$_lib-$_libver third_party/$_lib
  patch -Np1 -i ../$_patch
  patch -Np1 -i ../ext.patch
}
build() {
  cd $_src
  antlr4 -Dlanguage=Cpp -no-listener -visitor -o generated Lua.g4
  cmake -D BUILD_TESTS=OFF COVERAGE=OFF .
  make
}
package() {
  install -Dm644 $_src/LICENSE "$pkgdir"/usr/share/licenses/$_pkg/LICENSE
  install -Dm755 $_src/$_pkg "$pkgdir"/usr/bin/$_pkg
}
