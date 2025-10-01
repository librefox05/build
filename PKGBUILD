_name=librefox
_channel=stable
_lang=en-US
_pkgname="${_name}"
pkgname="librefox"
provides=('librefox')
conflicts=('librefox')
pkgdesc="Librefox browser, made with privacy and usability in mind (${_lang})"
pkgver=143.0.3
pkgrel=1
tag=${pkgver}-1
url="https://github.com/librefox05/releases/releases/download/${tag}/librefox-x86_64-${pkgver}.tar.xz"
arch=('x86_64' 'aarch64')
license=('MPL' 'GPL' 'LGPL')

depends=(
  'dbus-glib'
  'gtk3'
  'libxt'
  'nss'
  'mime-types'
  'python'
)

optdepends=(
  'pulseaudio: audio support'
  'ffmpeg: h.264 video'
  'hunspell: spell checking'
  'hyphen: hyphenation'
  'libnotify: notification integration'
  'networkmanager: location detection via available WiFi networks'
  'speech-dispatcher: text-to-speech'
  'startup-notification: support for FreeDesktop Startup Notification'
)

source=(
  "${_name}.tar.xz::${url}"
  "librefox.desktop"
)

sha256sums=(
  'SKIP'
  'SKIP'
)

package() {
  OPT_PATH="usr/lib/${_pkgname}"

  # Install the package files
  install -d "${pkgdir}"/{usr/bin,usr/lib}
  cp -r ${_name} "${pkgdir}"/${OPT_PATH}
  ln -s "/${OPT_PATH}/${_name}" "${pkgdir}"/usr/bin/${pkgname}

  # Install .desktop files
  install -Dm644 "${srcdir}"/${_name}.desktop -t "${pkgdir}"/usr/share/applications

  # Install icons
  SRC_LOC="${srcdir}"/${_name}/browser
  DEST_LOC="${pkgdir}"/usr/share/icons/hicolor
  for i in 16 32 48 64 128; do
    install -Dm644 "${srcdir}"/${_name}/browser/chrome/icons/default/default${i}.png "${DEST_LOC}"/${i}x${i}/apps/${pkgname}.png
  done

  # Use system-provided dictionaries
  rm -rf "${pkgdir}"/${OPT_PATH}/{dictionaries,hyphenation}
  ln -sf /usr/share/hunspell "${pkgdir}"/${OPT_PATH}/dictionaries
  ln -sf /usr/share/hyphen "${pkgdir}"/${OPT_PATH}/hyphenation
}
