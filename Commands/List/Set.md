# List,Set

Writes a value to a specific location in a list structure.

## Syntax

```pebakery
List,Set,<%ListVar%>,<Index>,<Value>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Index | The index where the item will be written. |
| Value | The value to be written. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. Case Insensitive. **Default:** `\|` |

## Remarks

Specifying an `Index` greater or less then the number of items in the list will result in an error.

## Related

[List,Append](./Append.md), [List,Insert](./Insert)

## Examples

### Example 1

Write _PEBakery_ to the 3rd position in a list.

```pebakery
[Main]
Title=List-Set Example
Description=Demonstrate usage of List,Set.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|Professional|Enterprise|Starter|Ultimate

[Process]
List,Set,%myList%,3,"PEBakery"
Message,"myList: %myList%"
```
