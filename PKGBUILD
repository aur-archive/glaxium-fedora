# Maintainer: Simone Sclavi 'Ito' <darkhado@gmail.com> 
pkgname=glaxium-fedora
__pkgalias=glaxium
pkgver=0.5
pkgrel=7
__patch=14
__fc=fc18
pkgdesc="An OpenGL space shooter with Fedora's patches"
arch=('i686' 'x86_64')
url='https://admin.fedoraproject.org/community/?package=glaxium#package_maintenance/package_overview'
license=('GPL')
makedepends=('rpmextract')
depends=('sdl_mixer' 'freeglut' 'libxmu' 'libpng' 'glu')
conflicts=('glaxium')
source=(            
http://kojipkgs.fedoraproject.org/packages/${__pkgalias}/${pkgver}/${__patch}.${__fc}/src/${__pkgalias}-${pkgver}-${__patch}.${__fc}.src.rpm
)
md5sums=('0d4b91dda7e8b415e3817f43c3182754')

build() {
    rpmextract.sh ${__pkgalias}-${pkgver}-${__patch}.${__fc}.src.rpm
    bsdtar -zxf ${__pkgalias}_${pkgver}.tar.gz
    cd ${__pkgalias}_${pkgver}
    patch -Np1 -i ../${__pkgalias}-0.5-fixes.patch
    patch -Np1 -i ../${__pkgalias}_0.5-allow-running-when-dsp-busy.patch
    patch -Np1 -i ../${__pkgalias}_0.5-glutInit.patch
    patch -Np1 -i ../${__pkgalias}_0.5-rh553067.patch
    patch -Np1 -i ../${__pkgalias}_0.5-64bit-crash.patch
    patch -Np1 -i ../${__pkgalias}_0.5-fighter2_meshes-fix.patch
    sed -i 's|/games/glaxium|/glaxium|g' configure* Makefile.in
    ./configure --prefix=/usr
    make
}

package(){
    cd ${__pkgalias}_${pkgver}
    install -Dm755 glaxium $pkgdir/usr/bin/glaxium
    mkdir -p $pkgdir/usr/share/glaxium/{samples,textures}
    install -m644 samples/* $pkgdir/usr/share/glaxium/samples
    install -m644 textures/* $pkgdir/usr/share/glaxium/textures

    cd $srcdir
    mkdir -p $pkgdir/usr/share/{applications,pixmaps}
    install -m644 glaxium.png $pkgdir/usr/share/pixmaps
    sed 's:glaxium-wrapper:glaxium:' -i glaxium.desktop
    install -m644 glaxium.desktop $pkgdir/usr/share/applications
}           


