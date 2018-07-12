# List,Sort

Sorts a list into alphabetical/lexicographical order. **Case Insensitive.**

## Syntax

```pebakery
List,Sort,<%ListVar%>,<Order>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Order | One of the following: |
|| ASC - Sort in Ascending order. |
|| DESC - Sort in Descending order. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. Case Insensitive. **Default:** `\|` |

## Remarks

Lexicographical order is not the same as natural order. When sorting a list containing numbers `10|98|50|32|0|1|5|2|4|3` the result will be `0|1|10|2|3|32|4|5|50|98`. This is because in a lexicographical sort each character sorted individually.

>To determine which of two strings comes first in alphabetical order, their first letters are compared. If they differ, then the string whose first letter comes earlier in the alphabet is the one which comes first in alphabetical order. If the first letters are the same, then the second letters are compared, and so on. If a position is reached where one string has no more letters to compare while the other does, then the first (shorter) string is deemed to come first in alphabetical order. [-Wikipedia](https://en.wikipedia.org/wiki/Alphabetical_order)

In our example above the number `1` is smaller then the number `10` so `1` is placed first, followed by `10` because the `1` in ten is larger then the number `2`.

If you need to sort a list in natural/numeric order consider using the `List,SortN` command instead.

## Related

[List,SortN](./SortN.md), [List,SortNX](./SortNX.md), [List,SortX](./SortX.md)

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