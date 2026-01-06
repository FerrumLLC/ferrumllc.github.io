# Baud

<div style="background-color: rgb(61, 44, 0); border: 1px solid rgb(251, 212, 106); color: rgb(251, 212, 106); padding: 15px; border-radius: 5px; margin-bottom: 15px;">
    This API has been deprecated in favor of the <a href="../../software_api.md" style="color: #3498db; text-decoration: underline;">Software API</a>.
</div>

The `km.baud([baud_rate])` command in the Legacy API lets developers adjust Ferrum's hardware baud rate directly. This
command is not available in the [Software API](../../software_api.md) due to it using a Virtual API, which means
commands are optimized before being sent to the Ferrum hardware, and always communicated at 3,000,000 baud.

Developers are strongly recommended to not exceed 3Mbd (3000000 baud) with the Ferrum hardware. Data transfer may not be
stable at these speeds, leading to command corruption. Furthermore, 3Mbd is more than fast enough for anything, taking
just 0.050ms to send `km.move(100, 100)\r\n`. The default speed is 115200 baud, as explained in
[Legacy API](../../legacy_api.md).

This function has no read feature. In other words, `km.baud()` does nothing, where other commands such as `km.left()`
would have returned the state of the button. If you're able to communicate with the device, then the speed is your
current speed.

## Examples

### Setting the Baud Rate to Max

Input:
```python
km.baud(3000000)
```

Output: (None)
```python
```

### Setting the Baud Rate to Default

Input:
```python
km.baud(115200)
```

Output: (None)
```python
```
