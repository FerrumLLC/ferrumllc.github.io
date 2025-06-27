# Lock

The `km.lock_[axis_lock_name]` command is used to read and write the state of the lock on any axis.

By replacing `axis_lock_name` with one of the axis lock names defined below, it can be made to work with any axis.

Calling the command with no arguments (by using `()`) will return the state of the lock on the axis.

Calling the command with one argument will set the lock's state. If the argument is `1` it will enable it. If it is `0`,
it will disable it.

When the lock is enabled, any physical movement on the axes will not be sent to the Output PC. The Input PC can still
send movement to the Output PC by using the [Move](move.md) command.

This is also known as "input masking", as the physical input is "masked" from the Ouput PC.

| Axis Lock Name | Axis Direction |
| -------------- | -------------- |
| mx             | left and right |
| my             | up and down    |

## Examples

### Locking the X Axis

Input:
```python
km.lock_mx(1)  # Since the value is 1, the lock is now on.
```

Output:
```python
km.lock_mx(1)
>>>
```

### Locking, Reading, Unlocking, and Reading the Y Axis

Input:
```python
km.lock_my(1)   # Any up and down input will no longer be sent to the Output PC.
km.lock_my()
km.lock_my(0)   # Up and down input will now be sent again like normal.
km.lock_my()
```

Output:
```python
km.lock_my(1)
>>> km.lock_my()
1                  # Since the lock is enabled, this outputs 1.
>>> km.lock_my(0)
>>> km.lock_my()
0                  # Since the lock is disabled, this outputs 0.
>>>
```
