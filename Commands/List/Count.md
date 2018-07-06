# List,Count

Returns the number of items in a list.

## Syntax

```pebakery
List,Count,<%ListVar%>,<%DestVar%>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| DestVar | The variable where the result will be saved. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. **Default:** `\|` |

## Remarks

The first element of a list is indexed by subscript of 1 (1-based index) and incremented for each additional item in the list.

## Related

## Examples

### Example 1

Use `List,Count` to retrieve the last item in a list.

```pebakery
[Main]
Title=List-Count Example 1
Description=Demonstrate usage of List,Count.
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

### Example 2

Loop through an entire list.

```pebakery
[Main]
Title=List-Count Example 2
Description=Demonstrate usage of List,Count.
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