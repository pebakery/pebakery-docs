# LoopLetter

Loops through a range of letters in alphabetical order.

`LoopLetterEx` is an extended form of the standard `LoopLetter` command that allows passing parameters by reference as well as by value.

## Syntax

```pebakery
LoopLetterEx,<FileName>,<Section>,<StartLetter>,<EndLetter>[,Parameters]
```

```pebakery
LoopLetterEx,BREAK
```

### Arguments

#### Version 1

| Argument | Description |
| --- | --- |
| FileName | The full path to the script containing the `Section` to execute. Hint: Use `%ScriptFile%` to reference the current script. |
| Section | The [Section] to execute. |
| StartLetter | The initial letter to start from. Each time the loop finishes the letter will be incremented lexicographically. |
| EndLetter |  The final letter to be reached by increment `StartLetter`. Once this letter is reached the loop stops. |
| Parameters | **(Optional)** Parameters to pass to the `Section` being executed. Parameters must be defined as either `In=` or `Out=`. |
|| `In=<%variable%>` - Pass by value. |
|| `Out=<%variable%>` - Pass by reference. If the variable does not exist it will be created. | 

#### Version 2

| Argument | Description |
| --- | --- |
| BREAK | Immediately exits the loop. The script will continue processing with the next line following the `LoopLetterEx` command. |

### Tokens

The following tokens are passed by PEBakery and can be used to perform additional operations within the loop.


| Token | Description |
| --- | --- |
| `%^SIPARAM_1%`, `%^SIPARAM_2%`, `%^SIPARAM_3%`, etc. | Used within a `Section` to access any parameters passed. The numbering scheme starts from `1` and continues in the order the parameters were passed. These tokens are discarded when the section is finished processing. |
| `%^SIPARAM_COUNT%` | Contains the number of parameters passed to `Section`. |
| `%^RET%` | Return a value from the `Section`. This token is not affected by the constraints of `System,SetLocal` and can be used to return the value of an isolated variable to the main process. `%^RET%` is volatile so if you need to preserve the return value copy it into a local variable. |
| `%^LOOP_IDX%` | Contains the current value of the loop relative to `StartValue` and `EndValue`. |
| `%^SOPARAM_1%`, `%^SOPARAM_2%`, `%^SOPARAM_3%`, etc.| References an `Out=` variable inside the called section. The numbering scheme starts from `1` and continues in the order the `Out=` parameters were passed. These tokens are discarded when the section is finished processing. |

## Remarks

PEBakery allows an unlimited number of parameters to be passed to the `[section]` being executed.

Although the parameters themselves are passed by value using tokens, all variables are in the scope of the entire script, so the original values can modified by referencing them by name. If required, you can use the `System,SetLocal` command to isolate variables modified within the running section.

## Related

[ForEach](./ForEach.md), [ForRange](./ForRange.md), [Loop](./Loop.md), [LoopLetter](./LoopLetter.md), [System,SetLocal](../System/SetLocal.md), [System,EndLocal](../System/EndLocal.md)

## Examples

### Example 1

This example shows how we can cycle through the drive letters A-Z searching for notepad.exe.

```pebakery
[Main]
Title=LoopLetter-A-Z Example
Description=Demonstrate how to loop through drive letters searching for a file.
Level=5
Version=2
Author=Homes32

[variables]

[process]
Set,%searchFile%,"Windows\notepad.exe"
LoopLetter,%ScriptFile%,Search-Drives,A,Z
If,EXISTFILE,%fullPath%,ShellExecute,OPEN,%fullPath%

[Search-Drives]
Echo,"Searching drive [%^LOOP_IDX%:\]"
Set,%fullPath%,%^LOOP_IDX%:\%searchFile%
If,EXISTFILE,%fullPath%,Loop,BREAK
```