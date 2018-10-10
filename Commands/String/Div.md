# StrFormat,Div

Divides two numbers.

**This command has been depreciated and may be removed in a future release. It is recommended that you update your code to use `Math,Div` as soon as possible to avoid breaking your script.**

## Syntax

```pebakery
StrFormat,Div,<%DestVar%>,<Integer>
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | Variable containing the number to divided. |
| Integer | The number to divide `DestVar` by. |

## Remarks

The result of the operation will be written back into `%DestVar%`.

## Related

[StrFormat,Mult](./Mult.md), [Math,Div](../Math/Div.md), [Math,IntDiv](../Math/IntDiv.md), [Math,Mul](../Math/Mul.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Div Example
Description=Show usage of the StrFormat,Div Command
Author=Homes32
Level=5

[Variables]
%int%=20

[Process]
StrFormat,Div,%int%,10
Message,"20 / 10 = %int%"
```