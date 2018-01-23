# StrFormat,Mult

Multiplies two numbers.

**This command has been deprecated and may be removed in a future release. It is recommended that you update your code to use `Math,Mul` as soon as possible to avoid breaking your script.**

## Syntax

```pebakery
StrFormat,Mult,<%DestVar%>,<Integer>
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | Variable containing the number to multiply. |
| Integer | The number to multiply `DestVar` by. |

## Remarks

The result of the operation will be written back into `%DestVar%`.

## Related

[StrFormat,Div](./Div.md), [Math,Div](../Math/Div.md), [Math,Mul](../Math/Mul.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Mult Example
Description=Show usage of the StrFormat,Mult Command
Author=Homes32
Level=5

[Variables]
%int%=20

[Process]
StrFormat,Mult,%int%,10
Message,"20 * 10 = %int%"
```