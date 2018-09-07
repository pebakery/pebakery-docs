# StrFormat,PadRight

Left-aligns the characters in a string by padding them with a specified character on the right, up to a specified total length.

## Syntax

```pebakery
StrFormat,PadRight,<String>,<Count>,<PadChar>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to align/pad. |
| Count | The number of characters to expand the resulting string with padding. |
| PadChar | Character to use for padding. |
| DestVar | The variable where the result will be saved. |

## Remarks

If the `String` length exceeds the number of characters defined by `Count` no padding will be applied.

## Related

[StrFormat,PadLeft](./PadLeft.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-RightPad Example
Description=Pad the right hand side of a string with 0's up to 7 characters.
Level=5
Version=1
Author=Homes32

[Variables]
%myString%=32

[Process]
StrFormat,PadRight,%myString%,7,0,%Dest%
Message,%Dest%
```