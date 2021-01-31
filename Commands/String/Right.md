# StrFormat,Right

Returns a number of characters from the right-hand side of a string.

## Syntax

```pebakery
StrFormat,Right,<String>,<Count>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| Count | The number of characters to return. |
| DestVar | The variable where the result will be saved. |

## Remarks

`Integer` must be a positive value.

If `Count` exceeds the string length then the entire string is returned.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Mid](./Mid.md), [StrFormat,Len](./Len.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,UCase](./UCase.md), [StrFormat,LCase](./LCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Right Example
Description=Demonstrate usage of StrFormat,Right.
Level=5
Version=1
Author=Homes32

[variables]
%string%="The quick brown fox jumps over the lazy dog."
%count%=19

[process]
StrFormat,Right,%string%,%count%,%result%
Message,"The %count% rightmost characters are: %result%"
```