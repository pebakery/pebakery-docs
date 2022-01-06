# FileCreateBlank

Creates an empty file.

## Syntax

```pebakery
FileCreateBlank,<FilePath>,[Encoding=<Encoding>],[PRESERVE],[NOWARN]
```

### Arguments

| Argument | Description |
| --- | --- |
| FilePath | Path to create empty file. The directory structure will be created if it does not exist. |
| Encoding= | **(Optional)** Character encoding to use in the new file. Supported encodings are : |
|| If no encoding is specified the file is encoded as UTF8 without BOM |
|| `ANSI` - ANSI |
|| `UTF8` - UTF-8 **(Default)** |
|| `UTF8BOM` - UTF-8 BOM |
|| `UTF16`, `UTF16LE` - UTF-16 Little Endian |
|| `UTF16BE` - UTF-16 Big Endian |

### Flags

Flags may be specified in any order.

| Flag | Description |
| --- | --- |
| PRESERVE | **(Optional)** Do not overwrite existing files. |
| NOWARN | **(Optional)** Do not log a warning if file is overwritten. |

## Remarks

Some commands such as `TXTAddLine` require that the file exists before it can be written. This command can be to create an empty text file if the target file does not exist.

For batch files (*.bat, *.cmd), use `ANSI` encoding. For normal text files, `UTF8` or `UTF16` encoding is highly recommended.

## Related

[TXTAddLine](../Text/TXTAddLine.md)

## Examples

### Example 1

Create empty file Unicode.txt, write BOM (U+FEFF) encoded with UTF-16 Little Endian.

```pebakery
FileCreateBlank,C:\Temp\Unicode.txt,UTF16
```

### Example 2

This sample script checks to see if the target file exists, and uses `FileCreateBlank` to create it if necessary.

```pebakery
[Main]
Title=FileCreateBlank
Description=Show the usage of FileCreateBlank.
Level=5
Version=1
Author=Homes32

[Variables]
%grubMenu%=C:\Temp\menu.lst

[process]
If,Not,ExistFile,%grubMenu%,FileCreateBlank,%grubMenu%
TXTAddLine,%grubMenu%,"TITLE Main Menu",APPEND
```