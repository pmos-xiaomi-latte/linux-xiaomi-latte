# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/x86_64/configs/(CHANGEME!)

pkgname=linux-xiaomi-latte
pkgver=3.14.79
pkgrel=0
pkgdesc="Xiaomi Mi Pad 2 kernel fork"
arch="x86_64"
_carch="x86_64"
_flavor="xiaomi-latte"
url="https://kernel.org"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="
	bash
	bc
	bison
	devicepkg-dev
	flex
	openssl-dev
	perl
"

# Source
_repository="android_kernel_xiaomi_latte"
_commit="d2afb1de9a761ff01dafdf9efe4736e521ab71f6"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/latte-dev/$_repository/archive/$_commit.tar.gz
	$_config
	x86-relocs-Make-per_cpu_load_addr-static.patch
	gcc7-give-up-on-ilog2-const-optimizations.patch
	gcc8-fix-put-user.patch
	gcc10-extern_YYLOC_global_declaration.patch
"
builddir="$srcdir/$_repository-$_commit"
_outdir="out"

prepare() {
	default_prepare
	. downstreamkernel_prepare
}

build() {
	unset LDFLAGS
	make O="$_outdir" ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
	downstreamkernel_package "$builddir" "$pkgdir" "$_carch" \
		"$_flavor" "$_outdir"
}

sha512sums="
bf71e4161a55574a9fcdc11e175137cad304985cb168e47e8633d35b1ebb5dfac06ce5a578f1ec06fbb580b22902b0f810165a7506eec02acd3bb4b84d476b59  linux-xiaomi-latte-d2afb1de9a761ff01dafdf9efe4736e521ab71f6.tar.gz
e2ccc1c77e1f408228ac03705794d9fd1963780c3f8f908f25cefcab29b19c4132bc6c5ff0a896c858701fd4ba84860645b28b9a2505638e1cc2dac5592a288c  config-xiaomi-latte.x86_64
08e13b88b043e6de0ff1e563487e1d0292c1fd54160a6384448934dd83776d1f4f7b3f3a1bf5b4471320336026d59efa55b14f3ca3982d4170df0aca3066e955  x86-relocs-Make-per_cpu_load_addr-static.patch
77eba606a71eafb36c32e9c5fe5e77f5e4746caac292440d9fb720763d766074a964db1c12bc76fe583c5d1a5c864219c59941f5e53adad182dbc70bf2bc14a7  gcc7-give-up-on-ilog2-const-optimizations.patch
197d40a214ada87fcb2dfc0ae4911704b9a93354b75179cd6b4aadbb627a37ec262cf516921c84a8b1806809b70a7b440cdc8310a4a55fca5d2c0baa988e3967  gcc8-fix-put-user.patch
2b48f1bf0e3f70703d2cdafc47d5e615cc7c56c70bec56b2e3297d3fa4a7a1321d649a8679614553dde8fe52ff1051dae38d5990e3744c9ca986d92187dcdbeb  gcc10-extern_YYLOC_global_declaration.patch
"
