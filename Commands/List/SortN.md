# List,SortN

Sorts a list into natural order. **Case Insensitive.**

## Syntax

```pebakery
List,SortN,<%ListVar%>,<Order>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Order | One of the following: |
|| ASC - Sort in Ascending order. |
|| DESC - Sort in Descending order. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. **Default:** `\|` |

## Remarks

Natural order is not the same as lexicographical order. When sorting a list containing numbers `10|98|50|32|0|1|5|2|4|3` the lexicographical result will be `0|1|10|2|3|32|4|5|50|98` whereas the natural result will be `0|1|2|3|4|5|10|32|50|98`. This is because in a lexicographical sort each character sorted individually as opposed to natural order, where multi-digit numbers are ordered as a single character.

If you need to sort a list in lexicographical order consider using the `List,Sort` command instead.

## Related

[List,Sort](./Sort.md), [List,SortNX](./SortNX.md), [List,SortX](./SortX.md) 

## Examples

### Example 1

Sort a list of strings.

```pebakery
[Main]
Title=List-SortN Example 1
Description=Demonstrate usage of List,SortN.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|UlTiMaTe|StarteR|enterprise|Professional|starter|Enterprise|PrOfEsSiOnAl|Starter|Ultimate

[Process]
List,SortN,%myList%,ASC
Message,"myList: %myList%"
```

### Example 2

Sort a numerical list.

```pebakery
[Main]
Title=List-SortN Example 2
Description=Demonstrate usage of List,SortN.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=10|98|50|32|0|1|5|2|4|3

[Process]
List,SortN,%myList%,ASC
Message,"myList: %myList%"
```

### Example 3

Sort a mixed list.

```pebakery
[Main]
Title=List-SortN Example 3
Description=Demonstrate usage of List,SortN.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|UlTiMaTe|10|StarteR|enterprise|50|Professional|2|98|0|4|starter|Enterprise|1|PrOfEsSiOnAl|2|5|3|Starter|Ultimate

[Process]
List,SortN,%myList%,DESC
Message,"myList: %myList%"
```