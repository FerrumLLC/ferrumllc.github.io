# Get Key State

The `km.isdown([key])` command is used to read the state of any of the keyboard keys.

By replacing `key` with the number or key string of any key, as defined in the [Keys](../keys.md) section, this
command can be used for all keys.

The command returns `1` if the key is pressed, or `0` if it is released. If no key is given, or the key is not
recognized, `0` is returned.

## Examples

### Reading the A Key's State

Input:
```python
km.isdown(4)
```

Output:
```python
km.isdown(4)
1            # The A Key in this case was pressed (1).
>>>
```

### Reading the Left Control Key's State

Input:
```python
km.isdown(224)
```

Output:
```python
km.isdown(224)
0            # The Left Control Key in this case was released (0).
>>>
```
