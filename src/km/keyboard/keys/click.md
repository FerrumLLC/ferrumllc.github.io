# Click

The `km.press([key])` command is used to make the keyboard press and release a key over some time. Rather unintuitively,
for compatibility's sake, the command is called `km.press`, despite being responsible for a full click of a key.

By replacing `key` with the number of any key, as defined in the [Keys](../keys.md) section, this command can be used
for all keys.

Currently this command presses, delays, releases, delays, and then returns to the hardware state.

There is a delay for how long the press and release are held for. The press and release durations are uniformly random
values between 75ms and 125ms, and 125ms and 175ms respectively. For fine control over the duration of the delays, I
strongly recommend developers use the commands defined in [Set Key State](set_key_state.md).

Clicks can be overridden by the user via the [Hardware Override](../../../hardware_override.md).

If the key is physically pressed when the click starts, it will be force released after the press delay, and then the
release will be removed after the release delay, putting it back in the hardware state (pressed if it's still
physically pressed, or released if the user released the key at some point).

## Examples

### Clicking the Z Key

Input:
```python
km.press(29)  # 29 for Z
```

Output:
```python
km.press(29)
>>>
```

### Clicking the Right Control Key

Input:
```python
km.press(228)  # 228 for Right Control
```

Output:
```python
km.press(228)
>>>
```
