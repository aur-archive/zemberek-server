# Maintainer: Atilla ÖNTAŞ <tarakbumba@gmail.com>
# Contributor: Samed Beyribey <ras0ir@eventualis.org>

pkgname=zemberek-server
pkgver=0.7.1
pkgrel=13
url="http://code.google.com/p/zemberek"
pkgdesc='A Turkish spell checker server based on Zemberek NLP library'
arch=('i686' 'x86_64')
license=('MPL')
provides=('zemberek-server-nolibs')
groups=('zemberek')
replaces=('zemberek-server-nolibs')
conflicts=('zemberek-server-nolibs')
depends=('java-runtime' 'dbus' 'libmatthew-java' 'dbus-java' 'apache-mina' 'zemberek' 'libenchant-zemberek')
makedepends=('apache-ant' 'java-environment' 'dbus-java' 'apache-mina' 'zemberek')
source=(http://zemberek.googlecode.com/files/zemberek-server-nolibs-$pkgver.tar.gz
	zemberek-server
	zemberek-server.service)
	
md5sums=('769345191af0f28afc780d7306c87cd0'
         '00e10389c3c79e4f15ee6e338af6dd42'
         '52c4645cc72c930c16c86184204d21c7')
build() {
	install -d  $pkgdir/etc/dbus-1/system.d
	install -d  $pkgdir/usr/share/java/zemberek
	install -d  $pkgdir/usr/share/licenses/$pkgname
	cd $srcdir
	
	# Export java path, only needed for OBS builds
	# export JAVA_HOME=/usr/lib/jvm/java-7-openjdk
    
	mkdir lib
	jars=(/usr/share/java/dbus-java/dbus.jar /usr/share/java/mina/mina-core.jar /usr/share/java/zemberek/zemberek-cekirdek.jar /usr/share/java/zemberek/zemberek-tr.jar)
	for lnjars in ${jars[@]}
	do ln -s $lnjars lib/
	done
	
# Build 'em
	ant
}

package() {
	install -D -m644 $srcdir/dist/config/conf.ini $pkgdir/etc/zemberek-server.ini
	install -m644 dist/config/zemberek-server.conf $pkgdir/etc/dbus-1/system.d
	install -m644 dist/zemberek-server-$pkgver.jar $pkgdir/usr/share/java/zemberek/zemberek-server.jar
	install -m644 dist/lisanslar/zemberek-licence.txt $pkgdir/usr/share/licenses/$pkgname
	install -D -m655 $startdir/zemberek-server $pkgdir/usr/bin/zemberek-server
        install -D -m644 $startdir/zemberek-server.service $pkgdir/usr/lib/systemd/system/zemberek-server.service
}
