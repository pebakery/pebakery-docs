# StrFormat,LongPath

Converts a `DOS 8.3` path to a long `NT` path.

**This command has been depreciated and will be removed in a future release.**

## Syntax

```pebakery
StrFormat,LongPath,<Path>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| Path | The full path to convert. |
| DestVar | The variable where the result will be saved. |

## Remarks

Successful conversion to a long path depends on the registry value `HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation`, therefore this command cannot be guaranteed to work properly on every system.

## Related

[StrFormat,ShortPath](./ShortPath.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-LongPath Example
Description=Demonstrate usage of StrFormat,LongPath.
Level=5
Version=1
Author=Homes32

[variables]
%path%="C:\Progra~2\Notepad++\Notepad++.exe"

[process]
StrFormat,LongPath,%path%,%result%
Message,"LongPath: %result%"
```