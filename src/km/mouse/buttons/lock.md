# Lock

The `km.lock_[button_lock_name]` command is used to read and write the state of the lock on any mouse button.

By replacing `button_lock_name` with one of the button lock names defined below, it can be made to work with any button.

Calling the command with no arguments (by using `()`) will return the state of the lock on the button.

Calling the command with one argument will set the lock's state. If the argument is `1` it will enable it. If it is `0`,
it will disable it.

When the lock is enabled, any physical button presses will not be sent to the Output PC. The Input PC can still read the
button states via either the [Get Button State](get_btn_state.md) or [Button State Event](btn_state_event.md) commands.
The Input PC can also still press/release the button via either the [Click](click.md) or
[Press/Release](set_btn_state.md) commands.

This is also known as "input masking", as the physical input is "masked" from the Output PC.

| Button Lock Name | Button Description      |
| ---------------- | ----------------------- |
| ml               | the left button         |
| mr               | the right button        |
| mm               | the scroll wheel button |
| ms1              | the rear side button    |
| ms2              | the front side button   |

## Examples

### Locking the Left Mouse Button

Input:
```python
km.lock_ml(1)  # Since the value is 1, the lock is now on.
```

Output:
```python
km.lock_ml(1)
>>>
```

### Locking, Reading, Unlocking, and Reading the Front Side Mouse Button

Input:
```python
km.lock_ms2(1)   # The side button will no longer function on the Output PC.
km.lock_ms2()
km.lock_ms2(0)   # The side button will now work again on the Output PC.
km.lock_ms2()
```

Output:
```python
km.lock_ms2(1)
>>> km.lock_ms2()
1                  # Since the lock is enabled, this outputs 1.
>>> km.lock_ms2(0)
>>> km.lock_ms2()
0                  # Since the lock is disabled, this outputs 0.
>>>
```
