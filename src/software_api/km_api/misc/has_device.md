# Device Presence

The `km.has_mouse()`, `km.has_keyboard()`, and `km.has_controller()` commands are used to check whether a device is
currently connected and designated as a Mouse, Keyboard, or Controller respectively.

Each command returns `1` if such a device is connected, or `0` if not. Any arguments passed are ignored.

This is useful for checking that the user has set up Ferrum correctly before sending commands, as commands sent to a
device type that isn't connected are silently discarded.

## Examples

### Checking for a Mouse

Input:
```python
km.has_mouse()
```

Output:
```python
km.has_mouse()
1            # A device designated as a Mouse is connected.
>>>
```

### Checking for a Keyboard

Input:
```python
km.has_keyboard()
```

Output:
```python
km.has_keyboard()
0            # No device designated as a Keyboard is connected.
>>>
```
