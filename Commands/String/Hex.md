# StrFormat,Hex

Convert an integer to it's hexadecimal representation.

## Syntax

```pebakery
StrFormat,Hex,<Integer>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| Integer | Number to convert. |
| DestVar | Variable where the resulting Hex representation will be stored. |

## Remarks

Negative integer conversion is supported.

For backwards compatibility with Winbuilder only 32bit integers are supported at this time.

## Related

None.

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Hex
Description=Show the usage of StrFormat,Hex.
Level=5
Version=1
Author=Homes32

[Variables]
%Int1%=88888888
%Int2%=-2

[process]
StrFormat,Hex,%Int1%,%result1%
StrFormat,Hex,%Int2%,%result2%
Message,"Input: [%Int1%] Hex: [0x%result1%]#$xInput: [%Int2%] Hex: [0x%result2%]"
```