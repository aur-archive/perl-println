# Maintainer: lspci <agm2819[[aaaa]][[tttt]]gmail[[dd]][[oo]][[tt]][[cc]][[oo]][[mm]]>
#
#
pkgname=perl-println
pkgver=0.1.3.2
pkgrel=7
pkgdesc="Perl module that enables you to use println() in your perl.  (Use it as 'use Println')"
arch=('i686' 'x86_64')
url="https://bitbucket.org/agalog/releases"
license=('BSD')
groups=('')
depends=('perl>=5.10.0') 
makedepends=('')
provides=()
conflicts=()
replaces=()
backup=()
options=()
source=("https://bitbucket.org/agalog/releases/downloads/$pkgname-$pkgver.tar.gz")
md5sums=('23cc7dcaeff7002f069b2dbdb6f9665d')

build() {
    cd "$srcdir/$pkgname-$pkgver"
    # if this isn't included then h2xs 'causes break since I don't 
    # want to include the -O (overwite) option in the args for h2xs.  
    if [[ -d "$srcdir/$pkgname-$pkgver/Println" ]]; then
	rm -R -f Println;
	h2xs -AX -n Println # generate the Makefile.PL and similar stuffs
    else
	h2xs -AX -n Println
    fi
    # Setting these env variables overwrites any command-line-options we don't want...
 ( export PERL_MM_USE_DEFAULT=1 PERL_AUTOINSTALL=--skipdeps \
     PERL_MM_OPT="INSTALLDIRS=vendor DESTDIR='$pkgdir'" \
     PERL_MB_OPT="--installdirs vendor --destdir '$pkgdir'" \
     MODULEBUILDRC=/dev/null
     
   cd Println
   /usr/bin/perl Makefile.PL
   make
 )
}
check() {
      cd "$srcdir/$pkgname-$pkgver"
      cd Println
     ( export PERL_MM_USE_DEFAULT=1 PERL5LIB=""
       make test
     )
}

package() {
    cd "$srcdir/$pkgname-$pkgver"
    cd Println
    make install
    find "$pkgdir" -name .packlist -o -name perllocal.pod -delete
    cd .. 
    if [[ -e "$pkgdir/usr/share/man/man3/Println.3pm.gz" ]]; then 
	rm -f "$pkgdir/usr/share/man/man3/Println.3pm.gz";
    fi
    if [[ -e "$pkdir/usr/share/man/man3/Println.3pm" ]]; then
	cd "$pkdir/usr/share/man/man3/";
	rm -f "Println.3pm";
    fi
    if [[ -e "$pkdir/usr/share/perl5/vendor_perl/Println.pm" ]]; then
	cd "$pkgdir/usr/share/perl5/vendor_perl/"
	rm -f "Println.pm";
    fi
    cd "$srcdir/$pkgname-$pkgver"

    cp "$srcdir/$pkgname-$pkgver/Println.3pm" "$pkgdir/usr/share/man/man3/";
    cp "$srcdir/$pkgname-$pkgver/Println.pm" "$pkgdir/usr/share/perl5/vendor_perl/";
    pwd
#    install -d "$pkgdir/usr/share/man/man3/"
    install -m 644 -D Println.3pm "$pkgdir/usr/share/man/man3/Println.3pm"
    install -m 644 -D Println.pm "$pkgdir/usr/share/perl5/vendor_perl/Println.pm";
}

