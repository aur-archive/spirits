# Maintainer: Zachary A. Jones <JazzplayerL9@gmail.com>
pkgname=spirits
pkgver=1.0.1
_pkgverext=120903-1348705231
pkgrel=1
pkgdesc="Lemmings-like 2-D Puzzle Game.  Requires purchase or Humble Bundle Key."
arch=('i686' 'x86_64')
url="http://spacesofplay.com/spirits.html"
license=('custom')
depends=(openal mesa gtk2)
makedepends=('curl')
PKGEXT='.pkg.tar'
groups=('humble-android3-bundle' 'games')
source=("spirits-linux-${pkgver}_${_pkgverext}.zip::https://www.humblebundle.com/login"
        "spirits-linux-${pkgver}_${_pkgverext}.zip::http://www.humblebundle.com/downloads?key=${_humbleand3bundlekey}" 
        "$pkgname.desktop")
case "$CARCH" in
    i686) _arch=x86_64
	  _archnum=64
    ;;
    x86_64) _arch=x86
	    _archnum=32
    ;;
esac

_char=\'
DLAGENTS=('https::/bin/echo %o > /tmp/arch && sed -i "s/.part//" /tmp/arch &&
 /usr/bin/curl -s --cookie-jar /tmp/cjar --output /dev/null %u && cp /tmp/cjar ./ &&
 /usr/bin/curl -sL --cookie /tmp/cjar --cookie-jar /tmp/cjar --data "username=$_humbleemail" --data "password=$_humblepassword" %u |
 grep -f /tmp/arch |grep -o -E "data-web=[^ ]+"| sed -e "s/data-web=\([^ ]*\)/\1/" > /tmp/url &&
 sed -i "s/$_char//g" /tmp/url &&
 /usr/bin/curl --cookie /tmp/cjar --cookie-jar /tmp/cjar -fLC -  --retry 3 --retry-delay 3 -o %o "$(</tmp/url)" &&
 rm -f /tmp/{arch,url} || return 0'
            "http::/usr/bin/curl -sL %u | grep spirits-linux | sed -e \"s/.*data-web='\([^']*\)'.*/url = \1/\" > /tmp/url && /usr/bin/curl -fLC -  --retry 3 --retry-delay 3 -o %o -K /tmp/url && rm /tmp/url")

if [[ ! -f "$SRCDEST"/"${source[0]%%:*}" ]]; then
    if [[ -z "$_humbleemail" || -z "$_humblepassword" ]]; then
        if [[ -z "$_humbleand3bundlekey" ]]; then
            msg "if you have bound your email and password to your account, "
            msg "please export the values _humbleemail and _humblepassword so"
            msg "that you can be logged in to download the game."
            echo
            msg "if you have not bound the key to an email, "
            msg "please export _humbleand3bundlekey in your .bashrc"
            return 1
        fi
    fi
fi

_archive_name="Spirits"
_archive="${pkgname}-linux-${pkgver//_/-}.zip"

build() {
  cd "${srcdir}"
  rm -rf "${srcdir}/${_archive_name}/${_arch}"
  rm "${srcdir}/${_archive_name}/${_archive_name}-${_archnum}"

  install -d "${pkgdir}"/opt/ "${pkgdir}"/usr/bin/ "${pkgdir}"/usr/share/applications/ "${pkgdir}"/usr/share/licenses/spirits/
  cp -dpr --no-preserve=ownership "${srcdir}/${_archive_name}" "${pkgdir}"/opt/

  install -Dm644 "${srcdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/$pkgname.desktop"
  cp -dpr --no-preserve=ownership "${srcdir}/${_archive_name}/LICENSES.TXT" "${pkgdir}/usr/share/licenses/spirits/LICENSE"

  ln -s "/opt/${_archive_name}/${_archive_name}" "${pkgdir}/usr/bin/${pkgname}"
  chmod 755 "${pkgdir}/opt/${_archive_name}/${_archive_name}"

}
md5sums=('609ac3dacd0599f7eb5144db77a2e563'
	 '609ac3dacd0599f7eb5144db77a2e563'
         '6e81e27e79cd3dee98f683f68cbfe03f')
