# StrFormat,Len

Returns the number of characters in a string.

## Syntax

```pebakery
StrFormat,Len,<String>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| DestVar | The variable where the result will be saved. |

## Remarks

None.

## Related

[StrFormat,Left](./Left.md), [StrFormat,SubStr](./SubStr.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,UCase](./UCase.md), [StrFormat,LCase](./LCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Len Example
Description=Demonstrate usage of StrFormat,Len.
Level=5
Version=1
Author=Homes32

[variables]
%string%="The quick brown fox jumps over the lazy dog."

[process]
StrFormat,Len,%string%,%length%
Message,"The number of characters is: %length%"
```