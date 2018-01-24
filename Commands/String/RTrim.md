# StrFormat,RTrim

Removes a number of characters from the right-hand side of a string.

## Syntax

```pebakery
StrFormat,RTrim,<String>,<Count>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| Count | The number of characters to return. |
| DestVar | The variable where the result will be saved. |

## Remarks

If `Count` exceeds the string length an empty string is returned.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,SubStr](./SubStr.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,UCase](./UCase.md), [StrFormat,LCase](./LCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-RTrim Example
Description=Demonstrate usage of StrFormat,RTrim.
Level=5
Version=1
Author=Homes32

[variables]
%string%="The quick brown fox jumps over the lazy dog."
%count%=19

[process]
StrFormat,RTrim,%string%,%count%,%result%
Message,"After removing %count% characters from the right, the remaining string is: %result%"
```