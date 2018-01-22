# PathMove

Moves a file or directory.

## Syntax

```pebakery
PathMove,<SrcPath>,<DestPath>
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcPath | Full path of the file or directory to move. |
| DestPath | Destination Path. |

## Remarks

Turning on compatibility option `FileRename and DirMove work like PathMove` makes FileRename and DirMove identical to PathMove.

## Related

[DirMove](./DirMove.md), [FileRename](./FileRename.md)

## Examples

### Example 1

`A.txt` will be renamed to `B.txt`.

```pebakery
PathMove,%SrcDir%\A.txt,%SrcDir%\B.txt
```

### Example 2

`%SrcDir%\A.txt` will be moved into `%DestDir%\B.txt`.

```pebakery
PathMove,%SrcDir%\A.txt,%DestDir%\B.txt
```

### Example 3

If %DestDir% exists: `%SrcDir%\A` will be moved into `%DestDir%\A`.
If %DestDir% does not exist: `%SrcDir%\A` will be moved into `%DestDir%`.

```pebakery
PathMove,%SrcDir%\A,%DestDir%
```
