# Button State Change Callback

## Prefix

The syntax for this function was designed by ihack, the developer of MAKCU. It is implemented here for compatibility's
sake. However, it is a rather complex function, and may be difficult to grasp at first. If you want something simple
instead, its functionality can be substituted by using the [Get Button State](get_btn_state.md) command.

As an aside, for those that do read and implement usage of this command, be sure your string parsing of the output of
the Callback accounts for the `\0` character. This is known as the null character, and is typically used for marking the
end of a string. As such, your parsing may mistakenly cut off early, thinking that it is the end of the string.

## Documentation

The `km.buttons` command is used to read from and write to the Button State Change Callback.

Sending the command with no arguments will return whether the Callback is enabled (`1`) or disabled (`0`).

Sending the command with one argument will either enable (`1`) the Callback, or disable (`0`) it.

When the callback is enabled, and a button's state is changed, such as Left being pressed, or the Front Side button
being released, the Callback will send a specific line of text on the serial port, representing the state of all keys.

Specifically, the Callback will send `km.[button_states]\r\n>>> `, where `button_states` is the raw bitmap of all button
states.

If you're not familiar with how binary works, now might be a good time to learn.

Essentially we make a number to represent all buttons. This number is made up of 5 bits, where each bit represents a
button, with the lowest being Left, and the highest being the Front Side Button.

When no buttons are pressed, the binary number is `0b00000`, which is the decimal number `0`, and the character `'\0'`
(Google/ChatGPT "escape sequence syntax" and what those characters mean if you don't understand).

When left is pressed: binary = `0b00001`, decimal = `1`, character = `'\1'`.

When left and the rear side button are pressed: binary = `0b01001`, decimal = `9`, character = `'\9'`.

Then this character is sent in `button_state`'s place. So as a whole if left and rear side are pressed, the character
is `'\9'`, and the string written to the serial port will be `"km.\9\r\n>>> "`.

## Examples

### Enabling the Callback

Input:
```python
km.buttons(1)  # Since the value is 1, the Callback is now enabled.
```

Output:
```python
km.buttons(1)
>>>
```

### Enabling, Reading, Disabling, and Reading the Callback State

Input:
```python
km.buttons(1)   # The Callback is now enabled.
km.buttons()
km.buttons(0)   # The Callback is now disabled.
km.buttons()
```

Output:
```python
km.buttons(1)
>>> km.buttons()
1                  # Since the Callback is enabled, this outputs 1.
>>> km.buttons(0)
>>> km.buttons()
0                  # Since the Callback is disabled, this outputs 0.
>>>
```

### When the User Presses and Releases Buttons, and Callback is Enabled

This example has the raw output of the serial console. The backslash prior to characters is not literally sent. If you
don't know what the backslash means in this context, use Google/ChatGPT to learn.

There are no implicit [Line Terminators](../../../serial_port/line_terminator.md) here.

The text in the square brackets is explaining context, and not actually sent on the serial port.

There is no Input here, as the User physically pressing a button is the cause for the Output.

Output:
```python
[User Has All Keys Released]
[User Presses Left]
km.\1\r\n          # Binary 0b00001, Left is Pressed
>>>
[User Releases Left]
km.\0\r\n          # Binary 0b00000, Nothing is Pressed
>>>
[User Presses Right]
km.\2\r\n          # Binary 0b00010, Right is Pressed
>>>
[User Presses Left]
km.\3\r\n          # Binary 0b00011, Left & Right are Pressed
>>>
[User Releases Right]
km.\1\r\n          # Binary 0b00001, Left is Pressed
>>>
[User Presses Front Side]
km.\17\r\n         # Binary 0b10001, Left & Front Side are Pressed
>>>
[User Presses Back Side]
km.\25\r\n         # Binary 0b11001, Left & Front & Back Side are Pressed
>>>
[User Releases Left]
km.\24\r\n         # Binary 0b11000, Front & Back Side are Pressed
>>>
[User Releases Front Side]
km.\8\r\n          # Binary 0b01000, Back Side is Pressed
>>>
[User Releases Back Side]
km.\0\r\n          # Binary 0b00000, Nothing is Pressed
>>>
```

## Footnotes

This is a rather complex feature. If it were up to me, I would rewrite it to be more developer friendly. However, for
compatibility's sake, it must remain.

Eventually, when I write the new API, I'm sure this will be done in an easier way.

For now, read slow, re-read, and ask ChatGPT to summarize if you don't understand, as it should be simple enough for it
to understand very well.
