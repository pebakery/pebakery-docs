# FileSize

**Alias**: `Retrieve,FileSize`

Gets the size of a file.

## Syntax

```pebakery
FileSize,<FilePath>,<DestVar>
```

### Arguments

| Argument | Description |
| --- | --- |
| FilePath | Full path of the file. |
| DestVar | Variable where the file size (in bytes) will be stored. |

## Remarks

You can use `StrFormat,BytesToInt` to convert the size to a more human readable format. (Ex. 3.5MB)

## Related

[DirSize](./DirSize.md), [StrFormat,BytesToInt](../String/BytesToInt.md)

## Examples

### Example 1

```pebakery
[Main]
Title=FileSize
Description=Show the usage of FileSize.
Level=5
Version=1
Author=Homes32

[Variables]
%File%=C:\Windows\notepad.exe

[process]
FileSize,%File%,%Size%
// Use StrFormat to convert the size to a more human readable format.
StrFormat,Bytes,%Size%,%StrSize%
Message,"File Size: %Size% bytes (%StrSize%)"
```
