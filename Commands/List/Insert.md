# List,Insert

Insert a new value into a specific location in a list.

## Syntax

```pebakery
List,Insert,<%ListVar%>,<Index>,<Value>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Index | The index where the item will be written. |
| Value | The value to insert. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. Case Insensitive. **Default:** `\|` |

## Remarks

`List,Insert` will not overwrite an existing index value, rather it will push the existing value and subsequent items down the list.

Specifying an `Index` greater then the number of items +1 or less then the number of items in the list will result in an error.

## Related

[List,Append](./Append.md), [List,Set](./Set.md)

## Examples

### Example 1

Prepend _PEBakery_ to the beginning of a list.

```pebakery
[Main]
Title=List-Insert Example 1
Description=Demonstrate usage of List,Insert.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|Professional|Enterprise|Starter|Ultimate

[Process]
List,Insert,%myList%,1,"PEBakery"
Message,"myList: %myList%"
```

### Example 2

Insert _PEBakery_ to the 4th position in a list.

```pebakery
[Main]
Title=List-Insert Example 2
Description=Demonstrate usage of List,Insert.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|Professional|Enterprise|Starter|Ultimate

[Process]
List,Insert,%myList%,4,"PEBakery"
Message,"myList: %myList%"
```