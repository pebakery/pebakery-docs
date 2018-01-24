# StrFormat,Ext

Returns the file extension from a path.

## Syntax

```pebakery
StrFormat,Ext,<FilePath>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| FilePath | The full path of the file. This can also be a URL. |
| DestVar | Variable where the result will be stored. |

## Remarks

If `FilePath` does not exist the operation will fail.

## Related

[StrFormat,DirPath](./DirPath.md), [StrFormat,FileName](./FileName.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Ext
Description=Show usage of the StrFormat,Ext Command
Author=Homes32
Level=5
Version=1

[Variables]
%File%=C:\Windows\System32\HAL.DLL

[Process]
StrFormat,Ext,%File%,%result%
Message,"File Ext: %result%"
```