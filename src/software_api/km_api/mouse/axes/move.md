# Move

The `km.move([x_amount], [y_amount])` command is used to move the mouse cursor around the screen.

The integer `x_amount` is used to represent the number of units (typically pixels) to move right or left. A positive
value means right, and a negative value means left. Similarly, the integer `y_amount` controls up or down, where
negative is up, and positive is down.

As per [Using a Serial Port](../../../../serial_port.md), the whitespace after the command and before `y_amount` can be any
width. Both arguments must always be included. If you don't want to move in an axis, simply send `0` in its place, as
shown in the examples below.

Units are generic, instead of being pixels. This is because of the processing the operating system can do. For example,
if a user has mouse acceleration on in Windows, or has their cursor sensitivity changed, an input of 10 may result in a
movement different than 10 pixels. Users typically have their device pre-configured to properly make 1 unit = 1 pixel,
which is done by using default Windows settings, and disabling Mouse Acceleration.

## Examples

### Moving Down and Right

Input:
```python
km.move(10, 10)    # 10 units Right, 10 units Down
```

Output:
```python
km.move(10, 10)
>>>
```

### Moving Left

Input:
```python
km.move(-5, 0)    # 5 units Left
```

Output:
```python
km.move(-5, 0)
>>>
```

### Moving Up

Input:
```python
km.move(0, -8)    # 8 units Up
```

Output:
```python
km.move(0, -8)
>>>
```
