# Move

The `km.move([x_amount], [y_amount])` command is used to move the mouse cursor around the screen. The integer `x_amount`
is used to represent the number of pixels to move right or left. A positive value means right, and a negative value
means left. Similarly, the integer `y_amount` controls up or down, where negative is up, and positive is down.

As per [Using a Serial Port](../../../serial_port.md), the whitespace after the command and before `y_amount` can be any
width. Both arguments must always be included. If you dont want to move in an axis, simply send `0` in its place, as
shown in the examples below.

## Examples

### Moving Down and Right

Input:
```python
km.move(10, 10)    # 10 pixels Right, 10 pixels Down
```

Output:
```python
km.move(10, 10)
>>>
```

### Moving Left

Input:
```python
km.move(-5, 0)    # 5 pixels Left
```

Output:
```python
km.move(-5, 0)
>>>
```

### Moving Up

Input:
```python
km.move(0, -8)    # 8 pixels Up
```

Output:
```python
km.move(0, -8)
>>>
```
