# Math,BoolOr

Performs an OR test on two boolean values.

A true output results if any one of the values is true.

## Syntax

```pebakery
Math,BoolOr,<%DestVar%>,<Vaue1>,<Value2>
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable where the result will be stored. |
| Value1 | The first value  in the equation. |
| Value2 | The second value in the equation. |

## Remarks

PEBakery supports standard boolean `True`, `False` comparisons, as well as C-Style integer `Non-Zero = True` and `Zero = False` comparisons.

## Related

[BoolAnd](./BoolAnd.md), [BoolNot](./BoolNot.md), [BoolXor](./BoolXor.md)

## Examples

### Example 1

```pebakery
[Main]
Title=Math-BoolOr Example
Description=Show usage of the Math,BoolOr Command
Author=Homes32
Level=5

[Variables]

[Process]
Math,BoolOr,%result1%,True,True
Math,BoolOr,%result2%,True,False
Math,BoolOr,%result3%,False,True
Math,BoolOr,%result4%,False,False

// Int Bool
Math,BoolOr,%result5%,2,1
Math,BoolOr,%result6%,2,0
Math,BoolOr,%result7%,0,1
Math,BoolOr,%result8%,0,0

// Output Result
Message,"Boolean OR Comparison:#$x[True/True] Return: %result1%#$x[True/False] Return: %result2%#$x[False/True] Return: %result3%#$x[False/False] Return: %result4%#$x[2/1] Return: %result5%#$x[2/0] Return: %result6%#$x[0/1] Return: %result7%#$x[0/0] Return: %result8%"
```