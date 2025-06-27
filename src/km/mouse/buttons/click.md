# Click

The `km.click([button])` command is used to make the mouse press and release a button over some time. By replacing
`button` with the number representing a button as shown below, this command can be used for all buttons. Currently it
will press, and then after the duration of the click, release the press, returning to the hardware state.

There is a delay for how long the button is held for. This value is a uniformly random duration between 75ms and 125ms.

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
