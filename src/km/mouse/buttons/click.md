# Click

The `km.click([button])` command is used to make the mouse press and release a button over some time.

By replacing `button` with the number representing a button as shown below, this command can be used for all buttons.

Currently this command presses, delays, releases, delays, and then returns to the hardware state.

There is a delay for how long the press and release are held for. The press and release durations are uniformly random
values between 75ms and 125ms, and 125ms and 175ms respectively. For fine control over the duration of the delays, I
strongly recommend developers use the commands defined in [Set Button State](set_btn_state.md).

Clicks can be overridden by the user via the [Hardware Override](../../../hardware_override.md).

If the button is physically pressed when the click starts, it will be force released after the press delay, and then
the release will be removed after the release delay, putting it back in the hardware state (pressed if it's still
physically pressed, or released if the user released the button at some point).

<center><b>Buttons</b></center>

| Button Number | Button Description      |
| ------------- | ----------------------- |
| 0             | the left button         |
| 1             | the right button        |
| 2             | the scroll wheel button |
| 3             | the rear side button    |
| 4             | the front side button   |

## Examples

### Clicking the Left Button

Input:
```python
km.click(0)  # 0 for Left
```

Output:
```python
km.click(0)
>>>
```

### Clicking the Front Side Button

Input:
```python
km.click(4)  # 4 for Front Side
```

Output:
```python
km.click(4)
>>>
```
