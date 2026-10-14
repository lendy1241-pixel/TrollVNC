# iPhone 13 Pro / iOS 15 / Dopamine build

Upstream: https://github.com/owngoal-dev/TrollVNC

Base commit: `a3e40816ea5b93a7c80c09625175893d15bd1070`

This build produces a rootless `iphoneos-arm64` Debian package for Dopamine.
The GitHub workflow is **Build iPhone 13 Pro rootless**. It builds on macOS 15
with Xcode 16.2 and a pinned Theos checkout, then verifies the package layout,
Mach-O build metadata, code-signing entitlements and SHA-256 checksum.

## Changes

- First-install, editable defaults: full resolution, a 60 Hz capture target,
  8 ms update coalescing, one in-flight update, clipboard and orientation sync.
  Actual frame rate and end-to-end latency still require testing on the phone.
- `winctrl` maps Windows Control to iOS Command so common editing shortcuts use
  Ctrl+C/V/A/X/Z. The original `std` and `altcmd` modes remain available.
- The daemon starts through the upstream launchd registration after jailbreaking.
  No SSH session or terminal window is needed for everyday use.
- On a first install the server is disabled. Set a full-access password and enable
  it once in Settings -> TrollVNC. No password is embedded in source or CI output.
- Existing user preferences are preserved when upgrading or reinstalling.

## Install and use

1. Download the `TrollVNC-iPhone13Pro-rootless` artifact from the completed build.
2. Install the `.deb` on the jailbroken phone and respring if needed for Settings.
3. Open Settings -> TrollVNC, set a full-access password, then enable the server.
4. Connect a Windows VNC viewer to the phone's LAN IP, TCP port 5901.
5. Keep the same phone LAN IP (for example, a DHCP reservation) and save a viewer
   connection profile for one-click connections on subsequent days.

This package is GPLv2, like upstream. See `COPYING` and the complete source here.
