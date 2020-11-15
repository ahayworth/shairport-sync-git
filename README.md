This is a personal copy of the archlinux PKGBUILD for [shairport-sync](https://github.com/mikebrady/shairport-sync)

Notably, this version drops optional Apple ALAC dependency: [according to the maintainer](https://github.com/mikebrady/shairport-sync/issues/483), there is no reason to prefer it over the built-in ALAC support.

This version compiles in support for the following:
  - ALSA backend
  - Pulseaudio backend
  - STDOUT backend
  - Pipe backend
  - Jack backend
  - Avahi
  - DNS-SD
  - SOXR interpolation
  - Convolution
  - Metadata
  - DBUS interface
  - MPRIS interface
  - MQTT client
  - systemd
