# StrFormat,IntToBytes

Converts an number of bytes to a more human readable format. Any amount of bytes specified will be converted to a string representing the size in KB, MB, GB, TB or PB.

## Syntax

```pebakery
StrFormat,IntToBytes,<Bytes>,<%DestVar%> 
```

### Arguments

| Argument | Description |
| --- | --- |
| Bytes | Bytes to format. |
| DestVar | Variable where the resulting string will be stored. |

## Remarks

PEBakery commands such as `DirSize`, `FileSize`, and `System,GetFreeSpace` return the size in bytes. This function is useful for converting the size in bytes to a more human readable format.

The operation can be reversed using the `StrFormat,BytesToInt` command.

## Related

[DirSize](../File/DirSize.md), [FileSize](../File/FileSize.md), [StrFormat, BytesToInt](./BytesToInt), [System,GetFreeSpace](../System/GetFreeSpace.md)

## Examples

### Example 1

In this example we get the size of a directory using `DirSize` and convert the result to a more readable format.

```pebakery
[Main]
Title=IntToBytes
Description=Show the usage of StrFormat,IntToBytes.
Level=5
Version=1
Author=Homes32

[Variables]
%Dir%=C:\Windows\System32

[process]
DirSize,%Dir%,%Size%
// Use StrFormat to convert the size to a more human readable format.
StrFormat,IntToBytes,%Size%,%StrSize%
Message,"Dir Size: %Size% bytes (%StrSize%)"
```