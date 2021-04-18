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
sha256sums=('d71ac28d73220c5cb4b9d4761630a273c5e0d408a8cce96f83450e5af3180643'
            'ad319cdf2c21f7904243111754dd564de1edbf1130a1ed49e92402917748f3c8')

package() {
  install -Dm644 "${srcdir}/90-dracut-uefi-install.hook" "${pkgdir}/usr/share/libalpm/hooks/90-dracut-uefi-install.hook"
  install -Dm755 "${srcdir}/dracut-uefi-simple"          "${pkgdir}/usr/share/libalpm/scripts/dracut-uefi-simple"
}
