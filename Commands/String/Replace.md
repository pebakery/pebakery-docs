# StrFormat,Replace

Replaces all occurrences of a substring within a string. **Case Insensitive.**

## Syntax

```pebakery
StrFormat,Replace,<String>,<SearchString>,<ReplaceString>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| SearchString | The string to find within `String`. |
| ReplaceString | The string to replace `SearchString`. |
| DestVar | The variable where the result will be saved. |

## Remarks

If the `SubString` is not found `%DestVar%` will not be modified.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,SubStr](./SubStr.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,LCase](./LCase.md), [StrFormat,UCase](./UCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,ReplaceX](./ReplaceX.md), [StrFormat,Split](./Split)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Replace Example
Description=Demonstrate usage of StrFormat,Replace.
Level=5
Version=1
Author=Homes32

[variables]
%string%="The quick brown fox jumps over the lazy brown dog."
%search%="brown"
%replace%="red"

[process]
StrFormat,Replace,%string%,%search%,%replace%,%result%
Message,"Substring [%search%] was replaced by [%replace%]: %result%"
```