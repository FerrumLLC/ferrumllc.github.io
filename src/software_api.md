# Software API

The Software API is the more modern, high-performance, and advanced API available on Ferrum. It supports not only KM
style commands (over a serial port), but also KMBox Net style commands (over a UDP Socket), DHZBox style commands (over a
UDP socket), as well as a variety of custom commands.

It is made up of the following APIs:

- [Keyboard Mouse API](software_api/km_api.md) - Simple commands to control and read the mouse and keyboard, over the
  serial port.
- [Mouse Proxy API](software_api/mouse_proxy_api.md) - Intercept and modify every frame of mouse input, over the serial
  port.
- [KMBox Net Style API](software_api/kmbox_net_style_api.md) - Compatibility with KMBox Net software, over the UDP
  socket.
- [DHZBox Style API](software_api/dhzbox_style_api.md) - Compatibility with DHZBox software, over the UDP socket.

The user can also change how some commands behave via [API Tweaks](software_api/api_tweaks.md).

The following sections provide information and pseudocode examples for the different commands available.
