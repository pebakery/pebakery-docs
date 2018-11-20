# Math,Hex

Convert an integer to it's hexadecimal representation.

## Syntax

```pebakery
Math,Hex,<%DestVar%>,<Integer>[,BitSize]
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable where the result will be stored. |
| Integer | The Integer to be converted to Hex. |
| Size | **(Optional)** Size of the number in bits: `8` `16` `32` `64` (Default is 32) |

## Remarks

Negative integer conversion is supported.

## Related

[Math,Dec](./Dec.md), [StrFormat,Hex](../String/Hex.md)

## Examples

### Example 1

```pebakery
[Main]
Title=Math-Hex Example
Description=Show the usage of Math,Hex.
Level=5
Version=1
Author=Homes32

[Variables]

[process]
Math,Hex,%result1%,3735928559
Math,Hex,%result2%,88888888
Math,Hex,%result3%,2343432205
Math,Hex,%result4%,-2,64
Math,Hex,%result5%,-2,32

Message,"Input: [3735928559] Hex: [%result1%]#$x#$xInput: [88888888] Hex: [%result2%]#$x#$xInput: [2343432205] Hex: [%result3%]#$x#$xInput: [-2] Hex: [%result4%] (64bit)#$x#$xInput: [-2] Hex: [%result5%] (32bit)"
```