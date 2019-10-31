# StrFormat,NTrim

Removes any and all numbers from the end of a string.

## Syntax

```pebakery
StrFormat,NTrim,<String>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| DestVar | The variable where the result will be saved. |

## Remarks

If no numbers exist at the end of the string it will not be modified.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,Mid](./Mid.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,UCase](./UCase.md), [StrFormat,LCase](./LCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-NTrim Example
Description=Demonstrate usage of StrFormat,NTrim.
Level=5
Version=1
Author=Homes32

[variables]
%string%="ABCDEFG12345678"

[process]
StrFormat,NTrim,%string%,%result%
Message,"After removing numbers from the end the remaining string is: %result%"
```