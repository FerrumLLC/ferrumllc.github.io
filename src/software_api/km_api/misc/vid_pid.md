# VID/PID

The `device.VID()` and `device.PID()` commands return the USB Vendor ID and Product ID of the peripheral connected to
Ferrum. They exist for compatibility with software written for the KMBox B Pro.

The response is formatted as `VID=[vid]` or `PID=[pid]`, where the value is a 4 digit lowercase hexadecimal number.

The value is taken from the first connected peripheral, which is not necessarily the one designated as the Mouse. If no
peripheral is connected, the default values of `046d` and `c53f` are returned.

Calling either command with arguments does nothing, and returns no response.

## Examples

### Reading the VID

Input:
```python
device.VID()
```

Output:
```python
device.VID()
VID=046d
>>>
```

### Reading the PID

Input:
```python
device.PID()
```

Output:
```python
device.PID()
PID=c53f
>>>
```
