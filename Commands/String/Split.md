# StrFormat,Split

Splits up a string into substrings based on the given delimiters.

## Syntax

```pebakery
StrFormat,Split,<String>,<Delimiter>,<Index>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | The string to split. |
| Delimiter | The delimiter used to split out the substrings. |
| Index | An integer representing the number of times the `String` will be split. |
|| 0 - Contains the number of times the `String` will be split using the given `Delimiter`. |
|| 1...n - The occurrence of the delimiter to split into `DestVar`. |
| DestVar | The variable where the result will be saved. |

## Remarks

This command is most often used in conjunction with the `Loop` command to split up a given string separated by a known delimiter, such as a space, comma, or a `|` character, and act on the individual components.

## Related

[Loop](../Branch/Loop.md), [StrFormat,Left](./Left.md), [StrFormat,Right](./Right.md), [StrFormat,Len](./Len.md), [StrFormat,SubStr](./SubStr.md), [StrFormat,RTrim](./RTrim.md), [StrFormat,LTrim](./LTrim.md), [StrFormat,CTrim](./CTrim.md), [StrFormat,NTrim](./NTrim.md), [StrFormat,LCase](./LCase.md), [StrFormat,UCase](./UCase.md), [StrFormat,Pos](./Pos.md), [StrFormat,PosX](./PosX.md), [StrFormat,Replace](./Replace.md), [StrFormat,ReplaceX](./ReplaceX.md)

## Examples

### Example 1

This example script uses the `Loop` command to display individual words in the supplied string.

```pebakery
[Main]
Title=StrFormat-Split Example
Description=Demonstrate usage of StrFormat,Split.
Level=5
Version=1
Author=Homes32

[variables]
%string%="The quick brown fox jumps over the lazy dog."

[process]
// Retrieve the number of times the string will be split using a [space] character. (Index: 0)
// We can use " " or #$s to represent the [space] character.
StrFormat,SPLIT,%string%,#$s,0,%count%

// Start a loop using the count we retrieved from Index: 0 to loop through the words.
Loop,%ScriptFile%,DisplayWords,1,%count%

[DisplayWords]
StrFormat,Split,%string%," ",#c,%result%
Message,"Split [#c] of [%count%]: %result%"
```