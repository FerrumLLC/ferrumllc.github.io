# Controller State

The `km.controller(...)` command is used to read the controller's state, and to override any of its axes and buttons.

## Reading the State

Calling the command with no arguments (by using `()`) will return the controller's most recent physical state, as
`(buttons, lt, rt, lx, ly, rx, ry)`.

The axes are in the ranges described in [Axes](../controller.md#axes), and `buttons` is every button combined into a
single number, as described in [Buttons](../controller.md#buttons).

## Overriding Axes and Buttons

Calling the command with keyword arguments (`name=value`) will override the named axes and buttons, using the names
defined in [Axes](../controller.md#axes) and [Buttons](../controller.md#buttons).

- An axis's value is its new position, such as `lx=-32768` (left stick fully left) or `rt=65535` (right trigger fully
  pressed).
- A button's value is `1` to press it, or `0` to release it.
- A value of `None` ends the override, returning the axis or button to its physical state.
- Any axis or button not named is left unchanged.

While overridden, the physical input of that axis or button is not sent to the Output PC, and the overridden value is
sent instead.

### Hold Duration

Each override only lasts for a short duration, after which the axis or button returns to its physical state. The
duration defaults to `20` milliseconds, and can be set from `0` to `255` milliseconds with the `hold` keyword argument,
such as `hold=100`. To hold an override longer, send the command again before it ends.

Each axis and button has its own duration, so sending a command only extends the overrides it names.

This means that if the Input PC stops sending commands, such as if its software crashes, the controller returns to
its physical state, instead of being stuck.

### Invalid Arguments

If any argument is invalid, such as an unknown name, a value out of range, or an argument without a `=`, the entire
command is ignored, and nothing is overridden.

## Examples

### Reading the State

Input:
```python
km.controller()
```

Output:
```python
km.controller()
(0, 0, 0, 0, 0, 0, 0)  # No buttons pressed, released triggers, and centered sticks.
>>>
```

### Holding the Right Stick Up

Input:
```python
km.controller(ry=32767)  # The right stick is held fully up for 20 milliseconds.
```

Output:
```python
km.controller(ry=32767)
>>>
```

### Pressing A for 100 Milliseconds

Input:
```python
km.controller(a=1, hold=100)  # Also works as km.controller(cross=1, hold=100).
```

Output:
```python
km.controller(a=1, hold=100)
>>>
```

### Overriding Multiple Axes and Buttons at Once

Input:
```python
km.controller(lx=-16000, rt=65535, rb=1, x=0)  # Left stick halfway left, right trigger fully pressed, RB pressed,
                                               # and X held released.
```

Output:
```python
km.controller(lx=-16000, rt=65535, rb=1, x=0)
>>>
```

### Ending an Override Early

Input:
```python
km.controller(a=1, hold=255)
km.controller(a=None)  # A returns to its physical state immediately.
```

Output:
```python
km.controller(a=1, hold=255)
>>> km.controller(a=None)
>>>
```
