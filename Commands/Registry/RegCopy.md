# RegCopy

Copies all subkeys and values from one registry key to another.

Wildcards are supported, allowing multiple registry keys to be copied at one time.

## Syntax

```pebakery
RegCopy,<SrcKey>,<SrcKeyPath>,<DestKey>,<DestKeyPath>[,WILDCARD]
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

### Flags

| Flag | Description |
| --- | --- |
| WILDCARD | **(Optional)** Use this flag to cause PEBakery to interpret `* ?` characters as wildcards to enable copying multiple keys at one time. |

## Remarks

`RegCopy` will copy from your **local** registry, so you must ensure that `SrcKeyPath` and/or `DestKeyPath` point to your mounted PE hive if you intend to copy to/from the PE registry.

The Windows registry allows the use of wildcard characters (? \*) in key names (eg. _HKLM\Software\PEBakery*?_ or _HKLM\Software\My*Registry?Key_). Keep this in mind when using the `WILDCARD` flag and limit the scope of your search as much as possible in order to avoid unintended results.

**Important:** `RegCopy` does not duplicate the security attributes of the keys and values that it copies. Rather, all security attributes in the destination key are the default attributes.

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

### Example 2

Copy all registry keys under _HKLM\DriverDatabase\DriverPackages_ that begin with _bda.inf_.

```pebakery
RegHiveLoad,Tmp_Drivers,%RegDrivers%
RegHiveLoad,Tmp_Install_Drivers,%RegInstallDrivers%
RegCopy,HKLM,Tmp_Install_Drivers\DriverDatabase\DriverPackages\bda.inf*,HKLM,Tmp_Drivers\DriverDatabase\DriverPackages,WILDCARD
RegHiveUnload,Tmp_Drivers
RegHiveUnload,Tmp_Install_Drivers
```