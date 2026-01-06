# Version

<div style="background-color: rgb(61, 44, 0); border: 1px solid rgb(251, 212, 106); color: rgb(251, 212, 106); padding: 15px; border-radius: 5px; margin-bottom: 15px;">
    This API has been deprecated in favor of the <a href="../../software_api.md" style="color: #3498db; text-decoration: underline;">Software API</a>.
</div>

The `km.version()` command in the Legacy API strictly returns `kmbox: 2.0.0 Aug 31 2020 21:49:51`, matching older KMBox
devices. This is for compatibility with legacy software, which may not be updated to work with newer devices.

## Examples

### Fetching the Device Version

Input:
```python
km.version()
```

Output:
```python
km.version()
kmbox: 2.0.0 Aug 31 2020 21:49:51
>>>
```
