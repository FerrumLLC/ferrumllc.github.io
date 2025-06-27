# Get Button State

The `km.[button_name]()` command is used to read the state of any of the mouse buttons. By replacing `button_name` with
the name of any button, as defined in the [Buttons](../buttons.md) section, this command can be used for all buttons.

## Examples

These examples are raw serial input and output. You are expected to know how to connect to, write to, and read from a
serial port. See [Using a Serial Port](../../../serial_port.md) for more info.

### Reading the Left Button's State

Input:
```python
km.left()
```

Output:
```python
km.left()
1            # The Left Button in this case was pressed (1).
>>>
```

### Reading the Front Side Button's State

Input:
```python
km.side2()
```

Output:
```python
km.side2()
0            # The Front Side Button in this case was released (0).
>>>
```
