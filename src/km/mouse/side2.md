# The km.side2 command

The `km.side2` command is used to read and write the state of the front side mouse button.

To read the state of the button, simply send `km.side2()`, and wait for it to respond.

To write the state of the button, and overwrite the user input, send `km.side2(1)` to press, or `km.side2(0)` to release
the press. Presses are indefinite, meaning until the user engages the [Hardware Override](./../../hardware_override.md),
the button will remain pressed.

## Examples

These examples are raw serial input and output. You are expected to know how to connect to, write to, and read from a
serial port. See [Using a Serial Port](./../../serial_port.md) for more info.

### Reading the Front Side Button's State

Input:
```python
km.side2()
```

Output:
```py
km.side2()   # The command is echoed back.
1            # The result, either 1 for Front Side being pressed, or 0 for it being released.
>>>          # The "input prompt" for the next command. There is a single space after the three arrows, and no proceeding newline.
```

### Pressing the Front Side Button

Input:
```python
km.side2(1)
```

Output:
```py
km.side2(1)   # The command is echoed back.
>>>          # The "input prompt" for the next command. There is a single space after the three arrows, and no proceeding newline.
```

### Releasing a Front Side Button Press

Input:
```python
km.side2(0)
```

Output:
```py
km.side2(0)   # The command is echoed back.
>>>          # The "input prompt" for the next command. There is a single space after the three arrows, and no proceeding newline.
```
