# List,Sort

Sorts a list. **Case Insensitive.**

## Syntax

```pebakery
List,Sort,<%ListVar%>,<SortOrder>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| SortOrder | One of the following: |
|| ASC - Sort in Ascending order. |
|| DESC - Sort in Descending order. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. **Default:** `\|` |

## Remarks



## Related

[List,SortX](./SortX.md) 

## Examples

### Example 1

Sort a list of strings.

```pebakery
[Main]
Title=List-Sort Example 1
Description=Demonstrate usage of List,Sort.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|UlTiMaTe|StarteR|enterprise|Professional|starter|Enterprise|PrOfEsSiOnAl|Starter|Ultimate

[Process]
List,Sort,%myList%,ASC
Message,"myList: %myList%"
```

### Example 2

Sort a numerical list.

```pebakery
[Main]
Title=List-Sort Example 2
Description=Demonstrate usage of List,Sort.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=10|98|50|32|0|1|5|2|4|3

[Process]
List,Sort,%myList%,ASC
Message,"myList: %myList%"
```

### Example 3

Sort a mixed list.

```pebakery
[Main]
Title=List-Sort Example 3
Description=Demonstrate usage of List,Sort.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|UlTiMaTe|10|StarteR|enterprise|50|Professional|2|98|0|4|starter|Enterprise|1|PrOfEsSiOnAl|2|5|3|Starter|Ultimate

[Process]
List,Sort,%myList%,DESC
Message,"myList: %myList%"
```