# Command Syntax

Commands sent over the serial port follow Python function call syntax: `name(arg1, arg2, ...)`, followed by a
[Line Terminator](./line_terminator.md). This page describes how Ferrum parses that input.

This does not apply to the [Legacy API](../legacy_api.md).

## Ignored Characters

Before a command is parsed, all whitespace, and every character other than letters, numbers, and `+-_.,()[];=`, is
removed. This means spacing does not matter, and quotes are optional.

`+` and `-` are kept so they can be used both as number signs (ex: `km.move(-5, +5)`) and in command names (ex:
[`km.lock_mx+`](../software_api/km_api/mouse/axes/lock.md#directional-locks)).

For example, all of the following are treated identically:

```python
km.move(1, 2)
km.move(1,2)
km . move ( 1 , 2 )
```

As are these:

```python
km.down('a')
km.down("a")
km.down(a)
```

A side effect of this is that arguments cannot contain any of the removed characters, nor `;`, `,`, or `=`, which have
special meaning. See [Keys](../software_api/km_api/keyboard/keys.md) for how this affects key strings.

## Keyword Arguments

Some commands, such as [`km.controller`](../software_api/km_api/controller/controller_state.md), take keyword arguments
in the form `name=value`, like Python. Keyword arguments can be given in any order, and any of them can be left out.

Like Python, `None` is used as a value to mean "no value". Its meaning depends on the command.

```python
km.controller(a=1, hold=100)
km.controller(hold=100, a=1)   # Identical to the above.
km.controller(a=None)
```

## Multiple Commands per Line

Multiple commands can be sent on a single line by separating them with a `;`. Every command is run in order, the line
is echoed back once, and **only the result of the last command that produced a result** is returned.

Input:
```python
km.left(); km.right()
```

Output:
```python
km.left(); km.right()
0                  # The result of km.right(). The result of km.left() is discarded.
>>>
```

## Invalid Commands

A line that is not a valid command, such as one missing its parentheses, having unbalanced parentheses or brackets, or
having extra text after the closing parenthesis, is discarded. Keep this in mind if your software waits for a response.

Input:
```python
km.left
```

Output:
```python
                   # Nothing is sent back.
```

## Unsupported Commands

Any command beginning with `km.` or `device.` that Ferrum does not support is accepted and ignored. It is echoed back
for KM API compatibility, but has no effect otherwise.
