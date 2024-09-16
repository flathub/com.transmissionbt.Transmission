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
* the host filesystem, because Transmission hasn't been adapted to use [portals](https://github.com/flatpak/flatpak/wiki/Portals) to open `.torrent`s and read/write downloads (#31)
* PulseAudio, to play a "ding!" when a transfer is complete
* Notifications, to show a bubble when a transfer is complete
* GVFS, to support opening torrent files by URI
* `org.kde.StatusNotifierWatcher`, to display a notification area icon in environments where this is supported
* `org.gnome.SessionManager`, to inhibit suspend / hibernation while there are active uploads or downloads

## Delta from upstream

* `appdata.patch`: Flathub requires OARS, not yet submitted upstream.
* `0001-gtk-use-com.transmissionbt.Transmission.-D-Bus-names.patch`: Flatpak only allows apps to own names within the namespace matching the app name. Not submitted upstream.
* `0002-gtk-Use-reversed-domain-icon-name-throughout.patch`: as above, but for icons.


## Colophon

This manifest is derived from that published by Pierre Dureau at <https://github.com/pdureau/flatpak-manifests.git>, via an [intermediate version used for Endless OS](https://github.com/endlessm/transmission-flatpak).
