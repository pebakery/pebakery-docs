# StrFormat,Floor

Rounds a value down to the formatted "size" (KB/MB/GB/TB/PB).

## Syntax

```pebakery
StrFormat,Floor,<%Integer%>,<FloorTo>
```

### Arguments

| Argument | Description |
| --- | --- |
| Integer | Variable containing the number to round down to Floor. |
| FloorTo | Size to round down to. Can be one of the following: |
|| <Int> - An positive integer representing the number of bytes to round down to. |
|| K - Round down to the Kilobyte |
|| M - Round down to the Megabyte |
|| G - Round down to the Gigabyte |
|| T - Round down to the Terabyte |
|| P - Round down to the Petabyte |

## Remarks

The `Integer` variable is overwritten with the result of the `StrFormat,Floor` operation.

This command can be used in conjunction with `StrFormat,IntToBytes` to return at human readable size rounded down to the specified floor.

For mathematical Floor operations use the `Math,Floor` command.

## Related

[Math,Ceil](../Math/Ceil.md), [Math,Floor](../Math/Floor.md), [Math,Round](../Math/Round.md), [StrFormat,Ceil](./Ceil.md), [StrFormat,IntToBytes](./IntToBytes.md), [StrFormat,Round](./Round.md)

## Examples

### Example 1

In this example we get the size of a directory in bytes, then use `StrFormat,Floor` to round down to the next Gigabyte and finally format our result with `StrFormat,IntToBytes`.

```pebakery
[Main]
Title=StrFormat-Floor
Description=Show the usage of StrFormat,Floor.
Level=5
Version=1
Author=Homes32

[Variables]
%Dir%=C:\Windows\System32

[process]
DirSize,%Dir%,%Bytes%
// Lets see what our formatted size is before rounding
StrFormat,IntToBytes,%Bytes%,%StrSize%
// Round Bytes down to the next Gigabyte
StrFormat,Floor,%Bytes%,g
// Use StrFormat to convert the size to a more human readable format.
StrFormat,IntToBytes,%Bytes%,%StrFloorSize%
Message,"Bytes: [%Bytes%]#$xFormatted: [%StrSize%]#$xFloor: [%StrFloorSize%]"
```