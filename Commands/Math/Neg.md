# Math,Neg

Calculates the additive inverse of a value *(n * -1)*.

## Syntax

```pebakery
Math,Neg,<%DestVar%>,<Value>
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable where the result will be stored. |
| Value | The value to invert. |

## Remarks

None.

## Related

## Examples

### Example 1

```pebakery
[Main]
Title=Math-Neg Example
Description=Show usage of the Math,Neg Command
Author=Homes32
Level=5

[Variables]

[Process]
Math,Neg,%neg%,32
Message,"32: %neg%"
Math,Neg,%neg%,-32
Message,"-32: %neg%"
```