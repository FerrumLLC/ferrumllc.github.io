# Set Button State

The `km.[button_name]([state])` command is used to set the state of any of the mouse buttons. By replacing `button_name`
with the name of any button, as defined in the [Buttons](../buttons.md) section, this command can be used for all
buttons. By replacing `state` with either `1` for pressed, or `0` for releasing a press, the command can be used to
force a button down, or release the force press.

Presses are indefinite, meaning until the user engages the
[Hardware Override](/src/hardware_override.md), the button will remain pressed.

## Examples

These examples are raw serial input and output. You are expected to know how to connect to, write to, and read from a
serial port. See [Using a Serial Port](../../../serial_port.md) for more info.

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
# A slight delay of >= 1ms is needed here to ensure the commands dont overlap.
km.side2(0)    # 0 for releasing the button
```

Output:
```python
km.side2(1)
>>> km.side2(0)
>>>
```
