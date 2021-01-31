# StrFormat,LTrim

Removes a number of characters from the left-hand side of a string.

## Syntax

```pebakery
StrFormat,LTrim,<String>,<Count>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| Count | The number of characters to remove. |
| DestVar | The variable where the result will be saved. |

## Remarks

If `Count` exceeds the string length an empty string is returned.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,Mid](./Mid.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,UCase](./UCase.md), [StrFormat,LCase](./LCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-LTrim Example
Description=Demonstrate usage of StrFormat,LTrim.
Level=5
Version=1
Author=Homes32

[variables]
%string%="The quick brown fox jumps over the lazy dog."
%count%=19

[process]
StrFormat,LTrim,%string%,%count%,%result%
Message,"After removing %count% characters from the left, the remaining string is: %result%"
```