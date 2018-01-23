# StrFormat,Ceil

Rounds a value up to the next formatted "size" (KB/MB/GB/TB/PB).

## Syntax

```pebakery
StrFormat,Ceil,<%Integer%>,<CeilTo>
```

### Arguments

| Argument | Description |
| --- | --- |
| Integer | Variable containing the number to round up. |
| CeilTo | Size to round up to. Can be one of the following: |
|| <Int> - An positive integer representing the number of bytes to Ceil. |
|| K - Round up to the next Kilobyte |
|| M - Round up to the next Megabyte |
|| G - Round up to the next Gigabyte |
|| T - Round up to the next Terabyte |
|| P - Round up to the next Petabyte |

## Remarks

The `Integer` variable is overwritten with the result of the `StrFormat,Ceil` operation.

This command can be used in conjunction with `StrFormat,IntToBytes` to return at human readable size rounded up to the specified ceiling.

For mathematical Ceiling operations use the `Math,Ceil` command.

## Related

[Math,Ceil](../Math/Ceil.md), [Math,Floor](../Math/Floor.md), [Math,Round](../Math/Round.md), [StrFormat,Floor](./Floor.md), [StrFormat,IntToBytes](./IntToBytes.md), [StrFormat,Round](./Round.md)

## Examples

### Example 1

In this example we get the size of a directory in bytes, then use `StrFormat,Ceil` to round up to the next Gigabyte and finally format our result with `StrFormat,IntToBytes`.

```pebakery
[Main]
Title=StrFormat-Ceil
Description=Show the usage of StrFormat,Ceil.
Level=5
Version=1
Author=Homes32

[Variables]
%Dir%=C:\Windows\System32

[process]
DirSize,%Dir%,%Bytes%
// Lets see what our formatted size is before rounding
StrFormat,IntToBytes,%Bytes%,%StrSize%
// Round Bytes up to the next Gigabyte
StrFormat,Ceil,%Bytes%,g
// Use StrFormat to convert the size to a more human readable format.
StrFormat,IntToBytes,%Bytes%,%StrCeilSize%
Message,"Bytes: [%Bytes%]#$xFormatted: [%StrSize%]#$xCeil: [%StrCeilSize%]"
```