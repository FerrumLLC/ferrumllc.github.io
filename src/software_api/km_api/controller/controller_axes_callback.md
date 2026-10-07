# Controller Axes Callback

## Documentation

The `km.controller_axes` command is used to enable and disable the Controller Axes Callback.

Sending the command with no arguments will return whether the Callback is enabled (`1`) or disabled (`0`).

Sending the command with one argument will either enable (`1`) the Callback, or disable (`0`) it.

When the callback is enabled, and any physical controller axis changes, such as a stick being moved or a trigger being
pressed, the Callback will send a specific line of text on the serial port, showing the position of every axis.

Specifically, the Callback will send `ControllerAxes([lt], [rt], [lx], [ly], [rx], [ry])\r\n>>> `, using the ranges
described in [Axes](../controller.md#axes).

Unlike the mouse's [Axis State Change Callback](../mouse/axes/axis_state_change_callback.md), which uses relative
movement, controller axes are absolute positions.

## Examples

### Enabling, Reading, Disabling, and Reading the Callback State

Input:
```python
km.controller_axes(1)   # The Callback is now enabled.
km.controller_axes()
km.controller_axes(0)   # The Callback is now disabled.
km.controller_axes()
```

Output:
```python
km.controller_axes(1)
>>> km.controller_axes()
1                  # Since the Callback is enabled, this outputs 1.
>>> km.controller_axes(0)
>>> km.controller_axes()
0                  # Since the Callback is disabled, this outputs 0.
>>>
```

### User Input with Callback Enabled

The text in the square brackets is explaining context, and not actually sent on the serial port.

There is no Serial Input here, as the User physically moving the controller's sticks and triggers is the cause for the
Output.

Output:
```python
[User Pushes the Left Stick Fully Right]
ControllerAxes(0, 0, 32767, 0, 0, 0)
>>> 
[User Half Presses the Right Trigger]
ControllerAxes(0, 32768, 32767, 0, 0, 0)
>>> 
[User Releases Both]
ControllerAxes(0, 0, 0, 0, 0, 0)
>>> 
```
