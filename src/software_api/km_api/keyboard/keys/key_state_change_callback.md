# Key State Change Callback

The `km.keys` command is used to enable and disable to the Key State Change Callback.

Sending the command with no arguments will return whether the Callback is enabled (`1`) or disabled (`0`).

Sending the command with one argument will either enable (`1`) the Callback, or disable (`0`) it.

When the callback is enabled, and a keyboard key's state is changed, such as A being pressed, or Left Shift being
released, the Callback will send a specific line of text on the serial port, representing the state of all keys.

Specifically, the Callback will send `Keys([keys])\r\n>>> `, where `keys` is the comma delimited list of decimal key
codes, **sorted by increasing decimal value**. See [Keys](../keys.md) for information on which key codes represent which
keys.

## Examples

### Enabling the Callback

Input:
```python
km.keys(1)  # Since the value is 1, the Callback is now enabled.
```

Output:
```python
km.keys(1)
>>>
```

### Enabling, Reading, Disabling, and Reading the Callback State

Input:
```python
km.keys(1)   # The Callback is now enabled.
km.keys()
km.keys(0)   # The Callback is now disabled.
km.keys()
```

Output:
```python
km.keys(1)
>>> km.keys()
1                  # Since the Callback is enabled, this outputs 1.
>>> km.keys(0)
>>> km.keys()
0                  # Since the Callback is disabled, this outputs 0.
>>>
```

### When the User Presses and Releases Keys, and Callback is Enabled

The text in the square brackets is explaining context, and not actually sent on the serial port.

There is no Input here, as the User physically pressing/releasing a key is the cause for the Output.

Note as stated above that when multiple keys are currently pressed, they are put in the list in increasing decimal
order, not in the order they were pressed.

Output:
```python
[User Has All Keys Released]
[User Presses A]
Keys(4)            # A = 4 is pressed
>>>
[User Releases A]
Keys()             # No keys are pressed
>>>
[User Presses K]
Keys(14)           # K = 14 is pressed
>>>
[User Presses C]
Keys(6, 14)        # C = 6, and K = 14 are pressed
>>>
[User Releases K]
Keys(6)            # C = 6 is pressed
>>>
[User Presses Left Shift]
Keys(6, 225)       # C = 6, and Left Shift = 225 are pressed
>>>
[User Presses Backspace]
Keys(6, 42, 225)   # C = 6, Backspace = 42, and Left Shift = 225 are pressed
>>>
[User Releases C]
Keys(42, 225)      # Backspace = 42, and Left Shift = 225 are pressed
>>>
[User Releases Left Shift]
Keys(42)           # Backspace = 42 is pressed
>>>
[User Releases Backspace]
Keys()             # No keys are pressed
>>>
```
