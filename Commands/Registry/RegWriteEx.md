# RegWriteEx

Create or modify a key or value in the registry.

`RegWriteEx` functions in the same way as `RegWrite` with the exception that `RegWriteEx` does not verify `ValueType`, allowing you to specify an arbitrary type such as `0x200000`.

## Syntax

```pebakery
RegWriteEx,<HKey>,<ValueType>,<KeyPath>,<ValueName>,<Value>,[NOWARN]
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
| ValueType   | The type of data the value contains. Can be one of the Standard types below or an arbitrary hex value. |
||0x0 - (REG_NONE) Empty Key |
||0x1 - (REG_SZ) String |
||0x2 - (REG_EXPAND_SZ) Expanded String - Will expand any variable value contained inside %%. (e.g. %temp%) |
||0x3 - (REG_BINARY) Binary data - Data is specified in HEX, with each byte being specified by groups of two digits splitting each value with commas. |
||0x4 - (REG_DWORD) 32bit integer |
||0x7 - (REG_MULTI_SZ) Multiple Null Separated Strings |
||0x11 - (REG_QWORD) 64bit integer |
| KeyPath | The full path of the registry key. |
| ValueName | The name of the value. |
| Value | The value to write.<br/>Large values can be wrapped for easier reading by using the `\` character to indicate that the value continues on the next line, similar to the .reg file format. **Note:** If the `Value` to be written is the `\` character eg. `RegWriteEx,HKLM,0x1,Tmp_System\Setup,OsLoaderPath,"\"` be sure to wrap it in double quotes so it is not mistaken for a line continuation.  |

### Flags

| Flag | Description |
| --- | --- |
| NOWARN | **(Optional)** Suppress Overwrite messages in the log if the `Value` already exists. |

## Remarks

PEBakery does not permit use of variables in `HKey` and `ValueType`.

If you need to modify the value of an ***existing*** REG_MULTI_SZ value consider using the `RegMulti` command to insert and delete values without overwriting the entire value list.

If you are calling RegWriteEx outside of the `[Process]` section and the registry value contains a `#` hash sign followed by one or more digits you should always use the escaped form `##` in order to prevent PEBakery from interpreting the hash as a parameter.

If you have a large number of keys to import it may be feasible to encode a _.reg_ file within the script and use the `RegImport` command to load the values into the PE's registry.

## Related

[RegHiveLoad](./RegHiveLoad.md), [RegHiveUnload](./RegHiveUnload.md), [RegImport](./RegImport), [RegMulti](./RegMulti.md), [RegWrite](./RegWrite.md)

## Examples

### Example 1

```pebakery
RegHiveLoad,Tmp_Drivers,%RegDrivers%
RegWriteEx,HKLM,0x200000,"Tmp_Install_Drivers\DriverDatabase\DriverPackages\monitor.inf_amd64_80f68dff92eaa9bf\Configurations\NonPnPMonitor.Install\Driver","MaxResolution",""
RegWriteEx,HKLM,0x100000,"Tmp_Install_Drivers\DriverDatabase\DriverPackages\monitor.inf_amd64_80f68dff92eaa9bf\Configurations\NonPnPMonitor.Install\Driver","MODES",""

RegHiveUnLoad,Tmp_Drivers
```
