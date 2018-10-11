# StrFormat,ShortPath

Converts a path into `DOS 8.3` compatible format.

**This command has been deprecated and will be removed in a future release.**

## Syntax

```pebakery
StrFormat,ShortPath,<Path>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| Path | The full path to convert. |
| DestVar | The variable where the result will be saved. |

## Remarks

Successful conversion to a short path depends on the registry value `HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation`, therefore this command cannot be guaranteed to work properly on every system.

## Related

[StrFormat,LongPath](./LongPath.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-ShortPath Example
Description=Demonstrate usage of StrFormat,ShortPath.
Level=5
Version=1
Author=Homes32

[variables]
%path%="C:\Program Files (x86)\Notepad++\Notepad++.exe"

[process]
StrFormat,ShortPath,%path%,%result%
Message,"ShortPath: %result%"
```