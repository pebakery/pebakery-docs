# Math,BitNot

Performs a bitwise NOT operation.

## Syntax

```pebakery
Math,BitNot,<%DestVar%>,<Value>[,Size]
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable where the result will be stored. |
| Value | The value to operate on. |
| Size | **(Optional)** Size of the `Value` in bits: `8` `16` `32` `64` |

## Remarks

Default bit size is 32bit.

## Related

[BitAnd](./BitAnd.md), [BitOr](./BitOr.md), [BitShift](./BitShift.md), [BitXor](./BitXor.md)

## Examples

### Example 1

```pebakery
[Main]
Title=Math-BitNot Example
Description=Show usage of the Math,BitNot Command
Author=Homes32
Level=5

[Variables]

[Process]
Math,BitNot,%result%,106

// Output Result
Message,"Bitwise NOT:#$x#$x00000000000000000000000001101010 (106)#$x11111111111111111111111110010101 (4294967189)#$x#$xReturn: %result%"
```