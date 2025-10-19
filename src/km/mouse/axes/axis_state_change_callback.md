# Axis State Change Callback

## Documentation

The `km.axes` command is used to enable and disable the Axis State Change Callback.

Sending the command with no arguments will return whether the Callback is enabled (`1`) or disabled (`0`).

Sending the command with one argument will either enable (`1`) the Callback, or disable (`0`) it.

When the callback is enabled, and input is received on an axis, such as the mouse being moved, or the mouse being
scrolled, the Callback will send a specific line of text on the serial port, showing the received movement.

Specifically, the Callback will send `Axes([x], [y], [scroll])\r\n>>> `, where `x` is the horizontal movement, `y` is
the vertical movement, and `scroll` is the amount scrolled.

Positive `x` is to the right, while negative is to the left. Positive `y` is down, while negative is up. Positive
`scroll` is up, while negative is down.

Typically mice will only send units of 1 (`1` or `-1`) when scrolling, as oppsoed to movement, which normally sends
potentially hundreds of units at once.

## Examples

### Enabling and Disabling the Callback

Input:
```python
km.axes(1)  # Since the value is 1, the Callback is now enabled.
```

Output:
```python
km.axes(1)
>>>
```

### Enabling, Reading, Disabling, and Reading the Callback State

Input:
```python
km.axes(1)   # The Callback is now enabled.
km.axes()
km.axes(0)   # The Callback is now disabled.
km.axes()
```

Output:
```python
km.axes(1)
>>> km.axes()
1                  # Since the Callback is enabled, this outputs 1.
>>> km.axes(0)
>>> km.axes()
0                  # Since the Callback is disabled, this outputs 0.
>>>
```

### User Input with Callback Enabled

The text in the square brackets is explaining context, and not actually sent on the serial port.

There is no Serial Input here, as the User physically pressing/releasing a button is the cause for the Output.

Output:
```python
[User Moves Right]
Axes(7, 0, 0)      # 7 units right, 0 units up, 0 scroll
>>> 
[User Moves Left]
Axes(-8, 0, 0)     # 8 units left, 0 units up, 0 scroll
>>> 
[User Moves Right & Down]
Axes(4, 5, 0)      # 4 units left, 5 units down, 0 scroll
>>> 
[User Scrolls Up]
Axes(0, 0, 1)      # scrolls up
>>> 
[User Scrolls Down]
Axes(0, 0, -1)     # scrolls down
>>> 
```
