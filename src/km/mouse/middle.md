# The km.middle command

The `km.middle` command is used to read and write the state of the middle mouse button (scroll wheel button).

To read the state of the button, simply send `km.middle()`, and wait for it to respond.

To write the state of the button, and overwrite the user input, send `km.middle(1)` to press, or `km.middle(0)` to
release the press. Presses are indefinite, meaning until the user engages the
[Hardware Override](./../../hardware_override.md), the button will remain pressed.

## Examples

These examples are raw serial input and output. You are expected to know how to connect to, write to, and read from a
serial port. See [Using a Serial Port](./../../serial_port.md) for more info.

### Reading the Middle Button's State

Input:
```python
km.middle()
```

Output:
```py
km.middle()  # The command is echoed back.
1            # The result, either 1 for Middle being pressed, or 0 for it being released.
>>>          # The "input prompt" for the next command. There is a single space afterthe three arrows, and no proceeding newline.
```

### Pressing the Middle Button

Input:
```python
km.middle(1)
```

Output:
```py
km.middle(1)   # The command is echoed back.
>>>          # The "input prompt" for the next command. There is a single space afterthe three arrows, and no proceeding newline.
```

### Releasing a Middle Button Press

Input:
```python
km.middle(0)
```

Output:
```py
km.middle(0)   # The command is echoed back.
>>>          # The "input prompt" for the next command. There is a single space afterthe three arrows, and no proceeding newline.
```
