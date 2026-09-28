# Mouse Proxy API

The Mouse Proxy API allows software to intercept every frame of input from the user's mouse (showing the full 8KHz),
and modify that input (or leave it as is) before it is sent to the `Output PC`. In other words, software sits in the
middle of the mouse and the `Output PC`, acting as a proxy.

The Mouse Proxy API is currently only available over the virtual serial port.

**When the Mouse Proxy API is enabled, all other mouse APIs are disabled/overwritten.**

## Overview

There are four commands in the Mouse Proxy API:

| Command                                                          | Description                                                      |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| [`mouse_proxy.start([window_size])`](./mouse_proxy_api/start.md) | Enables the proxy, buffering `window_size` microframes of input. |
| [`mouse_proxy.fetch()`](./mouse_proxy_api/fetch.md)              | Returns the input buffered since the last `fetch`.               |
| [`mouse_proxy.modify([frames])`](./mouse_proxy_api/modify.md)    | Sends the given frames in place of the fetched input.            |
| [`mouse_proxy.stop()`](./mouse_proxy_api/stop.md)                | Disables the proxy, re-enabling all other mouse APIs.            |

The general flow is to `start` the proxy with a window size, then in a loop, `fetch` the latest input and `modify` it,
and finally `stop` the proxy when you are done.

The window size is set in USB microframes, where 8 microframes is 1ms. It is how long your software has to fetch and
modify the input. Any input that is not modified within the window is sent to the `Output PC` unmodified. So a window
size of `80` (10ms) means your software must call `fetch` and `modify` at least every 10ms to modify all of the input.

## Examples

### Pseudocode

```python
# Request a 10ms = 80 microframe window, so Ferrum will hold 10ms of input that can be modified.
mouse_proxy.start(80)

loop:
    # Request the most recent input. Ferrum will send up to 10ms of raw input over the serial port.
    # This is the input the user made on their mouse.
    # ex: [(1, 2, 0, 0)] represents 1 unit right, 2 units down, no scroll, no buttons pressed.
    frames = mouse_proxy.fetch()

    # Re-send the input received, but modified. This is what the Output PC will see.
    # ex: In this case, mouse movement was inverted.
    mouse_proxy.modify([(-1, -2, 0, 0)])

    # Fetch and must be called modify at least every 10ms (window size).
    # Any slower, and some input will be sent unmodified.
    # So sleeps are for 5ms, giving ample headroom to meet the 10ms max.
    sleep(5ms)

# Now that the program is closing, we stop the proxy (optional, but recommended).
mouse_proxy.stop()
```

### Python

This example inverts all of the user's mouse movement for 5 seconds. Remember to change `COM17` to the serial port
Ferrum is using.

```python
import serial
import time
import ast

with serial.Serial("COM17", 9600, timeout=1) as ser:
    # Disable command echoing, making responses easier to parse.
    ser.write("km.echo(0)\n".encode("utf-8"))

    ser.write("mouse_proxy.start(80)\n".encode("utf-8"))
    ser.read_all()  # Flush

    start = time.time()

    while time.time() - start < 5.00:
        ser.write("mouse_proxy.fetch()\n".encode("utf-8"))
        window = ser.read_all().decode("utf-8").rstrip("\r\n")
        inputs = ast.literal_eval(window)
        if len(inputs) == 0:
            continue

        response_frames = []
        for entry in inputs:
            x = entry[0]
            y = entry[1]
            scroll = entry[2]
            buttons = entry[3]
            response_frames.append(f"({-x},{-y},{scroll},{buttons})")

        response = "[" + ",".join(response_frames) + "]"

        ser.write(f"mouse_proxy.modify({response})\n".encode("utf-8"))

    ser.write("mouse_proxy.stop()\n".encode("utf-8"))
```

## Footnotes

Exposing this API over the serial port isn't the best developer experience, as it requires string parsing on both ends.
It is planned for access to be added to the Net Socket, as well as an SDK that directly interfaces the driver. Feel
free to reach out via [Credits and Contact](../credits_and_contact.md) if you have any suggestions or requests.
