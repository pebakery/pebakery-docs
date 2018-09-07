# List,Append

Append a value to the end of a list.

## Syntax

```pebakery
List,Append,<%ListVar%>,<Value>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Value | The value to append. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. Case Insensitive. **Default:** `\|` |

## Remarks

To insert an item at the beginning of a list use the `List,Insert` command.

## Related

[List,Insert](./Insert.md), [List,Set](./Set.md)

## Examples

### Example 1

Append _PEBakery_ to the end of a list.

```pebakery
[Main]
Title=List-Append Example
Description=Demonstrate usage of List,Append.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|Professional|Enterprise|Starter|Ultimate

[Process]
List,Append,%myList%,"PEBakery"
Message,"myList: %myList%"
```
