# StrFormat,LCase

Converts a string to lowercase.

## Syntax

```pebakery
StrFormat,LCase,<String>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| DestVar | The variable where the result will be saved. |

## Remarks

None.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,Mid](./Mid.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,UCase](./UCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-LCase Example
Description=Demonstrate usage of StrFormat,LCase.
Level=5
Version=1
Author=Homes32

[variables]
%string%="The Quick BROWN FOX Jumps Over The LAZY DOG."

[process]
StrFormat,LCase,%string%,%result%
Message,"Lowercase string is: %result%"
```