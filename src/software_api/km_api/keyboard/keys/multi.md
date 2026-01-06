# Multiple Key Input

The `km.down`, `km.up`, and `km.press` commands have variants respectively called `km.multidown`, `km.multiup`, and
`km.multipress`. These variants act almost identically to the originals, however they allow as many arguments as the
caller desires, where each extra argument is another key to press/release/click.

These variants allow developers to press, release, or click multiple buttons within the same frame. Keep in mind that
currently developers are expected to add their own delay between presses, and so they should expect the `multi` variants
of these commands to instantly send all inputs within the same frame. This behavior may be changed in the future.

Note that `km.multipress` uses a different random click duration for each key.

## Examples

### Pressing Down A, B, and C Keys All at Once

Input:
```python
km.multidown(4, 5, 6)    # 4 for A, 5 for B, 6 for C
```

Output:
```python
km.multidown(4, 5, 6)
>>>
```

### Clicking Left Shift, H, and I at the Same Time

Input:
```python
km.multipress(225, 11, 12)    # 225 for Left Shift, 11 for H, 12 for I
```

Output:
```python
km.multipress(225, 11, 12)    # 225 for Left Shift, 11 for H, 12 for I
>>>
```

### Pressing and Releasing 1, 2, and 3 for Exactly One Frame

Input:
```python
km.multidown(30, 31, 32)    # 30 for 1, 31 for 2, 32 for 3
km.multiup(30, 31, 32)
```

Output:
```python
km.multidown(30, 31, 32)
>>> km.multiup(30, 31, 32)
>>>
```
