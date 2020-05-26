# Flatpak manifest for Transmission

Transmission is a BitTorrent client ([website](https://transmissionbt.com/), [Git](https://github.com/transmission/transmission)). This is a [Flatpak](http://flatpak.org/) manifest for its [Gtk+](https://www.gtk.org/) version; you can install it through [Flathub](https://flathub.org/).

## Building and testing locally

```console
$ git submodule update --init
$ rm -rf _build && flatpak-builder --install --user _build com.transmissionbt.Transmission.json
$ flatpak run com.transmissionbt.Transmission//master
```

## Permissions

This manifest allows Transmission access to:

* the network, for obvious reasons
* X11 and Wayland, also for obvious reasons
* the host filesystem, because Transmission hasn't been adapted to use [portals](https://github.com/flatpak/flatpak/wiki/Portals) to open `.torrent`s and read/write downloads
* PulseAudio, to play a "ding!" when a transfer is complete
* Notifications, to show a bubble when a transfer is complete
* DConf, because Gtk's file chooser tries to save its position, visible columns, etc.

## Delta from upstream

* `com.transmissionbt.Transmission.appdata.xml`: [accepted upstream](https://github.com/transmission/transmission/pull/224) but not yet part of a release.
* `0001-gtk-use-com.transmissionbt.Transmission.-D-Bus-names.patch`: Flatpak only allows apps to own names within the namespace matching the app name. Not submitted upstream.


## Colophon

This manifest is derived from that published by Pierre Dureau at <https://github.com/pdureau/flatpak-manifests.git>, via an [intermediate version used for Endless OS](https://github.com/endlessm/transmission-flatpak).
