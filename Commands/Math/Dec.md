# Math,Dec

Converts a a hexadecimal string to it's numeric representation.

## Syntax

```pebakery
Math,Dec,<%DestVar%>,<Hex>[,BitSize]
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable where the result will be stored. |
| Hex | The hex string to be converted. Strings must be prefixed with `0x`. |
| Size | **(Optional)** Size of the number in bits: `8` `16` `32` `64`. (Default is 32) |

## Remarks

Negative integer conversion is not supported.

## Related

[Math,Hex](./Hex.md)

## Examples

### Example 1

```pebakery
[Main]
Title=Math-Dec Example
Description=Show the usage of Math,Dec.
Level=5
Version=1
Author=Homes32

[Variables]

[process]
Math,Dec,%result1%,0xDEADBEEF
Math,Dec,%result2%,0x054C5638
Math,Dec,%result3%,0x8BADF00D

Message,"Input: [0xDEADBEEF] Dec: [%result1%]#$x#$xInput: [0x054C5638] Dec: [%result2%]#$x#$xInput: [0x8BADF00D] Dec: [%result3%]"
```