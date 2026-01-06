# Lock

The `km.mask([key], [state])` command is used to read and write the state of the lock/mask on any keyboard key.

By replacing `key` with the number of any key, as defined in the [Keys](../keys.md) section, this command can be used
for all keys.

Calling the command with `state` set to `0` will disable the lock, while `1` will enable it.

Calling the command with no second argument will return the state of the lock on the key.

When the lock is enabled, any physical key presses will not be sent to the Output PC. The Input PC can still read the
key states via the [Get Button State](get_key_state.md) command. The Input PC can also still press/release the key via
either the [Click](click.md) or [Press/Release](set_key_state.md) commands.

This is also known as "input masking", as the physical input is "masked" from the Output PC.

## Examples

### Locking the W Key

Input:
```python
km.mask(26, 1)  # Since the value is 1, the lock is now on.
```

Output:
```python
km.mask(26, 1)
>>>
```

### Locking, Reading, Unlocking, and Reading the Space Key

Input:
```python
km.mask(44, 1)   # The space bar will no longer function on the Output PC.
km.mask(44)
km.mask(44, 0)   # The space bar will now work again on the Output PC.
km.mask(44)
```

Output:
```python
km.mask(44, 1)
>>> km.mask(44)
1                  # Since the lock is enabled, this outputs 1.
>>> km.mask(44, 0)
>>> km.mask(44)
0                  # Since the lock is disabled, this outputs 0.
>>>
```
