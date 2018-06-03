# DirMove

Moves a directory.

## Syntax

```pebakery
DirMove,<SrcDir>,<DestPath>
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcDir | Full path of the directory to move. |
| DestPath | Full path of the destination directory. The directory structure will be created if it does not exist. Any existing files will be overwritten. |

## Remarks

WinBuilder 082 allows DirMove to move files. Turning on the compatibility option `FileRename and DirMove work like PathMove` makes the `DirMove` command identical to `PathMove`.

## Related

[DirCopy](./DirCopy), [DirDelete](./DirDelete), [PathMove](./PathMove.md)

## Examples

### Example 1

```pebakery
DirMove,%SrcDir%\A,%DestDir%
```
