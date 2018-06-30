# List,Get

Extracts a specific item from a list.

## Syntax

```pebakery
List,Get,<%ListVar%>,<Index>,<%DestVar%>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Index | The index where the item to retrieve is located. |
| DestVar | The variable where the result will be saved. |
| Delim= | **(Optional)** Delimiter used to separate the `Items` in the list. **Default:** `\|` |

## Remarks

The `List,Count` command can be used to retrieve the number of items in the list.

Specifying an `Index` greater or less then the number of `Items` in the list will result in an error.

## Related

[List,Count](./Count.md)

## Examples

### Example 1

Get the 3rd item in a list.

```pebakery
[Main]
Title=List-Get Example
Description=Demonstrate usage of List,Get.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|Professional|Enterprise|Starter|Ultimate

[Process]
List,Get,%myList%,3,%DestVar%
Message,"Item #3: %DestVar%"
```

### Example 2

Get the last item in a list.

```pebakery
[Main]
Title=List-Get Example
Description=Demonstrate usage of List,Get.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|Professional|Enterprise|Starter|Ultimate

[Process]
List,Count,%myList%,%n%
List,Get,%myList%,%n%,%DestVar%
Message,"Last Item: %DestVar%"
```