# CopyOrExpand

Copy or Extract files from a Microsoft Cabinet Archive (*.CAB).

If the source file exists, it will be copied to the `DestPath`. Otherwise, PEBakery will search for a compressed cabinet (*.ex_, *.dl_) and extract the file.

## Syntax

```pebakery
CopyOrExpand,<SrcFile>,<DestPath>,[PRESERVE],[NOWARN]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcFile | The full path of the file to copy. Wildcards (*, ?) can be used to CopyOrExpand multiple files. |
| DestPath | The full path where the file will be copied or extracted. |

### Flags

| Flag | Description |
| --- | --- |
| PRESERVE | Do not overwrite existing files. |
| NOWARN | Do not log an overwrite warning if a file is overwritten. |

Flags can be specified in any order.

## Remarks

PEBakery searches for files in the following order:

1. Copy
1. Expand

This command is mainly used to extract compressed EXE (\*.EX\_) and DLL (\*.DL\_) files from NT5 (WindowsXP) sources.

Expansion is performed using 7z.dll.

## Related

[Expand](./Expand.md)

## Examples

```pebakery
// If EXPLORER.EXE exists, it will be copied to %DestDir%.
// If EXPLORER.EXE does not exist, EXPLORER.EXE will be extracted from EXPLORER.EX_.
CppyOrExpand,%SrcDir%\EXPLORER.EXE,%DestDir%
```

```pebakery
// If EXPLORER.EXE exists, it will be copied to %DestDir% with the new name NEWEXP.EXE.
// If EXPLORER.EXE does not exist, EXPLORER.EXE will be extracted from EXPLORER.EX_ with the new name NEWEXP.EXE.
CppyOrExpand,%SrcDir%\EXPLORER.EXE,%DestDir%\NEWEXP.EXE
```
