# List,RemoveAt

Removes a value from a specific index in a list.

## Syntax

```pebakery
List,RemoveAt,<%ListVar%>,<Index>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Index | The index containing the value to be removed. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. **Default:** `\|` |

## Remarks

When a list value is removed by it's index the remaining items will be shifted left.

## Related

[List,Remove](./Remove.md), [List,RemoveX](./RemoveX.md)

## Examples

### Example 1

Remove the item in position 4 from a list.

```pebakery
[Main]
Title=List-RemoveAt Example 1
Description=Demonstrate usage of List,RemoveAt.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|UlTiMaTe|StarteR|Professional|Starter|Enterprise|PrOfEsSiOnAl|Starter|Ultimate

[Process]
List,RemoveAt,%myList%,4
Message,"myList: %myList%"
```
