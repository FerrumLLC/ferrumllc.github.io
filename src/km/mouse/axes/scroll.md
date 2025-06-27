# Scroll

The `km.wheel([amount])` command is used to scroll the mouse wheel a number of times up or down. When the integer
`amount` is positive, the scroll is up. When it is negative, the scroll is down. The number doesn't represent pixels,
but rather the number of scrolls to perform. One click in a physical scroll wheel is equivalent to one scroll up or
down.

## Security

To prevent sending suspicious output, please do not use values other than -1 or +1 unless you know what you are doing.
While I strongly doubt any games actually check this, I have never seen a mouse send any value other than +1 or -1 as
the scroll amount, even mice with unlocking scroll wheels. Therefore, sending any larger values than this could be seen
as a sign that the input is emulated and not legitimate.

## Examples

### Scrolling Up

Input:
```python
km.wheel(1)    # 1 for up
```

Output:
```python
km.wheel(1)
>>>
```

### Scrolling Down

Input:
```python
km.wheel(-1)   # -1 for down
```

Output:
```python
km.wheel(-1)
>>>
```
