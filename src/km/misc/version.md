# Version

The `km.version()` command can be used to retrieve the device version. This is a more universal command used to
determine hardware being used, such as MAKCU vs Ferrum.

TODO: Move the below line to the [Legacy API](../../legacy_api.md) section once it is added.
When connected to the [Ferrum Legacy API](../../legacy_api.md), this command returns "kmbox: 2.0.0 Aug 31 2020 21:49:51"
for compatibility with legacy software.

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
