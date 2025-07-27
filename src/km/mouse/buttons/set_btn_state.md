# Set Button State

The `km.[button_name]([state])` command is used to set the state of any of the mouse buttons.

By replacing `button_name` with the name of any button, as defined in the [Buttons](../buttons.md) section, this command
can be used for all buttons.

By replacing `state` with either `1` for pressed, or `0` for releasing a press, the command can be used to force a
button down, or release the force press.

Releases last for a uniformly random time period between 125ms and 175ms. After this time period, the button returns to
the physical state.

Presses are indefinite, meaning until the user engages the [Hardware Override](../../../hardware_override.md), or a
release or click command is sent, the button will remain pressed.

Note: The click command will override any presses or releases in place.

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
# A slight delay of is recommended here so the click appears realistic.
km.side2(0)    # 0 for releasing the button
```

Output:
```python
km.side2(1)
>>> km.side2(0)
>>>
```
