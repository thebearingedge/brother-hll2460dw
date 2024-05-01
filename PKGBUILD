# Maintainer: Tim Davis (contact at timdav dot is)

pkgname="brother-hll2460dw"
pkgver="4.1.0_1"
pkgrel=1
pkgdesc="Brother HL-L2460DW CUPS driver"
arch=("x86_64" "i686")
url="https://www.brother-usa.com/home"
license=("LicenseRef-Brother")
depends=("cups")
source=("https://download.brother.com/welcome/dlf105968/hll2460dwpdrv-4.1.0-1.i386.deb")
sha256sums=("2eef3273c649bb90e858a61de27e69f5dd341324cf0c40a4181d28c886d976a3")

__model="HLL2460DW"

if [ "$CARCH" == "x86_64" ]; then
	depends+=("lib32-glibc")
fi

prepare() {
	tar -xf data.tar.gz -C "${srcdir}"
}

package() {
	mkdir -p "${pkgdir}/usr/share"
	cp -R "${srcdir}/opt/brother" "${pkgdir}/usr/share"

	sed -i 's|\\\/opt\\\/|\\\/usr\\\/|' "${pkgdir}/usr/share/brother/Printers/${__model}/cupswrapper/lpdwrapper"
	sed -i 's|\\\/opt\\\/|\\\/usr\\\/|' "${pkgdir}/usr/share/brother/Printers/${__model}/lpd/lpdfilter"

	install -d "${pkgdir}/usr/lib/cups/filter/"
	ln -s "/usr/share/brother/Printers/${__model}/cupswrapper/lpdwrapper" "${pkgdir}/usr/lib/cups/filter/brother_lpdwrapper_${__model}"

	install -d "${pkgdir}/usr/share/cups/model/"
	ln -s "/usr/share/brother/Printers/${__model}/cupswrapper/brother-${__model}-cups-en.ppd" "${pkgdir}/usr/share/cups/model/"

	ln -s "/usr/share/brother/Printers/${__model}/lpd/$CARCH/brprintconflsr3" "${pkgdir}/usr/share/brother/Printers/${__model}/lpd/"
	ln -s "/usr/share/brother/Printers/${__model}/lpd/$CARCH/rawtobr3" "${pkgdir}/usr/share/brother/Printers/${__model}/lpd/"

	rmdir "${pkgdir}/usr/share/brother/Printers/${__model}/lpd/inf"
	ln -s "/usr/share/brother/Printers/${__model}/inf" "${pkgdir}/usr/share/brother/Printers/${__model}/lpd/inf"
}
