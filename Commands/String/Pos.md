# StrFormat,Pos

Returns the position of the given SubString inside the specified String. **Case Insensitive.**

## Syntax

```pebakery
StrFormat,Pos,<String>,<SubString>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| SubString | The string to find within `String`. |
| DestVar | The variable where the result will be saved. |

## Remarks

If the `SubString` is not found the `%DestVar%` will return zero.

If multiple occurrences of `SubString` exist within the string only the first occurrence will be returned.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,Mid](./Mid.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,LCase](./LCase.md), [StrFormat,UCase](./UCase.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Pos Example
Description=Demonstrate usage of StrFormat,Pos.
Level=5
Version=1
Author=Homes32

[variables]
%string%="The quick brown fox jumps over the lazy dog."
%subStr%="fox"

[process]
StrFormat,Pos,%string%,%subStr%,%result%
Message,"Substring [%subStr%] is at position: %result%"
```