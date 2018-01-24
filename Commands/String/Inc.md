# StrFormat,Inc

Increments a number or letter by a value of *n*.

## Syntax

```pebakery
StrFormat,Inc,<%DestVar%>,<Integer>
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable containing the value to increment. |
| Integer | Increase the value of `DestVar` by `Integer`. |

## Remarks

The result of the operation will be written back into `%DestVar%`.

This command supports letters of the alphabet as well as integers, allowing you to cycle through a range of drive letters.

`Integer` must be a positive value. If you need to Decrement a number or drive letter use `StrFormat,Dec`.

## Related

[Loop](../Branch/Loop.md), [Math,Add](../Math/Add.md), [Math,Sub](../Math/Sub.md), [StrFormat,Dec](./Dec.md)

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Inc Example
Description=Demonstrate usage of StrFormat,Inc.
Level=5
Version=1
Author=Homes32

[variables]
%int%=10

[process]
StrFormat,Inc,%int%,5
Message,"Inc [10] by [5] = [%int%]"
```

### Example 2

In this example we use `StrFormat,Inc` in conjunction with the `Loop` command to cycle through the drive letters A-Z  searching for notepad.exe.

```pebakery
[Main]
Title=Loop-A-Z Example
Description=Demonstrate how to loop through drive letters searching for a file.
Level=5
Version=2
Author=Homes32

[variables]

[process]
Set,%searchFile%,"Windows\notepad.exe"
Loop,%ScriptFile%,Search-Drives,1,26
If,EXISTFILE,%fullPath%,ShellExecute,OPEN,%fullPath%

[Search-Drives]
Set,%drive%,A
StrFormat,Inc,%drive%,#c
Echo,"Searching drive [%drive%:\]"
Set,%fullPath%,%drive%:\%searchFile%
If,EXISTFILE,%fullPath%,Loop,BREAK
```