# DirCopy

Copies a directory along with all sub-directories and files.

Wildcards are supported, allowing multiple directories to be copied at one time.

## Syntax

```pebakery
DirCopy,<SrcDir>,<DestDir>
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcDir | Full path of the directory to copy. Wildcards (*, ?) are allowed. |
| DestDir | Full path to the destination directory. The directory structure will be created if it does not exist. If the directory exists it will be overwritten. |

## Remarks

If `DestDir` is a file, DirCopy fails.

WinBuilder 082 has a bug that DirCopy works similar to FileCopy when wildcards are used. Turning on compatibility option `Simulate WinBuilder's DirCopy Asterisk Bug` emulates this bug. See Example 2 for more details.

## Related

[DirMove](./DirMove.md),[DirDelete](./DirDelete.md), [FileCopy](./FileCopy.md), [PathMove](./PathMove.md)

## Examples

Let us assume a directory `%SrcDir%` *C:\Temp\Src* contains these files:

```pebakery
C:\Temp\Src\
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

```pebakery
// The entire %SrcDir% will be copied into %DestDir%.
DirCopy,%SrcDir%,%DestDir%
```

**Result**

```pebakery
C:\Temp\Dest\
|--- Src\
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

### Example 2

```pebakery
// All files of %SrcDir% will be copied into %DestDir%.
DirCopy,%SrcDir%\A*,%DestDir%
```

**Result**

```pebakery
C:\Temp\Dest\
|--- AAA\
     |--- A.txt
|--- ABB\
     |--- B.ini
|--- ACC\
     |--- C.txt
     |--- D.txt
|--- AEE\
```

**Result when using the compatibility option to simulate WinBuilder's DirCopy Asterisk Bug**

```pebakery
C:\Temp\Dest\
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