# StrFormat,DirPath

**Alias**: `StrFormat,Path`

Returns a path without the filename or extension.

## Syntax

```pebakery
StrFormat,DirPath,<FilePath>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| FilePath | The full path of the file. This can also be a URL. |
| DestVar | Variable where the result will be stored. |

## Remarks

If `FilePath` does not exist the operation will fail.

## Related

[StrFormat,Ext](./Ext.md), [StrFormat,FileName](./FileName.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-DirPath
Description=Show usage of the StrFormat,DirPath Command
Author=Homes32
Level=5
Version=1

[Variables]
%File%=C:\Windows\System32\HAL.DLL

[Process]
StrFormat,DirPath,%File%,%result%
Message,"DirPath: %result%"
```

### Example 2

Retrieve the FileName and Path from a URL.

```pebakery
[Main]
Title=StrFormat-DirPath2
Description=Show usage of the StrFormat,DirPath Command
Author=Homes32
Level=5
Version=1

[Variables]
%URL%=http://live.sysinternals.com/Bginfo.exe

[Process]
StrFormat,FileName,%URL%,%name%
StrFormat,DirPath,%URL%,%path%
Message,"Downloading %name% from#$x%path%"
```