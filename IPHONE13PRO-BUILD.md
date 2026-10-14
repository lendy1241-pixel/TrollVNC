# iPhone 13 Pro / iOS 15 / TrollStore build

Upstream: https://github.com/owngoal-dev/TrollVNC

Base commit: `a3e40816ea5b93a7c80c09625175893d15bd1070`

The recommended workflow is **Build iPhone 13 Pro TrollStore app**. It builds an
IPA-format `.tipa` using upstream's `bootstrap` scheme on macOS 15, Xcode 16.2
and a pinned Theos checkout. It verifies app layout, iOS 15 compatibility,
Mach-O build metadata, code-signing entitlements and SHA-256 checksum.
Install the result directly with TrollStore. Filza and PreferenceLoader are
not required. The previous rootless Debian workflow remains available separately.

## Changes

- First-install, editable defaults: full resolution, a 60 Hz capture target,
  8 ms update coalescing, one in-flight update, clipboard and orientation sync.
  Actual frame rate and end-to-end latency still require testing on the phone.
- `winctrl` maps Windows Control to iOS Command so common editing shortcuts use
  Ctrl+C/V/A/X/Z. The original `std` and `altcmd` modes remain available.
- Opening the app starts the upstream background manager. No SSH session or
  terminal window is needed for everyday use. Open the app again if the service
  is not running after a phone restart.
- On a first install the server is disabled. Set a full-access password and enable
  it once inside the TrollVNC app. No password is embedded in source or CI output.
- Bundled defaults are persisted for the separate server process on app startup;
  existing values are preserved and settings remain editable.

## Install and use

1. Download the `TrollVNC-iPhone13Pro-TrollStore` artifact from the completed build.
2. Open the contained `.tipa` with TrollStore and install it.
3. Open TrollVNC, set a full-access password, enable the server and tap Apply.
4. Connect a Windows VNC viewer to the phone's LAN IP, TCP port 5901.
5. Keep the same phone LAN IP (for example, a DHCP reservation) and save a viewer
   connection profile for one-click connections on subsequent days.

This package is GPLv2, like upstream. See `COPYING` and the complete source here.
