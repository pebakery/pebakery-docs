# StrFormat,ReplaceX

Replaces all occurrences of a substring within a string. **Case Sensitive.**

## Syntax

```pebakery
StrFormat,ReplaceX,<String>,<SearchString>,<ReplaceString>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to read. |
| SearchString | The string to find within `String`. |
| ReplaceString | The replacement string. |
| DestVar | The variable where the result will be saved. |

## Remarks

If the `SubString` is not found `%DestVar%` will not be modified.

## Related

[StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,SubStr](./SubStr.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,LCase](./LCase.md), [StrFormat,UCase](./UCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,Split](./Split)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-ReplaceX Example
Description=Demonstrate usage of StrFormat,ReplaceX.
Level=5
Version=1
Author=Homes32

[variables]
%string%="The quick Brown fox jumps over the lazy brown dog."
%search%="brown"
%replace%="red"

[process]
StrFormat,ReplaceX,%string%,%search%,%replace%,%result%
Message,"Substring [%search%] was replaced by [%replace%]: %result%"
```