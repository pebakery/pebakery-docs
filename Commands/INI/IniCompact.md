# IniCompact

Compacts an .ini file, removing extra whitespace such as leading/trailing spaces and padding between key=value pairs.

## Syntax

```pebakery
IniCompact,<FileName>
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the file. |

## Remarks

If `FileName` does not exist the operation will fail.

## Example 1

Lets assume we have the following .ini file:

```pebakery
; C:\myFile.ini
     [mySection]
myKey=myValue
anotherKey   =     anotherValue
cow= moo
```

Compact the file C:\myFile.ini

```pebakery
IniCompact,C:\myFile.ini
```

Result:

```pebakery
; C:\myFile.ini
[mySection]
myKey=myValue
anotherKey=anotherValue
cow=moo
```