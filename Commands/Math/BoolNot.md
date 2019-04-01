# Math,BoolNot

Performs an Not test on two boolean values.

## Syntax

```pebakery
Math,BoolNot,<%DestVar%>,<Vaue>
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable where the result will be stored. |
| Value | The value to operate on. |

## Remarks

PEBakery supports standard boolean `True`, `False` comparisons, as well as C-Style integer `Non-Zero = True` and `Zero = False` comparisons.

## Related

[BoolAnd](./BoolAnd.md), [BoolOr](./BoolOr.md), [BoolXor](./BoolXor.md)

## Examples

### Example 1

```pebakery
[Main]
Title=Math-BoolNot Example
Description=Show usage of the Math,BoolNot Command
Author=Homes32
Level=5

[Variables]

[Process]
Math,BoolNot,%result1%,True
Math,BoolNot,%result2%,False

// Int Bool
Math,BoolNot,%result3%,0x132
Math,BoolNot,%result4%,0
   
// Output Result
Message,"Boolean Not Comparison:#$x[True] Return: %result1%#$x[False] Return: %result2%#$x[0x132] Return: %result3%#$x[0] Return: %result4%"
```