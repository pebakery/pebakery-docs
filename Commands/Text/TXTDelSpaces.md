# TXTDelSpaces

Delete all spaces from the beginning and end of each line inside a text file.

## Syntax

```pebakery
TXTDelSpaces,<FileName>
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the file. |

## Remarks

This command was created to make some specific INI files smaller in overall size.

If `FileName` does not exist the operation will fail.

## Related

[TXTAddLine](./TXTAddLine.md), [TXTDelEmptyLines](./TXTDelEmptyLines.md), [TXTDelLine](./TXTDelLine.md)

## Examples

### Example 1

```pebakery
TxtDelSpaces,C:\myFile.txt
```