# StrFormat,PathCombine

Combines a path with a filename to form a full path. 

## Syntax

```pebakery
StrFormat,PathCombine,<DirPath>,<FileName>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| DirPath | The path of the file. |
| FileName | The name and extension of the file. |
| DestVar | Variable where the result will be stored. |

## Remarks

PEBakery will add a trailing `\` to `DirPath` if it does not exist.

## Related

[StrFormat,DirPath](./DirPath.md), [StrFormat,Ext](./Ext.md), [StrFormat,FileName](./FileName.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-PathCombine
Description=Show usage of the StrFormat,PathCombine Command
Author=Homes32
Level=5
Version=1

[Variables]
%File%=HAL.DLL
%Path%=C:\Windows\System32\

[Process]
StrFormat,PathCombine,%Path%,%File%,%result%
Message,"Combined Path: %result%"
```