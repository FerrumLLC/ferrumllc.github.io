# Controller Buttons Callback

## Documentation

The `km.controller_buttons` command is used to enable and disable the Controller Buttons Callback.

Sending the command with no arguments will return whether the Callback is enabled (`1`) or disabled (`0`).

Sending the command with one argument will either enable (`1`) the Callback, or disable (`0`) it.

When the callback is enabled, and any physical controller button is pressed or released, the Callback will send a
specific line of text on the serial port, showing the state of every button.

Specifically, the Callback will send `ControllerButtons([buttons])\r\n>>> `, where `buttons` is every button combined
into a single number, as described in [Buttons](../controller.md#buttons).

## Examples

### Enabling, Reading, Disabling, and Reading the Callback State

Input:
```python
km.controller_buttons(1)   # The Callback is now enabled.
km.controller_buttons()
km.controller_buttons(0)   # The Callback is now disabled.
km.controller_buttons()
```

Output:
```python
km.controller_buttons(1)
>>> km.controller_buttons()
1                  # Since the Callback is enabled, this outputs 1.
>>> km.controller_buttons(0)
>>> km.controller_buttons()
0                  # Since the Callback is disabled, this outputs 0.
>>>
```

### User Input with Callback Enabled

The text in the square brackets is explaining context, and not actually sent on the serial port.

There is no Serial Input here, as the User physically pressing/releasing a button is the cause for the Output.

Output:
```python
[User Presses A]
ControllerButtons(64)    # Bit 6 (A) is set: 1 << 6 = 64.
>>> 
[User Presses LB, Still Holding A]
ControllerButtons(1088)  # Bits 6 (A) and 10 (LB) are set: 64 + 1024 = 1088.
>>> 
[User Releases Both]
ControllerButtons(0)
>>> 
```
