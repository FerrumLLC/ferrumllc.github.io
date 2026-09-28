# Start

The `mouse_proxy.start([window_size])` command enables the Mouse Proxy.

The integer `window_size` is the number of frames Ferrum will buffer, in units of USB microframes. A USB microframe is
125 microseconds, meaning there are 8 of them every millisecond (8KHz). So a `window_size` of `80` means Ferrum holds 80
microframes, which is `80 * 125 / 1000 = 10ms` of input.

The window is the time available to modify the input. Any input that is not fetched and modified within the window will
be sent to the `Output PC` unmodified. A larger window gives your software more time to respond, at the cost of more
delay between the user moving their mouse, and the `Output PC` seeing it.

Once the proxy is started, all other mouse APIs are disabled until it is [stopped](./stop.md), or the Ferrum acting as
a mouse is reconnected.

## Examples

### Starting the Proxy with a 10ms Window

Input:
```python
mouse_proxy.start(80)    # 80 microframes = 10ms
```

Output:
```python
mouse_proxy.start(80)
>>>
```

### Starting the Proxy with a 2ms Window

Input:
```python
mouse_proxy.start(16)    # 16 microframes = 2ms
```

Output:
```python
mouse_proxy.start(16)
>>>
```
