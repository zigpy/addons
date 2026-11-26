# Changelog

## 0.5.1

 - Fix `Missing required option 'network_address'` error when updating or starting
   the app without a network address set.

## 0.5.0

 - Bump ziggurat to 81ec8c05.
 - Add Green Power frame TX support.
 - Better routing in large meshes: fewer route request floods, more accurate link
   quality estimates, and faster recovery when a route breaks.
 - Ziggurat now tries to reconnect to the radio for up to 30 seconds when the
   connection drops (e.g. a brief USB disconnect) or the radio stops responding,
   instead of restarting at once.
 - Devices that leave and rejoin the network are handled more reliably.
 - Routers are less likely to be dropped as neighbors by mistake.
 - Fixes for devices that could get stuck partway through joining.
 - Adds a `network_address` option to connect to the RCP over a raw TCP socket
   (`tcp://host:port`, e.g. a network-attached RCP or a `ser2net`-style
   serial-to-TCP bridge) instead of a local serial device. Wi-Fi-connected radios
   are not recommended — see [zigpy/ziggurat#39](https://github.com/zigpy/ziggurat/pull/39).

## 0.4.0

 - Bump ziggurat to 1e319a4c.
 - Requires Home Assistant 2026.11.0b0 or newer.
 - Indicate to the client if incoming packets were APS encrypted.
 - Add Green Power frame RX support.
 - Clear End Device Initiator when relaying an end device child's frame.

## 0.3.1

 - Bump ziggurat to 816f6331.
 - The stack now owns the APS sequence number instead of accepting it from zigpy.
 - Allow duplicate pending APS ACKs.

## 0.3.0

 - Bump ziggurat to 96face24.
 - Routing hints API for fast startup with ZHA.
 - Switch from the JSON API to the binary transport API.
 - Properly send the transport key to joining Zigbee 3.0 devices.
 - Many other fixes.

## 0.2.0

 - Bump ziggurat to the 0.1.0 release on crates.io.
 - Routing and path cost fixes, in addition to frame parser hardening.

## 0.1.1

 - Bump ziggurat to 6e0df44f.
 - Adds energy + network scanning APIs and the ability to permit joins on just a single router.

## 0.1.0

- Initial release
