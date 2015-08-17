# Maintainer: Brian Szmyd <brian.szmyd@rightscale.com>
# Contributor: Chris Fordham <chris.fordham@rightscale.com>

pkgname=rightscale-rightlink
pkgver=5.8.13
pkgrel=2
pkgdesc='RightScale RightLink cloud instance agent.'
arch=('i686' 'x86_64' 'armv6h')
url=http://rightscale.com/
license=(MIT RUBY)
depends=()
makedepends=(autoconf git tar patch)
conflicts=(rightscale-deb)
options=(emptydirs strip !docs !libtool !staticlibs)

_gitname=right_link
_rl_prefix="/opt/rightscale"

source=(
  "${_gitname}::git://github.com/rightscale/right_link.git"
  LICENSE
  system_configurator.rb.patch
  server_importer.rb.patch)
	
md5sums=('SKIP'
         '3f31b6f7aba7c235143e0594a7ef1230'
         'ea36f42257352c44f5240ed67e36f4fb'
         'e47fadba0866d2773ba9d2cc124e112e')		 # generate with 'makepkg -g'

package() {
	mkdir -p ${pkgdir}/${_rl_prefix}/right_link
	
	msg 'Installing RightLink into package...'
	pushd ${srcdir}/$_gitname
		git archive --format=tar v${pkgver} | tar -C ${pkgdir}/${_rl_prefix}/${_gitname} -x
	popd

	cd "$pkgdir"
	msg "Applying patch for system_configurator.rb..."
	patch -p0 < "$startdir/system_configurator.rb.patch"

	msg "Applying patch for server_importer.rb..."
	patch -p0 -R --no-backup-if-mismatch < "$startdir/server_importer.rb.patch"

  msg 'Adding LICENSE to package...'
	install -D "$startdir/LICENSE" "$pkgdir/usr/share/rightscale-rightlink/LICENSE"
}

# vim:syntax=sh