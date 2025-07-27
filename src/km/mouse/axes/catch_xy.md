# Catch XY

The `km.catch_xy([duration])` command is used to find the amount of x/y input over the last `duration` of time.

The parameter `duration` is a value in milliseconds up to 1000, declaring how far back in time to sum the x/y input.

The command returns the summed input in the following format: `(x, y)`.

## Examples

### Summing the Last Second of Input

Input:
```python
km.catch_xy(1000)  # 1000ms = 1 second = max duration
```

Output:
```python
km.catch_xy(1000)
(500, -500)        # The mouse moved 500 to the right, and 500 up in the last second.
>>>
```

### Summing the Last 10 MilliSeconds of Input

Input:
```python
km.catch_xy(10)    # 10ms
```

Output:
```python
km.catch_xy(10)
(-3, 10)           # The mouse moved 3 left, and 10 up in the last 10ms.
>>>
```
