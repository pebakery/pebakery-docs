# Expand

Extract files from a Microsoft Cabinet Archive (*.CAB).

## Syntax

```pebakery
Expand,<CabFile>,<DestDir>,[FileName],[PRESERVE],[NOWARN]
```

### Arguments

| Argument | Description |
| --- | --- |
| CabFile | The full path of the cabinet file to extract. |
| DestDir | Directory where the files will be extracted. |
| FileName | **(Optional)** Extract only this specific file. |

### Flags

| Flag | Description |
| --- | --- |
| PRESERVE | **(Optional)** Do not overwrite existing files when `SingleFile` is specified. |
| NOWARN | **(Optional)** Do not log an overwrite warning if a file is overwritten when extracting a single file. |

Flags can be specified in any order.

## Remarks

This command is mainly used to extract compressed EXE (\*.EX\_) and DLL (\*.DL\_) files from NT5 (WindowsXP) sources.

Expansion is performed using [7-Zip](https://www.7-Zip.org).

## Related

[CopyOrExpand](./CopyOrExpand.md)

## Examples

```pebakery
// ex1.cab will be decompressed into %DestDir%.
Expand,%SrcDir%\ex1.cab,%DestDir%
```

```pebakery
// EXPLORER.EXE will be extracted from EXPLORER.EX_
Expand,%Source_Win%\EXPLORER.EX_,%Target_Win%
```

```pebakery
// Extract only BatteryLine.exe from multi.cab, overwrite with warning if file exists.
Expand,%SrcDir%\multi.cab,%DestDir%,BatteryLine.exe
```

```pebakery
// Extract only BatteryLine.exe from multi.cab, do not overwrite if file exists.
Expand,%SrcDir%\multi.cab,%DestDir%,BatteryLine.exe,PRESERVE
```
