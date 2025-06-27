# Command Echoing

For maximum compatibility with software expecting a Python interface, the Ferrum serial interface implements command
echoing, as well as an input prompt.

This means that when a command is sent to Ferrum, it will repeat the command back, then send the result of the command,
and then send the input prompt (`>>> `). Note that the echo uses the same [line terminator](../line_terminator.md) as the
original command, and that the input prompt is exactly three right facing arrows, followed by a single space, and no
line terminator.

## Examples

Note these examples use raw data, meaning `\r` is not a backslash and an r, but instead the carriage return character.
If you don't understand what this means, try asking ChatGPT, or Googling it.

### Using \r\n

Input:
```python
km.left()\r\n
```

Output:
```python
km.left()\r\n
1\r\n
>>>           # Note this line is `>>> ` with a single space.
```

### Using \n

Input:
```python
km.left()\n
```

Output:
```python
km.left()\n
1\r\n
>>>           # Note this line is `>>> ` with a single space.
```

### A Command with No Response

Input:
```python
km.left(1)\n
```

Output:
```python
km.left(1)\n
>>>           # Note this line is `>>> ` with a single space.
```