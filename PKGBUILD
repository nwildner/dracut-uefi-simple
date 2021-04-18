# Maintainer: Nícolas Wildner <nicolasgaucho@gmail.com>

pkgname=dracut-uefi-simple
pkgver=1
pkgrel=0
pkgdesc="Install/update hooks for dracut unifed uefi image made simple"
arch=(x86_64)
license=('MIT')
depends=(dracut systemd)
source=('90-dracut-uefi-install.hook'
        'dracut-uefi-simple')
sha256sums=('292160c3feafcd882d6eb9dd2e20ce111997dc21336df204cee2965d69126701'
            'f40d53a786b8833e59e71e5bcdb57d6c6134137a6dfa7e0c521f9d3743cb3ff0')

package() {
  install -Dm644 "${srcdir}/90-dracut-uefi-install.hook" "${pkgdir}/usr/share/libalpm/hooks/90-dracut-uefi-install.hook"
  install -Dm755 "${srcdir}/dracut-uefi-simple"          "${pkgdir}/usr/share/libalpm/scripts/dracut-uefi-simple"
}
