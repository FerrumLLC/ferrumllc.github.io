# Controller

This section covers all km commands that affect devices designated as Controllers, such as Xbox and Playstation
controllers.

## Axes

A controller has 6 axes. Sticks use the range `-32768` to `32767`, centered at `0`, where positive is up or right, and
negative is down or left.
Triggers use the range `0` (released) to `65535` (fully pressed).

<center><b>Axes</b></center>

| Axis Names | Axis                   | Range               |
| ---------- | ---------------------- | ------------------- |
| lx         | left stick horizontal  | `-32768` to `32767` |
| ly         | left stick vertical    | `-32768` to `32767` |
| rx         | right stick horizontal | `-32768` to `32767` |
| ry         | right stick vertical   | `-32768` to `32767` |
| lt, l2     | left trigger           | `0` to `65535`      |
| rt, r2     | right trigger          | `0` to `65535`      |

## Buttons

A controller has up to 17 buttons. Each can be named by its Xbox or Playstation name (case-insensitive).

When reading every button at once, the buttons are combined into a single number, where each button is one bit. The
`Bit` column shows each button's bit, so a button is pressed if `buttons & (1 << bit)` is not `0`.

<center><b>Buttons</b></center>

| Bit | Xbox Names    | Playstation Names | Button                       |
| --- | ------------- | ----------------- | ---------------------------- |
| 0   | up            | up                | D-pad up                     |
| 1   | right         | right             | D-pad right                  |
| 2   | down          | down              | D-pad down                   |
| 3   | left          | left              | D-pad left                   |
| 4   | y             | triangle          | top face button              |
| 5   | b             | circle            | right face button            |
| 6   | a             | cross             | bottom face button           |
| 7   | x             | square            | left face button             |
| 8   | ls            | l3                | left stick press             |
| 9   | rs            | r3                | right stick press            |
| 10  | lb            | l1                | left bumper                  |
| 11  | rb            | r1                | right bumper                 |
| 12  | view, back    | create            | left center button           |
| 13  | menu, start   | options           | right center button          |
| 14  | share         | touchpad          | center button                |
| 15  | home, guide   | ps                | home button                  |
| 16  |               | mute              | mute button                  |

Triggers are axes rather than buttons (see [Axes](#axes)), due to being analog.

Note that `share` refers to the Xbox Share button (the center button). The Playstation 4's Share button is the left
center button, named `create`.
