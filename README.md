# Librefox Build Repository
Librefox is a modified version of firefox, it is a customized project which includes different preferences that respect user privacy as much as possible. We use preferences from betterfox and cachyOS.

Here all the configuration of Librefox are stored and Librefox is built here through `github actions` for the sake of transparency.

The public repository can be located [here](https://github.com/librefox05/librefox_repo)

## Usage
To use librefox builds, add this repo in pacman by pasting the following

```
[librefox_repo]
SigLevel = Optional DatabaseOptional
Server = https://github.com/librefox05/$repo/raw/refs/heads/main/$arch
```

then run
```
sudo pacman -Syy firefox-stable-bin
```

