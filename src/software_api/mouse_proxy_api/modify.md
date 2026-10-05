# Modify

The `mouse_proxy.modify([frames])` command tells Ferrum what to send to the `Output PC` in place of the frames that were
returned by [Fetch](./fetch.md).

Each call to `fetch` should be followed by exactly one call to `modify`, passing in the exact same number of frames as
were returned, in the same `(x, y, scroll, buttons)` format. The values in the frames can be changed however desired.
To send a frame unmodified, simply pass it back as it was received.

If `fetch` returned an empty list, there is nothing to modify, and `modify` does not need to be called.

Any fetched input that is not modified within the window set by [Start](./start.md) will be sent to the `Output PC`
unmodified. If some of the fetched frames have already been sent by the time `modify` is received, those frames are
skipped, and only the remaining frames are modified.

The entire `modify` is ignored, with no error returned, if:

- The number of frames doesn't match the number returned by the last `fetch`.
- All of the fetched frames have already been sent.
- There was no `fetch` since the last `modify`.
- The proxy is not started.

Values outside the valid ranges are clamped: `x` and `y` to `-32768` to `32767`, and `scroll` to `-128` to `127`.
Only the lowest 5 bits of `buttons` are used.

## Examples

### Inverting Mouse Movement

Input:
```python
mouse_proxy.fetch()
mouse_proxy.modify([(-1, -2, 0, 0), (0, -1, 0, 0)])
```

Output:
```python
mouse_proxy.fetch()
[ (1, 2, 0, 0), (0, 1, 0, 0) ]    # The user moved right and down.
>>> mouse_proxy.modify([(-1, -2, 0, 0), (0, -1, 0, 0)])    # The Output PC sees left and up.
>>>
```

### Blocking Left Click

Input:
```python
mouse_proxy.fetch()
mouse_proxy.modify([(3, 0, 0, 0)])
```

Output:
```python
mouse_proxy.fetch()
[ (3, 0, 0, 1) ]   # The user moved right while holding Left (bitmap 0b00001).
>>> mouse_proxy.modify([(3, 0, 0, 0)])    # Movement is kept, but Left is released.
>>>
```

### Passing Input Through Unmodified

Input:
```python
mouse_proxy.fetch()
mouse_proxy.modify([(5, -2, 1, 0)])
```

Output:
```python
mouse_proxy.fetch()
[ (5, -2, 1, 0) ]
>>> mouse_proxy.modify([(5, -2, 1, 0)])    # The Output PC sees exactly what the user did.
>>>
```
