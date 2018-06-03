# FileRename

**Alias**: `FileMove`

Rename or move a file.

## Syntax

```pebakery
FileRename,<SrcPath>,<DestPath>
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcPath | Full path of the file to rename. |
| DestPath | New path of the renamed file. |

## Remarks

`FileRename` can also be used to move a file.

WinBuilder 082 allows `FileRename` to move a directory. Turning on compatibility option `FileRename and DirMove work like PathMove` makes `FileRename` identical to `PathMove`.

## Related

[FileCopy](./FileCopy.md), [PathMove](./PathMove.md)

## Examples

### Example 1

`A.txt` will be renamed to `B.txt`.

```pebakery
FileRename,%SrcDir%\A.txt,%SrcDir%\B.txt
```

### Example 2

`%SrcDir%\A.txt` will be moved into `%DestDir%\B.txt`.

```pebakery
FileMove,%SrcDir%\A.txt,%DestDir%\B.txt
```
