_name=firefox
_channel=stable
_lang=en-US
_pkgname="${_name}"
pkgname="librefox"
provides=('librefox')
conflicts=('librefox' 'firefox-stable-bin' 'firefox')
pkgdesc="Fast, Private & Safe Web Browser from Mozilla — With better defaults (${_lang})"
url="https://download.mozilla.org/?product=${_name}-latest&os=linux64"
pkgver=140.0.2
pkgrel=2
arch=('x86_64' 'aarch64')
license=('MPL' 'GPL' 'LGPL')
conflicts=('firefox')

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

## copy conifgs to current directory
cp -f configs/* .

source=(
  "${_name}.tar.xz::${url}"
  "firefox.desktop"
  "policies.json"
  "firefox.cfg"
  "autoconfig.js"
)

validpgpkeys=('14F26682D0916CDD81E37B6D61B7B526D98F0353') # Mozilla’s GnuPG release key

sha256sums=(
  '0de987e3065409d7feeba28e8b9c59c8270b917a293c140a5423579c7e70f8ce'
  'SKIP'
  'SKIP'
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
  install -Dm644 "${srcdir}"/${_name}.cfg -t "${pkgdir}"/${OPT_PATH}
  install -Dm644 "${srcdir}"/autoconfig.js -t "${pkgdir}"/${OPT_PATH}/defaults/pref

  # Install icons
  SRC_LOC="${srcdir}"/${_name}/browser
  DEST_LOC="${pkgdir}"/usr/share/icons/hicolor
  for i in 16 32 48 64 128; do
    install -Dm644 "${SRC_LOC}"/chrome/icons/default/default${i}.png "${DEST_LOC}"/${i}x${i}/apps/${pkgname}.png
  done

  # Disable auto-updates
  install -Dm644 "${srcdir}"/policies.json -t "${pkgdir}"/${OPT_PATH}/distribution

  # Use system-provided dictionaries
  rm -rf "${pkgdir}"/${OPT_PATH}/{dictionaries,hyphenation}
  ln -sf /usr/share/hunspell "${pkgdir}"/${OPT_PATH}/dictionaries
  ln -sf /usr/share/hyphen "${pkgdir}"/${OPT_PATH}/hyphenation
}
