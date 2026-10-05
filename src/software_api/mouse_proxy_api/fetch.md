# Fetch

The `mouse_proxy.fetch()` command returns all buffered input that has not yet been modified, up to the size of the
window set by [Start](./start.md).

For example, with a `window_size` of `80`, if `fetch` is called it may return 80 frames (10ms). If it is then followed
by a [Modify](./modify.md), and `fetch` is called again 1ms later, it will only return 8 frames (1ms).

Only [Modify](./modify.md) removes frames from the buffer. Calling `fetch` twice without a `modify` in between returns
the same frames again (along with any new ones), and only the most recent `fetch` can then be modified.

The frames are returned as a list, where each frame is in the format `(x, y, scroll, buttons)`:

- `x` - The number of units moved right (positive) or left (negative), as in [Move](../km_api/mouse/axes/move.md).
- `y` - The number of units moved down (positive) or up (negative), as in [Move](../km_api/mouse/axes/move.md).
- `scroll` - The amount scrolled, as in [Scroll](../km_api/mouse/axes/scroll.md).
- `buttons` - The bitmap of all button states, as described in
  [Button State Change Callback](../km_api/mouse/buttons/btn_state_change_callback.md).

The list is formatted with a space after the opening bracket and before the closing bracket, such as
`[ (1, 2, 0, 0) ]`. If there is no new input, or the proxy has not been started, an empty list (`[  ]`) is returned.

Each call to `fetch` that returns frames should be followed by a call to [Modify](./modify.md).

## Examples

### Fetching Mouse Movement

Input:
```python
mouse_proxy.fetch()
```

Output:
```python
mouse_proxy.fetch()
[ (1, 2, 0, 0), (0, 1, 0, 0) ]    # 2 frames of input. The user moved right and down.
>>>
```

### Fetching a Left Click

Input:
```python
mouse_proxy.fetch()
```

Output:
```python
mouse_proxy.fetch()
[ (0, 0, 0, 1), (0, 0, 0, 0) ]    # Left was pressed (bitmap 0b00001), then released.
>>>
```

### Fetching with No New Input

Input:
```python
mouse_proxy.fetch()
```

Output:
```python
mouse_proxy.fetch()
[  ]               # The user has not used their mouse since the last fetch.
>>>
```
