# Lock

The `km.lock_[axis_lock_name]` command is used to read and write the state of the lock on any axis.

By replacing `axis_lock_name` with one of the axis lock names defined below, it can be made to work with any axis.

Calling the command with no arguments (by using `()`) will return the state of the lock on the axis.

Calling the command with one argument will set the lock's state. If the argument is `1` it will enable it. If it is `0`,
it will disable it.

When the lock is enabled, any physical movement on the axes will not be sent to the Output PC. The Input PC can still
send movement to the Output PC by using the [Move](./move.md) command, or scroll by using the [Scroll](./scroll.md)
command.

This is also known as "input masking", as the physical input is "masked" from the Output PC.

Each axis can also have just one of its directions locked. See [Directional Locks](#directional-locks).

<center><b>Axis Locks</b></center>

| Axis Lock Name | Axis Direction |
| -------------- | -------------- |
| mx             | left and right |
| my             | up and down    |
| mw             | scroll wheel   |

## Directional Locks

The `km.lock_[axis_lock_name]+` and `km.lock_[axis_lock_name]-` commands work the same way as `km.lock_[axis_lock_name]`,
but only lock or unlock one direction of the axis. `+` refers to the positive direction, and `-` to the negative
direction, as defined below.

<center><b>Axis Directions</b></center>

| Axis Lock Name | Positive (`+`) | Negative (`-`) |
| -------------- | -------------- | -------------- |
| mx             | right          | left           |
| my             | down           | up             |
| mw             | scroll up      | scroll down    |

When a direction is locked, physical movement in that direction is not sent to the Output PC, while movement in the
other direction is sent like normal.

Each direction's lock is independent of the other:

- Locking both `+` and `-` locks the whole axis, the same as `km.lock_[axis_lock_name](1)`.
- Unlocking one direction of a fully locked axis leaves only the other direction locked.
- `km.lock_[axis_lock_name](0)` unlocks both directions.

Calling a directional command with no arguments returns whether that direction is locked. Calling
`km.lock_[axis_lock_name]()` returns `1` if either direction is locked.

## Examples

### Locking the Scroll Wheel

Input:
```python
km.lock_mw(1)  # Physical scrolling will no longer be sent to the Output PC.
```

Output:
```python
km.lock_mw(1)
>>>
```

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

### Locking Only Upward Movement

Input:
```python
km.lock_my-(1)  # Upward movement is no longer sent, while downward movement still is.
```

Output:
```python
km.lock_my-(1)
>>>
```

### Combining and Removing Directional Locks on the X Axis

Input:
```python
km.lock_mx+(1)  # Rightward movement is locked.
km.lock_mx-(1)  # Leftward movement is also locked, so the whole axis is now locked.
km.lock_mx()
km.lock_mx+(0)  # Rightward movement is unlocked, leaving only leftward movement locked.
km.lock_mx+()
km.lock_mx-()
```

Output:
```python
km.lock_mx+(1)
>>> km.lock_mx-(1)
>>> km.lock_mx()
1                  # Both directions are locked.
>>> km.lock_mx+(0)
>>> km.lock_mx+()
0                  # The positive direction is now unlocked.
>>> km.lock_mx-()
1                  # The negative direction is still locked.
>>>
```
