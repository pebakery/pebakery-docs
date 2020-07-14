# IniWriteTextLine

Write a line of text to a section inside a standard .ini file.

## Syntax

```pebakery
IniWriteTextLine,<FileName>,<Section>,<Line>[,APPEND]
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the file. |
| Section | The section where the string will be written. |
| Line | The string to write. |

### Flags

| Flag | Description |
| --- | --- |
| APPEND | **(Optional)** If specified this will cause the string to be inserted at the end of the section. |

## Remarks

If `FileName` does not exist it will be created using UTF-8 encoding.

Unless the `APPEND` flag is specified the `Line` will be inserted at the beginning of the section.

PEBakery will optimize multiple `IniWriteTextLine` commands in a row into a single write operation.

## Example

Lets assume we have the following .ini file:

```pebakery
// C:\myFile.ini
[mySection]
myKey=myValue
anotherKey=anotherValue
```

In the following example the string `Hello World!` will be written to the beginning of the section.
Additionally the string `Goodbye World!` will be written to the end of the section.

```pebakery
IniWriteTextLine,C:\myFile.ini,mySection,"Hello World!"
IniWriteTextLine,C:\myFile.ini,mySection,"Goodbye World!",APPEND
```

The resulting .ini file:

```pebakery
// C:\myFile.ini
[mySection]
Hello World!
myKey=myValue
anotherKey=anotherValue
Goodbye World!
```
