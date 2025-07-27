# Set Key State

The `km.down([key])` and `km.up([key])` commands are used to set the state of any of the keyboard keys.

By replacing `key` with the number of any key, as defined in the [Keys](../keys.md) section, this command can be used
for all keys.

As their names suggest, `down` makes the key become pressed, while `up` makes it force release. For compatibility
reasons, these names are slightly confusing, and so be careful to not mistake `down` for the `km.press` command, as
`km.press` actually performs a click.

Releases last for a uniformly random time period between 125ms and 175ms. After this time period, the button returns to
the physical state.

Presses are indefinite, meaning until the user engages the [Hardware Override](../../../hardware_override.md), or a
release or click command is sent, the button will remain pressed.

Note: The click command will override any presses or releases in place.

## Examples

### Pressing the A Key

Input:
```python
km.down(4)    # 4 for A
```

Output:
```python
km.down(4)
>>>
```

### Pressing and Releasing the Left Shift Key

Input:
```python
km.down(225)    # 225 for Left Shift
# A slight delay of is recommended here so the click appears realistic.
km.up(225)
```

Output:
```python
km.down(225)
>>> km.up(225)
>>>
```
