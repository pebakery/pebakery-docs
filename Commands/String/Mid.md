# StrFormat,Mid

Extracts a number of characters from a specific starting point in a string.

## Syntax

```pebakery
StrFormat,Mid,<String>,<StartPos>,<Count>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| StartPos | The character position from the left to start reading. |
| Count | The number of characters to return. |
| DestVar | The variable where the result will be saved. |

## Remarks

If `Count` exceeds the string length then the entire remainder of the string is returned.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,UCase](./UCase.md), [StrFormat,LCase](./LCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Mid Example
Description=Demonstrate usage of StrFormat,Mid.
Level=5
Version=1
Author=Homes32

[variables]
%string%="The quick brown fox jumps over the lazy dog."
%start%=21
%count%=10

[process]
StrFormat,Mid,%string%,%start%,%count%,%result%
Message,"The %count% characters starting from %start% are: %result%"
```