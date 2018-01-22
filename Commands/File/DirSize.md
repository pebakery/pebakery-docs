# DirSize

**Alias**: `Retrieve,DirSize`

Gets the size of a directory.

## Syntax

```pebakery
DirSize,<DirPath>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| DirPath | Full path of the directory. |
| DestVar | Variable where the directory size (in bytes) will be stored. |

## Remarks

If `DirPath` contains files that cannot be accessed with `Administrator` privileges PEBakery ignores them.

You can use `StrFormat,Bytes` to convert the size to a more human readable format. (Ex. 3.5GB)

## Related

[FileSize](./FileSize.md), [StrFormat,Bytes](../String/Bytes.md)

## Examples

### Example 1

```pebakery
[Main]
Title=DirSize
Description=Show the usage of DirSize.
Level=5
Version=1
Author=Homes32

[Variables]
%Dir%=C:\Windows\System32

[process]
DirSize,%Dir%,%Size%
// Use StrFormat to convert the size to a more human readable format.
StrFormat,Bytes,%Size%,%StrSize%
Message,"Dir Size: %Size% bytes (%StrSize%)"
```
