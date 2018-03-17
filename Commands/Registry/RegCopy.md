# RegCopy

Copies all subkeys and values from one registry key to another.

This command has the same effect as running `REG.exe COPY <SrcRegPath> <DestRegPath> /S /F` from Windows.

## Syntax

```pebakery
RegCopy,<SrcKey>,<SrcKeyPath>,<DestKey>,<DestKeyPath>
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcKey | The source root key must be one of the following: |
|| HKEY_LOCAL_MACHINE or HKLM |
|| HKEY_CURRENT_CONFIG or HKCC |
|| HKEY_CLASSES_ROOT or HKCR |
|| HKEY_CURRENT_USER or HKCU |
|| HKEY_USERS or HKU |
| SrcKeyPath | The full path of the registry key to copy. |
| DestKey | The destination root key must be one of the following: |
|| HKEY_LOCAL_MACHINE or HKLM |
|| HKEY_CURRENT_CONFIG or HKCC |
|| HKEY_CLASSES_ROOT or HKCR |
|| HKEY_CURRENT_USER or HKCU |
|| HKEY_USERS or HKU |
| DestKeyPath | The full path of the destination key. Existing values will be overwritten. |

## Remarks

`RegCopy` will copy from your **local** registry, so you must ensure that `SrcKeyPath` and/or `DestKeyPath` point to your mounted PE hive if you intend to copy to/from the PE registry.

## Related

[RegHiveLoad](./RegHiveLoad.md), [RegHiveUnload](./RegHiveUnload.md)

## Examples

### Example 1

```pebakery
RegHiveLoad,Tmp_Ins_System,InstallSrc\windows\system32\config\SYSTEM
RegHiveLoad,Tmp_System,%RegSystem%
// Copy HKLM\System\ControlSet001\Services\Tcpip and all subkeys/values from Install.wim registry to Boot.wim registry
RegCopy,HKLM,Tmp_Ins_System\ControlSet001\Services\Tcpip,HKLM,Tmp_System\ControlSet001\Services\Tcpip
RegHiveUnLoad,Tmp_System
RegHiveUnLoad,Tmp_Ins_System
```