# StrFormat,Dec

Decrements a number or letter by a value of *n*.

## Syntax

```pebakery
StrFormat,Dec,<%DestVar%>,<Integer>
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable containing the value to increment. |
| Integer | Decrease the value of `DestVar` by `Integer`. |

## Remarks

The result of the operation will be written back into `%DestVar%`.

This command supports letters of the alphabet as well as integers, allowing you to cycle through a range of drive letters.

`Integer` must be a positive value. If you need to Increment a number or drive letter use `StrFormat,Inc`.

## Related

[Loop](../Branch/Loop.md), [Math,Add](../Math/Add.md), [Math,Sub](../Math/Sub.md), [StrFormat,Inc](./Inc.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Dec Example
Description=Demonstrate usage of StrFormat,Dec.
Level=5
Version=1
Author=Homes32

[variables]
%int%=10
%letter%=Z

[process]
StrFormat,Dec,%int%,5
StrFormat,Dec,%letter%,1
Message,"Dec [10] by [5] = [%int%]#$xDec [Z] by [1] = [%letter%]"
```