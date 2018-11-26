# FileCopy

Copies one or more files.

Wildcards are supported, allowing multiple files to be copied at one time.

## Syntax

```pebakery
FileCopy,<SrcFile>,<DestPath>[,PRESERVE][,NOWARN][,NOREC]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcFile | File(s) to copy. Wildcards (* ?) are allowed. |
| DestPath | Destination path. This can be either a file name or a directory if multiple files are to be copied. The directory structure will be created if it does not exist. |

### Flags

Flags may be specified in any order.

| Flag | Description |
| --- | --- |
| PRESERVE | **(Optional)** Do not overwrite existing files. |
| NOWARN | **(Optional)** Do not log a warning if a file is overwritten or if `SrcFile` contains a wildcard pattern resulting in no matching files. |
| NOREC | **(Optional)** Do not copy files in subdirectories when using wildcards. |

## Remarks

When wildcard is used in filename, `FileCopy` copies subdirectories by default. To prevent this, use the `NOREC` flag.

Wildcards cannot be used in directory names.

## Related

[DirCopy](./DirCopy.md), [DirCreate](./DirCreate.md), [FileDelete](./FileDelete.md), [FileMove](./FileMove.md), [PathMove](./PathMove.md)

## Examples

Let us assume a directory `%SrcDir%` _C:\Temp\Src_ contains these files:

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

`C:\Temp\AZ.txt` will be copied into %DestDir% `C:\Temp\myFolder\`

```pebakery
FileCopy,%SrcDir%\AZ.txt,%DestDir%
```

Result

```pebakery
C:\Temp\myFolder\
|--- AZ.txt
```

### Example 2

`C:\Temp\AZ.txt` will be copied into %DestDir%\ `C:\Temp\myFolder\` and renamed `B.txt`

```pebakery
FileCopy,%SrcDir%\AZ.txt,%DestDir%\B.txt
```

Result

```pebakery
C:\Temp\myFolder\
|--- B.txt
```

### Example 3

All `.txt` files in %SrcDir% will be copied under %DestDir%.

```pebakery
FileCopy,%SrcDir%\*.txt,%DestDir%
```

Result

```pebakery
C:\Temp\myFolder\
|--- AAA\
     |--- A.txt
|--- ACC\
     |--- C.txt
     |--- D.txt
|--- AZ.txt
```

### Example 4

All `.txt` files in %SrcDir% will be copied under %DestDir%, ignoring subdirectories.

```pebakery
FileCopy,%SrcDir%\*.txt,%DestDir%,NOREC
```

Result

```pebakery
C:\Temp\myFolder\
|--- AZ.txt
```
