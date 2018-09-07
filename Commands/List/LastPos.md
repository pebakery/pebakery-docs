# List,LastPos

Returns the last position of the given value inside the specified list. **Case Insensitive.**

## Syntax

```pebakery
List,LastPos,<%ListVar%>,<Value>,<%DestVar%>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Value | The value to find within the list. |
| DestVar | The variable where the result will be saved. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. Case Insensitive. **Default:** `\|` |

## Remarks

If the `Value` is not found the `%DestVar%` will return zero.

If multiple occurrences of `Value` exist within the list only the last occurrence will be returned.

## Related

[List,LastPosX](./LastPosX.md), [List,Pos](./Pos.md), [List,PosX](./PosX.md)

## Examples

### Example 1

Get the index for the last occurrence of _Starter_.

```pebakery
[Main]
Title=List-LastPos Example
Description=Demonstrate usage of List,LastPos.
Level=5
Version=1
Author=Homes32

[variables]
%myList%=Home|UlTiMaTe|StarteR|Professional|Starter|Enterprise|PrOfEsSiOnAl|Starter|Ultimate

[process]
List,LastPos,%myList%,Starter,%result%
Message,"Last value of [Starter] is at position: %result%"
```