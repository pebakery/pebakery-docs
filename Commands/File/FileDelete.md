# FileDelete

Deletes a file.

Wildcards are supported, allowing multiple files to be deleted at one time.

## Syntax

```pebakery
FileDelete,<FilePath>,[NOWARN],[NOREC]
```

### Arguments

| Argument | Description |
| --- | --- |
| FilePath | File or files to delete. Wildcards (*, ?) are allowed. |

### Flags

Flags may be specified in any order.

| Flag | Description |
| --- | --- |
| NOWARN | **(Optional)** Do not log a warning if the files do not exist. |
| NOREC | **(Optional)** Ignore subdirectories when deleting files using wildcards. |

## Remarks

When wildcards are used files in subdirectories will also be deleted. To prevent this, use `NOREC` flag.

**Deleted folders are permanently removed can not be recovered from the recycle bin.**

## Related

[DirDelete](./DirDelete.md), [FileCopy](./FileCopy.md), [PathMove](./PathMove.md)

## Examples

Let us assume a directory `%SrcDir%` *C:\Temp* contains these files:

```pebakery
C:\Temp\
|--- AAA\
     |--- A.txt
|--- ABB\
     |--- B.ini
|--- ACC\
     |--- C.txt
     |--- D.txt
|--- AEE\
|--- Y.ini
|--- AZ.txt
```

### Example 1

`C:\Temp\AZ.txt` will be deleted.

```pebakery
FileDelete,%SrcDir%\AZ.txt
```

**Result**

```pebakery
C:\Temp\
|--- AAA\
     |--- A.txt
|--- ABB\
     |--- B.ini
|--- ACC\
     |--- C.txt
     |--- D.txt
|--- AEE\
|--- Y.ini
```

### Example 2

All `.txt` files in %SrcDir% will be deleted, including those located in subdirectories.

```pebakery
FileDelete,%SrcDir%\*.txt
```

**Result**

```pebakery
C:\Temp\
|--- AAA\
|--- ABB\
     |--- B.ini
|--- ACC\
|--- AEE\
|--- Y.ini
```

### Example 3

All `.ini` files in %SrcDir% will be deleted, ignoring any files located in subdirectories.

```pebakery
FileDelete,%SrcDir%\*.ini,NOREC
```

**Result**

```pebakery
C:\Temp\
|--- AAA\
     |--- A.txt
|--- ABB\
     |--- B.ini
|--- ACC\
     |--- C.txt
     |--- D.txt
|--- AEE\
|--- AZ.txt
```
