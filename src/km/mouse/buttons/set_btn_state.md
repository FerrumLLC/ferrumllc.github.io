# Set Button State

The `km.[button_name]([state])` command is used to set the state of any of the mouse buttons.

By replacing `button_name` with the name of any button, as defined in the [Buttons](../buttons.md) section, this command
can be used for all buttons.

By replacing `state` with either `1` for pressed, or `0` for releasing a press, the command can be used to force a
button down, or release the force press.

Currently this function does not force release the mouse button when a release command is sent. Instead it releases the
press request, returning the device to its original state. This is as defined in the
[Hardware Override](../../../hardware_override.md) state machine, and is likely to change in the future.

Presses are indefinite, meaning until the user engages the [Hardware Override](../../../hardware_override.md), the button
will remain pressed.

## Examples

### Pressing the Left Button

Input:
```python
km.left(1)    # 1 for pressing the button
```

Output:
```python
km.left(1)
>>>
```

### Pressing and Releasing the Front Side Button

Input:
```python
km.side2(1)    # 1 for pressing the button
# A slight delay of >= 1ms is needed here to ensure the commands don't overlap.
km.side2(0)    # 0 for releasing the button
```

Output:
```python
km.side2(1)
>>> km.side2(0)
>>>
```
