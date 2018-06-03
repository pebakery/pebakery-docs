# FileVersion

**Alias**: `Retrieve,FileVersion`

Retrieves the version number of the specified file.

## Syntax

```pebakery
FileVersion,<FilePath>,<DestVar>
```

### Arguments

| Argument | Description |
| --- | --- |
| FilePath | Full path of the file. |
| DestVar | Variable where the file version will be stored. |

## Remarks

If version information is not available the command returns `0.0.0.0`

## Related

## Example

```pebakery
[Main]
Title=FileVersion
Description=Show the usage of FileVersion.
Level=5
Version=1
Author=Homes32

[Variables]
%File%=C:\Windows\notepad.exe

[process]
FileVersion,%File%,%Ver%
Message,"%File%#$xFile Version: %Ver%"
```