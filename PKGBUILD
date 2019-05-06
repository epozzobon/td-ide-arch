# Maintainer: Your Name <enricopozzobon@gmail.com>
pkgname=td-ide
pkgver=4.4.433
pkgrel=1
epoch=
pkgdesc="Anlogic TD Tang Dynasty FPGA IDE, for the Sipeed Tang Primer development board"
arch=('x86_64')
url="http://www.anlogic.com/down.aspx?TypeId=23&fid=t14:23:14"
license=('unknown')
groups=()
depends=()
makedepends=(unrar)
checkdepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
_sourcearchive="TD1903_linux.rar"
_sourcedir="rel190228_r4.4.433_RHEL"
source=("http://dl.sipeed.com/TANG/Primer/IDE/$_sourcearchive")
noextract=($_sourcearchive)
md5sums=('3d6ba2fa4e512225a2369f9dcc7ec1d9')
validpgpkeys=()
_installdir="/opt/td-ide"

prepare() {
	unrar x -y $_sourcearchive
}

build() {
	cd "$_sourcedir"

# Make a script to launch the IDE in GUI mode
	echo "#!/bin/sh" > "bin/td-ide"
	echo "$_installdir/bin/td -gui \$@" >> "bin/td-ide"

# Make the programs executable
	chmod +x "bin/td"
	chmod +x "bin/td-ide"
}

package() {
# Write udev rules
	mkdir -p "$pkgdir/etc/udev/rules.d"
	echo '# Sipeed Tang Primer' >> "$pkgdir/etc/udev/rules.d/87-tang-primer.rules"
	echo 'ATTR{idVendor}=="0547", ATTR{idProduct}=="1002", MODE="666"' >> "$pkgdir/etc/udev/rules.d/87-tang-primer.rules"

# Move the extracted files into the installation directory
	mkdir "$pkgdir/opt/"
	mv "$_sourcedir" "$pkgdir/$_installdir/"

# Create a symbolic link to start the IDE easily
	mkdir -p "$pkgdir/usr/bin/"
	ln -sr "$pkgdir/$_installdir/bin/td-ide" "$pkgdir/usr/bin/td-ide"
}
