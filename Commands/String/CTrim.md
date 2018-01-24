# StrFormat,CTrim

Removes specific character(s) from the beginning or end of a string if they exist.

## Syntax

```pebakery
StrFormat,CTrim,<String>,<Chars>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| Chars | The character(s) to trim. |
| DestVar | The variable where the result will be saved. |

## Remarks

If `Chars` do not exist at the beginning or end of the string it will not be modified.

This command can be used to remove (Trim) trailing `\` characters from the start or end of a path, without having a separate statement to check if they exist.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,SubStr](./SubStr.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,UCase](./UCase.md), [StrFormat,LCase](./LCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-CTrim Example
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