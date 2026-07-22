# Changelog

## 0.3.0

 - Adds a `network_address` option to connect to the RCP over a raw TCP socket
   (`tcp://host:port`, e.g. a network-attached RCP or a `ser2net`-style
   serial-to-TCP bridge) instead of a local serial device. Wi-Fi-connected radios
   are not recommended — see [zigpy/ziggurat#39](https://github.com/zigpy/ziggurat/pull/39).
 - Targets the next zigpy/ziggurat release (past the current 0.1.0 on crates.io,
   which predates the change above); the `ZIGGURAT_VERSION` build arg will need
   confirming against whatever version is actually published.

## 0.2.0

 - Bump ziggurat to the 0.1.0 release on crates.io.
 - Routing and path cost fixes, in addition to frame parser hardening.

## 0.1.1

 - Bump ziggurat to 6e0df44f.
 - Adds energy + network scanning APIs and the ability to permit joins on just a single router.

## 0.1.0

- Initial release
