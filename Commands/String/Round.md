# StrFormat,Round

Rounds a value to the nearest formatted "size" (KB/MB/GB/TB/PB).

## Syntax

```pebakery
StrFormat,Round,<%Integer%>,<RoundTo>
```

### Arguments

| Argument | Description |
| --- | --- |
| Integer | Variable containing the number to round. |
| FloorTo | Size to round to. Can be one of the following: |
|| <Int> - An positive integer representing the number of bytes to round to. |
|| K - Round to the Kilobyte |
|| M - Round to the Megabyte |
|| G - Round to the Gigabyte |
|| T - Round to the Terabyte |
|| P - Round to the Petabyte |

## Remarks

The `Integer` variable is overwritten with the result of the `StrFormat,Round` operation.

This command can be used in conjunction with `StrFormat,IntToBytes` to return at human readable size rounded to nearest integer.

For mathematical Rounding operations use the `Math,Round` command.

## Related

[Math,Ceil](../Math/Ceil.md), [Math,Floor](../Math/Floor.md), [Math,Round](../Math/Round.md), [StrFormat,Ceil](./Ceil.md), [StrFormat,Floor](./Floor.md), [StrFormat,IntToBytes](./IntToBytes.md)

## Examples

### Example 1

In this example we get the size of a directory in bytes, then use `StrFormat,Floor` to round to the nearest Gigabyte and finally format our result with `StrFormat,IntToBytes`.

```pebakery
[Main]
Title=StrFormat-Round
Description=Show the usage of StrFormat,Round.
Level=5
Version=1
Author=Homes32

[Variables]
%Dir%=C:\Windows\System32

[process]
DirSize,%Dir%,%Bytes%
// Lets see what our formatted size is before rounding
StrFormat,IntToBytes,%Bytes%,%StrSize%
// Round Bytes to the nearest Gigabyte
StrFormat,Round,%Bytes%,g
// Use StrFormat to convert the size to a more human readable format.
StrFormat,IntToBytes,%Bytes%,%StrFloorSize%
Message,"Bytes: [%Bytes%]#$xFormatted: [%StrSize%]#$xRound: [%StrFloorSize%]"
```