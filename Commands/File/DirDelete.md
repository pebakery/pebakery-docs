# DirDelete

Deletes a directory and all files and sub-directories it contains.

## Syntax

```pebakery
DirDelete,<DirPath>
```

### Arguments

| Argument | Description |
| --- | --- |
| DirPath | Full path of the directory to delete. |

## Remarks

If `DirPath` does not exist the build will halt.

**Deleted folders are permanently removed can not be recovered from the recycle bin.**

## Related

[FileDelete](./FileDelete.md)

## Examples

### Example 1

```pebakery
// C:\Temp will be deleted.
DirDelete,C:\Temp
```