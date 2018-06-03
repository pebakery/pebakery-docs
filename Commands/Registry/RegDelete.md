# RegDelete

Deletes a key or value from the registry.

## Syntax

```pebakery
RegDelete,<HKEY>,<KeyPath>[,ValueName]
```

### Arguments

| Argument | Description |
| --- | --- |
| HKEY | The root key must be one of the following: |
|| HKEY_LOCAL_MACHINE or HKLM |
|| HKEY_CURRENT_CONFIG or HKCC |
|| HKEY_CLASSES_ROOT or HKCR |
|| HKEY_CURRENT_USER or HKCU |
|| HKEY_USERS or HKU |
| KeyPath | The full path of the registry key. |
| ValueName | **(Optional)** The value to be deleted. If `ValueName` is not specified the entire registry key will be removed. |

## Remarks

None.

## Related

[RegHiveLoad](./RegHiveLoad.md), [RegHiveUnload](./RegHiveUnload.md)

## Examples

### Example 1

Delete a registry value.

```pebakery
RegHiveLoad,Tmp_System,%RegSystem%
RegDelete,HKLM,Tmp_System\ControlSet001\Services\VgaSave\Device0,DefaultSettings.XResolution
RegHiveUnLoad,Tmp_System
```

### Example 2

Delete a registry key.

```pebakery
RegHiveLoad,Tmp_System,%RegSystem%
RegDelete,HKLM,Tmp_System\ControlSet001\Services\VgaSave\Device0
RegHiveUnLoad,Tmp_System
```
