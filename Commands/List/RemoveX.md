# List,RemoveX

Removes all occurrences of a value from a list. **Case Sensitive.**

## Syntax

```pebakery
List,RemoveX,<%ListVar%>,<Value>[,Delim=<Str>]
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

[List,Remove](./RemoveX.md), [List,RemoveAt](./RemoveAt.md)

## Examples

### Example 1

Remove _Starter_ from a list.

```pebakery
[Main]
Title=List-RemoveX Example 1
Description=Demonstrate usage of List,RemoveX.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|UlTiMaTe|StarteR|Professional|Starter|Enterprise|PrOfEsSiOnAl|Starter|Ultimate

[Process]
List,RemoveX,%myList%,"Starter"
Message,"myList: %myList%"
```
