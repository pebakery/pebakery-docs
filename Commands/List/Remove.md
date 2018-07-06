# List,Remove

Removes all occurrences of a value from a list. **Case Insensitive.**

## Syntax

```pebakery
List,Remove,<%ListVar%>,<Value>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Value | The value to remove. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. **Default:** `\|` |

## Remarks

If the `Value` is not found `%ListVar%` will not be modified.

## Related

[List,RemoveAt](./RemoveAt.md), [List,RemoveX](./RemoveX.md)

## Examples

### Example 1

Remove _Ultimate_ from a list.

```pebakery
[Main]
Title=List-Remove Example 1
Description=Demonstrate usage of List,Remove.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|UlTiMaTe|StarteR|Professional|Starter|Enterprise|PrOfEsSiOnAl|Starter|Ultimate

[Process]
List,Remove,%myList%,"Ultimate"
Message,"myList: %myList%"
```
