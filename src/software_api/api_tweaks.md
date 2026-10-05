# API Tweaks

The Ferrum App has some settings, known as API Tweaks, that let the user change how Ferrum responds to software
commands. They are controlled by the user, not by software, but developers should be aware of them, as they can change
the result of commands.

In the future, these may able to be controlled via software APIs.

## Move Multiplier

Every software mouse movement, whether sent via the [KM API](./km_api/mouse/axes/move.md), the
[KMBox Net Style API](./kmbox_net_style_api.md), or the [DHZBox Style API](./dhzbox_style_api.md), is multiplied by
the Move Multiplier before being sent to the `Output PC`.

Fractional remainders are not lost. Instead, they are carried over and added to the next movement. For example, with a
multiplier of `0.5`, sending `km.move(1, 0)` twice results in one movement of `0` (not sent), then one movement of `1`.

Any movement that becomes `(0, 0)` after multiplication is not sent. A multiplier of `1` leaves movement unchanged.

## No Button Release

Normally, software releases (such as `km.left(0)` or `km.up(4)`) force the button or key to be released for a short
time, before returning it to its physical state. See [Set Button State](./km_api/mouse/buttons/set_btn_state.md) and
[Set Key State](./km_api/keyboard/keys/set_key_state.md).

When No Button Release is enabled, software releases instead only remove any software press, immediately returning the
button or key to its physical state. If the user is physically holding the button, it stays pressed.

This applies to releases sent via any API. See [The Hardware Override](../hardware_override.md) for more on how
software and physical input interact.
