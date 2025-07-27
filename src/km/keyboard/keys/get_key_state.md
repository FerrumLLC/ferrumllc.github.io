# Get Key State

The `km.isdown([key])` command is used to read the state of any of the keyboard keys.

By replacing `key` with the number of any key, as defined in the [Keys](../keys.md) section, this command can be used
for all keys.

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
