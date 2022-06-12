# List,Range

Generate a list of values from a given number range.

## Syntax

```pebakery
List,Range,<%ListVar%>,<Start>,<End>,<Step>
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Start | The starting value in the range. (Integer) |
| End |  The ending value in the range. (Integer) |
| Step | Decrement/Increment by this value until `End` is reached. (Integer) |

## Remarks

Setting `<Start>` equal to `<End>` will produce an empty list.

## Related

[ForRange](../Branch/ForRange.md)

## Examples

### Example 1

Create a list of numbers that increment from 1 to 10.

```pebakery
[Main]
Title=List-Range Example 1
Description=Demonstrate usage of List,Range.
Level=5
Version=1
Author=Homes32

[Variables]

[Process]
List,Range,%myList%,1,11,1
Message,"myList: %myList%"
```

### Example 2

Create a list of numbers that decrement from 10 to 1.

```pebakery
[Main]
Title=List-Range Example 1
Description=Demonstrate usage of List,Range.
Level=5
Version=1
Author=Homes32

[Variables]

[Process]
List,Range,%myList%,10,0,-1
Message,"myList: %myList%"
```
