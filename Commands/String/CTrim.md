# StrFormat,CTrim

Removes specific character(s) from the beginning and end of a string.

## Syntax

```pebakery
StrFormat,CTrim,<String>,<TrimChars>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| TrimChars | The character(s) to remove. Leave blank to remove white-space characters.|
| DestVar | The variable where the result will be saved. |

## Remarks

Each leading and trailing trim operation stops when a character different from `TrimChars` is encountered. 

If `TrimChars` do not exist at the beginning or end of the string it will not be modified.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,Mid](./Mid.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,StartTrim](./StartTrim.md), [StrFormat,EndTrim](./EndTrim.md), [StrFormat,UCase](./UCase.md), [StrFormat,LCase](./LCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-CTrim Example 1
Description=Demonstrate usage of StrFormat,CTrim.
Level=5
Version=1
Author=Homes32

[variables]
%string%="%BaseDir%\Projects\"
%URL%="https://www.google.com"

[process]
StrFormat,CTrim,%string%,"\",%result%
Message,"After removing [\] characters the remaining string is: %result%"
StrFormat,CTrim,%URL%,"https://",%result%
Message,"After removing [https://] characters the remaining string is: %result%"
```

### Example 2

Remove white-space from the beginning and end of strings before concatenating them.

```pebakery
[Main]
Title=StrFormat-CTrim Example 2
Description=Demonstrate usage of StrFormat,CTrim.
Level=5
Version=1
Author=Homes32

[variables]
%string1%="    Hello     "
%string2%="World!"

[process]
StrFormat,CTrim,%string1%,"",%result1%
StrFormat,CTrim,%string2%,"",%result2%
Message,"String1: [%string1%]#$xString2: [%string2%]#$xResult: [%result1% %result2%]"
```