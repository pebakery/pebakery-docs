# StrFormat,StartTrim

Removes specific character(s) from the beginning of a string.

## Syntax

```pebakery
StrFormat,StartTrim,<String>,<TrimChars>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| TrimChars | The character(s) to remove. Leave blank to remove white-space characters.|
| DestVar | The variable where the result will be saved. |

## Remarks

The trim operation stops when a character different from `TrimChars` is encountered. 

If `TrimChars` do not exist at the beginning of the string it will not be modified.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,Mid](./Mid.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,EndTrim](./EndTrim.md), [StrFormat,UCase](./UCase.md), [StrFormat,LCase](./LCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-StartTrim Example 1
Description=Demonstrate usage of StrFormat,StartTrim.
Level=5
Version=1
Author=Homes32

[variables]
%string%="$@PhoenixPE"

[process]
StrFormat,StartTrim,%string%,"$@",%result%
Message,"After removing [$@] from the beginning of [%string%] the remaining string is [%result%]."
```

### Example 2

Remove white-space from the beginning of a string.

```pebakery
[Main]
Title=StrFormat-StartTrim Example 2
Description=Demonstrate usage of StrFormat,StartTrim.
Level=5
Version=1
Author=Homes32

[variables]
%string%="    Hello World!"

[process]
StrFormat,StartTrim,%string%,"",%result%
Message,"After removing white-space from the beginning of [%string%] the remaining string is [%result%]."
```
