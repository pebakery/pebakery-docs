# List,Get

Extracts a specific item from a list structure.

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
| Delim= | **(Optional)** Delimiter used to separate the items in the list. Case Insensitive. **Default:** `\|` |

## Remarks

The `List,Count` command can be used to retrieve the number of items in the list.

Specifying an `Index` greater or less then the number of items in the list will result in an error.

## Related

[List,Count](./Count.md)

## Examples

### Example 1

Get the 3rd item in a comma delimited list.

```pebakery
[Main]
Title=List-Get Example 1
Description=Demonstrate usage of List,Get.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home,Professional,Enterprise,Starter,Ultimate

[Process]
// Comma's are reserved, so we must escape (#$c) or quote ("Delim=,") them.
List,Get,%myList%,3,%DestVar%,Delim=#$c
Message,"Item #3: %DestVar%"
```

### Example 2

Get the last item in a list.

```pebakery
[Main]
Title=List-Get Example 2
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

### Example 3

Loop through an entire list.

```pebakery
[Main]
Title=List-Get Example 3
Description=Demonstrate usage of List,Get.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|Professional|Enterprise|Starter|Ultimate

[Process]
List,Count,%myList%,%n%
Loop,%ScriptFile%,GetListItem-Loop,1,%n%

[GetListItem-Loop]
List,Get,%myList%,#c,%DestVar%
Message,"Item [#c/%n%]: %DestVar%"
```