# Version

The `km.version()` command can be used to retrieve the device version. This is a more universal command used to
determine hardware being used, such as MAKCU vs Ferrum.

When connected to the Ferrum App, and thus using the [Keyboard Mouse API](../../km_api.md), this command returns
"kmbox: Ferrum", formatted as such for compatibility with legacy software.

## Examples

### Fetching the Device Version

Input:
```python
km.version()
```

Output:
```python
km.version()
kmbox: Ferrum
>>>
```
