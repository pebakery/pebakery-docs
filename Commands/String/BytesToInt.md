# StrFormat,BytesToInt

Converts a human readable string representing the size of a file or directory to a machine readable integer representing the size in bytes.

Strings can be converted to bytes from KB, MB, GB, TB or PB.

## Syntax

```pebakery
StrFormat,BytesToInt,<String>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| String | String containing the formated size. |
| DestVar | Variable where the resulting bytes will be stored. |

## Remarks

This operation can be used to reverse the `StrFormat,IntToBytes` command and convert human readable sizes into machine readable format.

Whitespace in the string is discarded, so `5.123GB` is treated the same as `5.123 GB`.

## Related

[DirSize](../File/DirSize.md), [FileSize](../File/FileSize.md), [StrFormat, IntToBytes](./IntToBytes), [System,GetFreeSpace](../System/GetFreeSpace.md)

## Examples

### Example 1

In this example we convert a string containing the size `5.274GB` into bytes.

```pebakery
[Main]
Title=BytesToInt
Description=Show the usage of StrFormat,BytesToInt.
Level=5
Version=1
Author=Homes32

[Variables]
%StrSize%="5.274GB"

[process]
// Use StrFormat to convert the human readable format to machine readable format.
StrFormat,BytesToInt,%StrSize%,%Size%
Message,"Size: %StrSize% (%Size% bytes)"
```